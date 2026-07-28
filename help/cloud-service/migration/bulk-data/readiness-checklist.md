---
title: 顧客対応チェックリスト
description: エンゲージメント、マシンラーニング、ソース、ターゲットを網羅したチェックリストを利用して、Adobe Commerce as a Cloud Serviceへのデータの一括移行に備える方法をご確認ください。
feature: Cloud
badgeSaas: label="SaaSのみ" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud ServiceおよびAdobe Commerce Optimizer プロジェクト（Adobeが管理するSaaS インフラストラクチャ）にのみ適用されます。"
role: Developer
level: Intermediate
autotag-review: '2026-07-22T19:19:18.443Z'
TQID: 'https://experienceleague.adobe.com/728hkK-dzIPzyuBhuNyOqEE9FxlVGdVc9R2wIRcXobk'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: bd989d82-1e15-4534-88db-f1f51dd77ffa
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
  - id: c32adafa-ed01-4b31-997e-2413013911b0
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
  - id: f08fa0de-a550-4acd-b570-f81cf1d03aaf
subfeature_v2:
  - id: f8ddfd3b-6194-46e8-a176-0e918039be56
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2:
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: 670b6214b28be93a16130552a226a8cadb487324
workflow-type: tm+mt
source-wordcount: 1171
ht-degree: 0%

---

# 導入準備のチェックリスト

{{bulk-data-early-access}}

このチェックリストを使用して、一括データ移行ツールを使用して、[!DNL Adobe Commerce on Cloud]またはオンプレミス インスタンスから[!DNL Adobe Commerce as a Cloud Service]へのデータ移行を準備します。

移行ツールは、Commerce Deployed Engineering （CDE）のエンゲージメントプロセスの一部として配布されます。 ツールへのアクセスは、署名済みのCDE契約書に基づいて行われ、公開されません。

このチェックリストでは、ツールを共有する前に必要なもの（[&#x200B; ステージ 1](#stage-1-before-tool-access)）と、ツールを入手した後に設定と実行を開始する準備ができているものについて説明します（[&#x200B; ステージ 2](#stage-2-before-running-the-migration)）。 一部の項目をAdobeと連携する必要があるため、このチェックリストをAdobe部門と早い段階で確認しましょう。

## ステージ 1：ツールにアクセスする前

移行ツールとドキュメントを提供する前に、次の項目を完了するか、確認します。

- **CDE エンゲージメント** – 署名済みのCommerce デプロイ エンジニアリング契約が有効である必要があります。 ツールへのアクセスは、CDE ライフサイクルの契約書署名ステージで付与されます。 Adobeチームとの連携。
- **スコープアンケートが完了しました** — CDEの検出中にスコープアンケートが完了し、現在のツール機能で移行が実現可能であることを検証し、データフットプリントと複雑さを評価します。 Adobeを導入する前に、このステップを完了しておく必要があります。
- **HIPAA データが確認されていません** — ソースインスタンスにHIPAAで制御されたデータを含めることはできません。 続行する前にこれを確認してください。
- **指定されたIP アドレス** – 移行ツールを実行する静的IP アドレスのリストをAdobe チームに提供します。 これは、Adobe側でネットワークアクセスを設定するために必要です。
- **Target インスタンスがプロビジョニングされました** – 移行を開始する前に、ターゲット [!DNL Adobe Commerce as a Cloud Service] インスタンスをプロビジョニングする必要があります。 Adobeチームと調整し、インスタンスの準備が整ったことを確認します。

## ステージ 2：移行を実行する前

ツールにアクセスできたら、設定と実行を開始する前に、次の項目を準備します。

### 移行マシン

移行ツールは、専用のジャンプボックスなど、自分で制御するマシン上で実行されます。 この機械は次の条件を満たさなければなりません。

- **[!DNL Docker]と[!DNL Docker Compose]がインストールされました** — ツールは[!DNL Docker] ベースです。 `docker`と`docker compose` （またはレガシー`docker-compose`）の両方をインストールし、移行マシンで作業する必要があります。
- **[!DNL Docker]実行権限** – 移行を実行しているユーザーが[!DNL Docker] コマンドを実行することを許可する必要があります。 [!DNL Linux]のユーザーは`docker` グループに属している必要があります。 [!DNL macOS]および[!DNL Windows]では、[!DNL Docker Desktop]が実行中でアクセス可能である必要があります。
- **書き込み可能な作業ディレクトリ** – 移行ツールが抽出されるディレクトリは、移行ユーザーによって完全に書き込み可能である必要があります。 このツールは、実行中にログ、キャッシュ、[!DNL Composer]の依存関係、生成ファイルを書き込みます。
- **十分なディスク領域** – 抽出されたデータ、[!DNL Docker]画像、およびログ出力に十分な空きディスク領域を確保します。 必要な領域は、ソースデータベースのサイズによって異なります。
- **オンプレミス ソース：移行マシンからの直接データベース接続** — オンプレミス ソース インスタンスの場合、移行マシンはソース データベースへの直接ネットワーク アクセスを持っている必要があります。 このツールは、オンプレミスのデータベース接続を自動的に確立しません。 移行コマンドを実行する前に、移行マシンからホスト、ポート、資格情報にアクセスできることを確認します。
- **Cloud CLIがインストールされ、SSH キーが登録されました** — [!DNL Adobe Commerce on Cloud]個のソースインスタンスの場合、[Cloud CLI](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/dev-tools/cloud-cli/cloud-cli-overview)を移行マシンにインストールする必要があります。 SSH公開鍵もアカウントに登録する必要があります。 手順については、[&#x200B; セキュア接続ガイド &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/develop/secure-connections)を参照してください。

### Source インスタンス

- **Source ストア APIにアクセス可能** — ソースストアのREST APIとGraphQL APIには、移行マシンからアクセスできる必要があります。 HTTP Basic認証またはネットワーク制限がソース URLへのAPI トラフィックをブロックしていないことを確認します。
- **Source OAuth資格情報** – 移行ツールはOAuthを使用してソースストアで認証を行います。 ソース [!UICONTROL **管理者**] （[!UICONTROL **システム**] > [!UICONTROL **拡張機能**] > [!UICONTROL Integrations]）で統合を作成または確認し、コンシューマーキー、コンシューマーシークレット、アクセストークン、アクセストークンの準備を整えます。
- **PaaS ソース：Magento Cloud API トークン** — [!UICONTROL **アカウント設定**] > [!UICONTROL **API トークン**]&#x200B;の[Cloud アカウント設定](https://accounts.magento.cloud)から[!DNL Cloud]API トークンを生成します。 ソースが[!DNL Adobe Commerce on Cloud] インスタンスの場合にのみ必要です。
- **Source データベース資格情報** — （オンプレミスのみ）ソース [!DNL MySQL]のデータベース接続の詳細を構成用に準備しています：`host`、`port`、`user`、`password`、および`database`の名前。
- **cron**&#x200B;を一時停止する機能 – データ抽出の期間中、同時の書き込みを防ぐために、ソースインスタンスでcronを停止できる必要があります。
- **統合とバックグラウンド ジョブを一時停止する機能** — ソース データベースに書き込むサードパーティ統合（ERP、OMS、PIM）、スケジュールされたジョブ、またはバックグラウンド プロセスは、抽出ウィンドウで一時停止する必要があります。
- **メンテナンスモードを有効および無効にする機能** — （段階的な移行のみ）メンテナンスウィンドウで段階的な移行を実行する場合は、ソースインスタンスでメンテナンスモードを有効および無効にできる必要があります。

### Target インスタンス

- **テナント IDと組織IDが確認されました** – 設定する前に、Adobe チームから`TARGET_TENANT_ID`と`TARGET_ORG_ID`を取得します。
- **IMS OAuth サーバー間の資格情報** – 移行ツールがターゲットと認証するために必要です。 [Adobe Developer Console](https://developer.adobe.com/console/)を通じて生成されました。 Adobe組織には[!UICONTROL Developer]または[!UICONTROL Admin]のアクセス権が必要です。基本的なユーザーアクセス権だけでは資格情報を作成できません。 選択する正しい製品プロファイルをAdobe チームと調整し、クライアント ID （`ADOBE_IMS_CLIENT_ID`）とクライアント シークレット （`ADOBE_IMS_CLIENT_SECRET`）の準備を整えます。
- **CDMS エンドポイント URL** — Adobe チームによって提供されます。 この値を推測しようとしない。 サンドボックスおよびテスト移行のプリプロダクションエンドポイントと、ライブカットオーバー移行の実稼動エンドポイントの両方が必要です。
- ソースとターゲット間で調整された&#x200B;**コア設定** — ストア設定やシステム設定などのコア設定データは、ツールによって移行されません。 移行前にソースと一致するように、ターゲットで手動で設定します。
- **B2B ストア：B2B機能が一貫して構成されています** — ソースがB2B対応ストアの場合は、移行前に、ソースとターゲットの両方で関連するB2B [!UICONTROL Admin]設定が一貫して構成されていることを確認してください。 必要な特定の設定については、[移行ガイド &#x200B;](migration-guide.md)を参照してください。

### 移行計画

- **移行アプローチが決定** – 開始する前に、どのアプローチがユースケースに適しているかを決定します。
  - 単相移行 – メンテナンスモードは必要ありません。 ドライラン、開発環境またはサンドボックス環境、または抽出中にソースを維持できる移行に適しています。
  - 多相移行 – メンテナンスモードが必要です。 データの一貫性を確保するために、ソースを抽出中にフリーズする必要がある実稼動移行には、複数段階の移行が必要です。
- **メンテナンスウィンドウが計画されました** – 複数段階の移行にのみ適用されます。 メンテナンス期間を事前に計画し、連絡します。 ソースインスタンスは、抽出フェーズと読み込みフェーズの間、エンドユーザーは利用できません。
- **ストアビューコードが確認されました** — ソースインスタンス上のストアビューコード （`STORE_CODE`）を特定します。 デフォルトは`default`ですが、[!UICONTROL Admin] > [!UICONTROL Stores] > [!UICONTROL All Stores]の実際のコードと一致する必要があります。 誤ったストアコードは、移行中のデータ操作に影響を与える可能性があります。

すべての項目を確認したら、[移行サービスアクセスガイド &#x200B;](cdms-access.md)でサービスアクセスを検証し、[移行ガイド &#x200B;](migration-guide.md)で設定と実行の手順を開始する準備が整います。
