---
title: バルクデータ移行ツール
description: 一括データ移行ツールを使用して、既存のAdobe Commerce on Cloud インスタンスから [!DNL Adobe Commerce as a Cloud Service]にデータを移行する方法を説明します。
feature: Cloud
badgeSaas: label="SaaSのみ" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud ServiceおよびAdobe Commerce Optimizer プロジェクト（Adobeが管理するSaaS インフラストラクチャ）にのみ適用されます。"
role: Developer
level: Intermediate
exl-id: 81522de9-df54-4651-b8ed-58956376af86
autotag-review: '2026-07-22T19:18:39.433Z'
TQID: 'https://experienceleague.adobe.com/tkCFabZpBKu-W34wsufHlVIWzCUE8FKm4kK7qZahxBU'
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: dac87252-6066-4d6e-a9d2-f6d84c323de7id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75id: f08fa0de-a550-4acd-b570-f81cf1d03aaf
subfeature_v2: id: f8ddfd3b-6194-46e8-a176-0e918039be56
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2: id: c1579802-ddd4-4214-8a91-97b2066abe11id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: 4c0eca0039bab7d015144dd9ac3885a0b2be0563
workflow-type: tm+mt
source-wordcount: 924
ht-degree: 0%

---

# バルクデータ移行ツール

>[!IMPORTANT]
>
>一括データ移行ツールは現在、早期アクセス中です。 アクセスは、Commerce デプロイドエンジニアリング（CDE）のエンゲージメントプロセスを通じてのみ提供されます。

一括データ移行ツールを使用すると、システム インテグレーターはファーストパーティのコアコマースデータを[!DNL Adobe Commerce on Cloud]またはオンプレミスのインストールから[!DNL Adobe Commerce as a Cloud Service]に移行できます。

バルクデータ移行ツールは、システムインテグレーターが自分の移行マシンで実行するDocker ベースのCLIです。 ソースインスタンスに接続し、ファーストパーティのコアコマースデータを抽出して、Adobe移行サービス（Commerce Data Migration Service）にアップロードし、完了までの進捗状況を監視します。

すべてのコマンドはローカルで実行されるため、移行の開始時間、メンテナンスモードの適用時間、各フェーズの実行時間を制御できます。

## 移行ワークフロー

このツールは、次のステージをエンドツーエンドで管理します。

- **データ抽出** — ソースインスタンス （[!DNL Adobe Commerce on Cloud]またはオンプレミス）から1st パーティコアコマースデータを抽出します。
- **データ読み込み** – 抽出されたデータをターゲット [!DNL Adobe Commerce as a Cloud Service] インスタンスに読み込みます。
- **データ統合検証** — RESTとGraphQL APIの比較およびレコード数の検証を含む、移行後の自動チェックを実行します。

>[!NOTE]
>
>現在、一括データ移行ツールでは、ファーストパーティのコアコマースデータの移行のみがサポートされています。 カスタムデータの移行は現在サポートされていません。 構成設定（ストア設定、システム設定）は自動的に移行されないので、移行前にターゲットインスタンスで個別に設定する必要があります。

## デザイン

バルクデータ移行ツールは、安全で効率的なデータ移行を可能にする分散アーキテクチャに従います。 このツールは、システム インテグレーターが既存の[!DNL Adobe Commerce on Cloud or on-premises instance]から[!DNL Adobe Commerce as a Cloud Service]にデータを移行するのに役立ちます。 移行プロセスについて詳しくは、[移行の概要](../overview.md)を参照してください。

次の画像は、一括データ移行ツールを使用したアーキテクチャとエンドツーエンドのデータフローの詳細を示しています。

![PaaSからSaaSへのデータフローを示すバルクデータ移行ツールアーキテクチャ図](../../assets/bulk-data-diagram.png){zoomable="yes"}

### コンポーネント

| コンポーネント | 役割 |
| --------- | ---- |
| **一括データ移行ツール** | Docker ベースのCLIです。このCLIでは、システム インテグレータが移行マシン上で実行され、ソースからスキーマとデータを読み取り、抽出されたデータをAdobeの移行サービスにアップロードし、ステータス トランジションを駆動することで、パイプライン全体をオーケストレーションします。 |
| **Source インスタンス （Commerce オンクラウドまたはオンプレミス）** | 移行ソース。 このツールは、REST APIとGraphQL APIを介して、SSH トンネル （[!DNL Adobe Commerce on Cloud]）またはデータ抽出用のダイレクトデータベース接続（オンプレミス）を介して接続します。 |
| **Commerce Data Migration Service （CDMS） API** | Adobeで管理されるREST APIは、移行を登録し、ステート移行を調整し、抽出されたデータをアップロードするための安全なエンドポイントを提供します。 移行ツールは、CDMS エンドポイント URLと`.env`設定のIMS資格情報を使用してこのAPIに接続します。 |
| **Commerce Data Migration Service （CDMS） ワーカー** | Adobeで管理されているバックグラウンドサービスは、抽出したデータをターゲットインスタンスに読み込み、読み込み後の整合性の検証を実行します。 |
| **[!DNL Adobe Commerce as a Cloud Service]** | Adobe CommerceのSaaS ベースのバージョンと移行先： 読み込まれたデータを受け取り、整合性の検証中に使用されるカタログ、ライブサーチ、価格ルールサービスを公開します。 |

### データフロー

データは、次の順序でコンポーネント内を移動します。

1. 一括データ移行ツールは、[!DNL Adobe Commerce on Cloud]のSSH トンネルまたはオンプレミスの直接データベース接続を介して、ソースインスタンスからデータベーススキーマとデータを読み取ります。
1. ツールは移行を登録し、抽出したデータをCDMS APIを通じてアップロードします。
1. CDMS ワーカーは、ターゲット [!DNL Adobe Commerce as a Cloud Service] テナントにデータを読み込みます。
1. [!DNL Adobe Commerce as a Cloud Service]は、読み込まれたカタログ データを取り込み、カタログ インデックスを作成します。
1. Commerce Data Migration Service （CDMS） ワーカーは、次のサービスのデータベースチェックサム比較、REST、およびGraphQLを使用して、読み込まれたデータを検証します。

   - **Catalog** （GraphQL） – 商品およびカテゴリーデータ。
   - **ライブサーチ** （REST） – 検索インデックスの正確性。
   - **価格設定ルール** （REST） – 価格とルールのデータ。

1. ツールは、全体にわたって移行ステータスをポーリングし、完了時に最終的な移行レポートを取得します。


## エンゲージメントライフサイクル

バルクデータマイグレーションツールへのアクセスは、Commerce Deployed Engineering （CDE）エンゲージメントを通じてのみ提供されます。 このツールは一般には公開されていません。

一般的なエンゲージメントライフサイクルは次のとおりです。

1. **CDE Discovery** – 最初のスコーピング呼び出しを完了し、データ フットプリントと複雑さを評価し、スコーピング アンケートを完了します。
1. **契約サイン** – 商用契約が有効で、移行範囲が確認されています。 この段階で、移行ツールへのアクセス権が付与されます。
1. **CDEの共同イノベーションとサポート** - Adobeと共同で作業して、環境にツールをインストールし、テスト移行を実行します。
1. **運用開始** – 実稼動カットオーバー移行を実行し、データの整合性の検証を完了します。

## ツール配布

このツールは、CDE エンゲージメントの一部として配布されます。 Adobeの担当者が、以下を含むツールパッケージを提供します。

- Docker ベースのCLIとビルド設定
- すべての必要な環境変数に関するドキュメントを含む`.example.env`設定テンプレート
- ツールのアーキテクチャ、設定リファレンス、カスタム変換とテストフレームワーク、トラブルシューティングガイドに関する包括的な技術ドキュメント

セットアップと操作手順の詳細については、ツール配布パッケージに含まれているドキュメントを参照してください。

## 移行ガイド

次のページでは、準備から実行までの移行ライフサイクル全体を示します。 移行プロセスについて詳しくは、次の順序で確認してください。

1. [顧客対応チェックリスト ](readiness-checklist.md) — ツールへのアクセスをリクエストする前に、エンゲージメント、移行マシン、ソース、およびターゲットの前提条件を確認します。
1. [移行サービスへのアクセスを確認](cdms-access.md) — ツールへのアクセスを取得した後、Commerce Data Migration Service （CDMS） APIに対して、ネットワークの到達性、IMS認証、およびテナント認証を検証します。
1. [一括データ移行を実行](migration-guide.md) — ツールを設定し、ネットワークとインスタンスを準備し、移行を開始します。

完全な設定リファレンス、カスタム変換およびテストフレームワーク、トラブルシューティングガイダンスについては、ツール配布パッケージに含まれるドキュメントを参照してください。
