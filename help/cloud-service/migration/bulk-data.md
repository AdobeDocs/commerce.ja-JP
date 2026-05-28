---
title: バルクデータ移行ツール
description: Bulk Data Migration Toolを使用して、既存のAdobe Commerce on Cloud インスタンスから [!DNL Adobe Commerce as a Cloud Service]にデータを移行する方法を説明します。
feature: Cloud
badgeSaas: label="SaaSのみ" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud ServiceおよびAdobe Commerce Optimizer プロジェクト（Adobeが管理するSaaS インフラストラクチャ）にのみ適用されます。"
role: Developer
level: Intermediate
exl-id: 81522de9-df54-4651-b8ed-58956376af86
TQID: https://experienceleague.adobe.com/4Zx1cFtsyfuy21Af6Ov9pU7ndMW35NyCwlcdlKNTk6Q
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2: id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: 6a3bacace012153f6b8f7c87192d19bf349a2446
workflow-type: tm+mt
source-wordcount: 729
ht-degree: 0%

---

# バルクデータ移行ツール

バルクデータ移行ツールは、PaaSからSaaS環境への安全で効率的なデータ移行を可能にする分散アーキテクチャに従っています。 このツールは、ソリューションの実装が既存のAdobe Commerce on Cloud インスタンス （PaaS）から[!DNL Adobe Commerce as a Cloud Service] （SaaS）にデータを移行するのに役立ちます。 移行プロセスについて詳しくは、[移行の概要](./overview.md)を参照してください。

>[!NOTE]
>
>バルクデータ移行ツールでは、ファーストパーティのコアコマースデータの移行のみがサポートされています。 カスタムデータの移行は現在サポートされていません。

次の画像では、一括データ移行ツールを使用するためのアーキテクチャと主要コンポーネントについて詳しく説明します。

![PaaSからSaaSへのデータフローを示すバルクデータ移行ツールアーキテクチャ図](../assets/bulk-data-diagram.png){zoomable="yes"}

## 移行ワークフロー

データの一括移行ワークフローは、次の手順で構成されます。

1. 移行用に新しい環境を設定します。
1. 古いシステムからデータをコピーします。
1. データを新しいシステムに移行する：
1. 商品カタログを新しいシステムで利用できるようにします。
1. データが正しく移行されたことを確認します。

次の節では、これらの手順について詳しく説明します。

## 一括データ移行ツールへのアクセス

一括データ移行ツールの可用性は次のとおりです。

このツールは現在、デプロイされたエンジニアリングエンゲージメントを通じて利用できます。 ご興味のある方は、Adobe担当者にお問い合わせください。

## ターゲット環境の作成

ソリューション実装者（SI）は、移行のターゲット環境を作成します。 この環境には、ソースインスタンスから移行されたデータが保存されます。

まず、[新しい [!DNL Adobe Commerce as a Cloud Service]  （SaaS） インスタンスを作成](../getting-started.md#create-an-instance)します。

### 抽出ツールの設定

抽出ツールを使用して、ソースインスタンスからデータを抽出します。

1. Adobeから提供されたリンクから抽出ツールをダウンロードします。
1. 抽出ツールで次の環境変数を設定します。
   - 既存のMySQL データベースへの接続の詳細
   - [!DNL Adobe Commerce as a Cloud Service] インスタンスのターゲットテナント ID
   - 次を含むIMS資格情報
      - クライアント ID
      - クライアント秘密鍵
      - IMS スコープ
      - IMS URL - ベース URL。 例：`https://ims-na1.adobelogin.com/`。
      - IMS組織ID

   IMS スコープおよびその他の値の場合、[Adobe Developer Console](https://developer.adobe.com/console/)のプロジェクト内の&#x200B;**資格情報** セクションでOAuth タイプを選択します。 詳細については、抽出ツールに含まれる`.example.env` ファイルを参照してください。

### データの抽出

抽出ツールを実行する前に、ソリューションの実装者は、次の方法を使用してPaaS データベースへのSSH トンネルを確立する必要があります。

```bash
magento-cloud tunnel:open
```

次に、抽出ツールを実行します。

1. PaaS データベースに接続し、そのスキーマを分析し、SaaS テナントスキーマの詳細と比較します。
1. PaaSとSaaS間の共通スキーマ要素に基づいて、抽出および変換計画を生成します。
1. カタログデータ管理サービス（CDMS）を利用してデータを抽出する。

### データを読み込む

Adobeが提供するロードデータツールを実行します。 このツールは次の操作を行います。

1. 移行アカウントを使用してSaaS テナントデータベースに接続します。
1. 積載計画を生成します。
1. 計画を実行し、データをSaaS テナントデータベースに一括で移動します。
1. カタログメディアを処理し、ターゲット環境に転送します。
1. SaaS Redis キャッシュをフラッシュし、テナントのデータベースインデックスを無効にします。

### カタログデータの収集

データが読み込まれると、カタログデータは自動的にSaaS テナントデータベースからカタログサービスに流れます。

カタログサービスでは、このデータをライブサーチと商品レコメンデーションと共有します。 このプロセスに手作業は必要ありません。 取り込みが完了すると、データはすべてのサービスで利用できます。

>[!IMPORTANT]
>
>設定設定は自動的には読み込まれません。 データ移行プロセスを開始する前に、[!DNL Commerce Admin]の現在のカタログ構成設定をメモしてください。 次に、ターゲット [!DNL Adobe Commerce as a Cloud Service]環境に同じ設定を実装します。

### データの完全性の検証

移行後、CDMSは次の自動データ整合性チェックを実行して、移行されたデータの正確性と完全性を確認します。

**API ベースの検証**

CDMSは、検証時に、以前に実行したクエリのRESTおよびGraphQL API応答を、ターゲットインスタンスの対応するレコードと比較します。 移行ステータスに不一致が表示されます。

**データベースレベルの検証**

検証中、CDMSは抽出されたレコード数をカウントし、その数を読み込まれたレコード数と比較します。

**オンデマンド検証（オプション）**

すべてのシステムレコードの包括的な検証を手動でトリガーすることもできます。

>[!NOTE]
>
>このプロセスはリソースを必要とするため、サンドボックス環境でのみ使用します。

完全な検証には次のものが含まれます。

- 事前に抽出されたあらゆるRESTおよびGraphQL API応答を使用した、API ベースの完全な検証
- 見つかった不整合の詳細なレポート
