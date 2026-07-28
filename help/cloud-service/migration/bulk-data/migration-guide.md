---
title: 一括データ移行の実行
description: CLIを使用して、Adobe Commerce PaaSまたはオンプレミスのインスタンスからAdobe Commerce as a Cloud Serviceへの一括データ移行を設定して実行する方法について説明します。
feature: Cloud
badgeSaas: label="SaaSのみ" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud ServiceおよびAdobe Commerce Optimizer プロジェクト（Adobeが管理するSaaS インフラストラクチャ）にのみ適用されます。"
role: Developer
level: Intermediate
autotag-review: '2026-07-22T19:19:07.600Z'
TQID: 'https://experienceleague.adobe.com/z9659Vnf2JLxJ4U5p3tEEjurj5Mg3bfKj68Gheq2AXY'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: bd989d82-1e15-4534-88db-f1f51dd77ffa
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
  - id: c32adafa-ed01-4b31-997e-2413013911b0
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
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
source-wordcount: 2802
ht-degree: 0%

---

# 一括データ移行の実行

{{bulk-data-early-access}}

このガイドは、一括データ移行ツールを使用して、[!DNL Adobe Commerce] PaaSまたはオンプレミスのインストールから[!DNL Adobe Commerce as a Cloud Service]へのデータ移行を実行するための手順ごとの運用上のリファレンスです。 実際の設定値と環境固有の詳細は、設定によって異なります。

開始する前に、[顧客準備チェックリスト &#x200B;](readiness-checklist.md)のすべての項目を完了し、[移行サービスアクセスガイド &#x200B;](cdms-access.md)でAPI アクセスを確認したことを確認してください。

>[!NOTE]
>
>ツール配布パッケージの一部として、ツールのアーキテクチャ、内部設計、データ変換フレームワーク、整合性テストフレームワークに関する包括的な技術文書を提供します。

## 前提条件

- **[!DNL Docker]**&#x200B;と&#x200B;**[!DNL Docker Compose]**&#x200B;は、移行を実行するコンピューターにインストールする必要があります。
- 移行を実行しているユーザーには、`docker`および`docker compose` （または従来の`docker-compose`）コマンドを実行する権限が必要です。 [!DNL Linux]のユーザーは`docker` グループに属している必要があります。 [!DNL macOS]および[!DNL Windows]では、[!DNL Docker Desktop]が実行中でアクセス可能である必要があります。 移行CLIは[!DNL Docker]を繰り返し呼び出し、ここで権限エラーが発生すると、実行がブロックされます。
- 移行を実行する前に、ソースとターゲット間でコア設定が一貫している必要があります。 ストア設定やシステム設定などのコア設定データは、このツールによって移行されません。 移行前に、ターゲット上で個別に設定し、ソースに合わせて調整します。

## ツールパッケージの設定

一括データ移行用の環境を設定します。

>[!VIDEO](https://video.tv.adobe.com/v/3496121)

1. `ccsaas-migration-tools.tar.gz`の内容を抽出します。

1. 抽出した`ccsaas-migration-tools` フォルダーからコマンドをすべて実行します（`bin/console`が存在）。

1. フォルダーがログ、キャッシュ、[!DNL Composer]、および生成されたファイルに対して書き込み可能であることを確認します。

   そのディレクトリの下にあるすべてのファイルとサブフォルダーの所有権を、移行を実行するオペレーティングシステムのユーザーに変更します。これにより、ツールは一貫して読み取りと書き込みを行うことができます。 例：[!DNL Linux]: `chown -R <user>:<group> <project-root>`。

1. サンプルファイル （`.example.env` ～ `.env`、および`.my.cnf.example` ～ `.my.cnf`）をコピーして、プロジェクトルート内の`.env`および`.my.cnf` ファイルを作成し、次の節で説明する値を入力します。

### 設定ファイルの例

リポジトリ ルート内の`.example.env`および`.my.cnf.example` ファイルは、設定の開始点です。 各ファイルを作業名にコピーし、必要な値を入力します。

| サンプルファイル | コピー先 | 内容 |
| --- | --- | --- |
| `.example.env` | `.env` | サポートされているすべての環境変数の注釈付きリスト：パフォーマンス、CDMS、IMS、ターゲット SaaS、ソース URL認証、OAuth、オプションのPaaS値（`.my.cnf`で`id=`が設定されている場合は`MAGENTO_CLOUD_CLI_TOKEN`）。 完全な変数リストは、`.env` ファイルで利用できます。 |
| `.my.cnf.example` | `.my.cnf` | オンプレミス [!DNL MySQL]およびPaaS （`id=project:environment`）の`[section]` レイアウトを参照してください。 `[section]`名は`.env`の`SOURCE_CONNECTION_NAME`と一致する必要があります。 フィールドには、PaaSの`user`、`password`、`host`、`port`、`database`および`id=`が含まれます。 |

## 環境ファイルの設定

プロジェクト ルートの`.env` ファイルは、移行と抽出の設定です。 ソースおよびターゲット URL、OAuth、リモート CDMS接続、SaaSおよびIMS認証、その他のスイッチを含むCLI パイプラインを駆動します。

>[!NOTE]
>
>URLに末尾のスラッシュを含めないでください。 例えば、`https://example.com/`の代わりに`https://example.com`を使用します。

`.env` ファイルを編集し、少なくとも次の値を正しく設定してください。 サポートされている変数の完全なリストについては、`.example.env`のインライン注釈を参照してください。

```shell-session
SOURCE_INSTANCE_URL=https://<source-host>
SOURCE_INSTANCE_GRAPHQL_URL=https://<source-host>/graphql
SOURCE_INSTANCE_REST_URL=https://<source-host>/rest
SOURCE_INSTANCE_CONSUMER_KEY=<consumer_key>
SOURCE_INSTANCE_CONSUMER_SECRET=<consumer_secret>
SOURCE_INSTANCE_ACCESS_TOKEN=<access_token>
SOURCE_INSTANCE_ACCESS_TOKEN_SECRET=<access_token_secret>
```

### ソース OAuth資格情報の設定

>[!VIDEO](https://video.tv.adobe.com/v/3496142)

これらの4つの値は、移行ツールからソースストア APIにリクエストを署名します。 それらを取得するには、ソース [!UICONTROL Admin]を開き、[!UICONTROL **システム**] > [!UICONTROL **拡張機能**] > [!UICONTROL **統合**]&#x200B;に移動します。 統合を作成するか開いて、値を`.env`にコピーします。

```shell-session
SOURCE_INSTANCE_CONSUMER_KEY=<consumer_key>
SOURCE_INSTANCE_CONSUMER_SECRET=<consumer_secret>
SOURCE_INSTANCE_ACCESS_TOKEN=<access_token>
SOURCE_INSTANCE_ACCESS_TOKEN_SECRET=<access_token_secret>
```

### Cloud CLI トークンの設定

>[!NOTE]
>
>これは、[!DNL Adobe Commerce on Cloud]個のソースインスタンスにのみ適用されます。 ツールは、`.my.cnf`から自動的にソースタイプを検出します。 `SOURCE_CONNECTION_NAME` セクションに`id=`行（例：`id=project:production`）が含まれる場合、ソースは[!DNL Adobe Commerce on Cloud]で`MAGENTO_CLOUD_CLI_TOKEN`が必要です。 `id=`のないオンプレミス ソースの場合、このトークンは必要なく、トンネル設定はスキップされます。

1. `https://accounts.magento.cloud`に移動してログインします。

1. プロファイル画像をクリックし、[!UICONTROL **アカウント設定**]&#x200B;を選択します。

1. 「[!UICONTROL **API トークン**]」セクションに移動します。

1. [!UICONTROL **API トークンを作成**]&#x200B;を選択し、わかりやすい名前を付けて、生成されたトークンをコピーします。

1. トークンを`.env`に設定します。

   ```text
   MAGENTO_CLOUD_CLI_TOKEN=<your_magento_cloud_api_token>
   ```

>[!NOTE]
>
>Cloud CLIを初めて使用する場合は、SSH公開鍵をアカウントにも追加する必要があります。 手順については、[&#x200B; セキュア接続ガイド &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/develop/secure-connections)を参照してください。

### Commerce管理者設定の調整

移行前に、次の設定がソースとターゲットの間で一貫していることを確認してください。

>[!NOTE]
>
>移行をスムーズにするために、[!DNL Adobe]では、ターゲットインスタンスのすべてのコア設定をソースと一致させることをお勧めします。

### ターゲット SaaSおよびIMS資格情報の設定

>[!VIDEO](https://video.tv.adobe.com/v/3496167)

ターゲットの[!DNL Adobe Commerce as a Cloud Service] IMSおよびAPI設定です。 テナント ID、組織ID、IMS OAuth サーバー間の資格情報、および環境に適したIMS ホストが必要です。 Adobeチームと連携して、整理、テナント、プロファイルアクセスを行います。 機密値を推測または推定しようとしない。

#### IMS資格情報の生成

[Adobe Developer Console](https://developer.adobe.com/console/)を使用します。 プロジェクトを作成するには、Adobe組織で[!UICONTROL Developer]または[!UICONTROL Admin]のアクセス権が必要です。 基本的なユーザーログインだけでは、APIを追加することはできません。

1. プロジェクトを作成するか、既存のプロジェクトを開いて、[!UICONTROL Add API]を選択します。

1. [!UICONTROL **Adobe Commerce as a Cloud Service**]&#x200B;を選択して続行します。

1. 認証タイプとして「[!UICONTROL **OAuth Server-to-Server**]」を選択して続行します。

1. Adobe チームがこのテナントに期待する製品プロファイルを選択し、[!UICONTROL **設定されたAPIを保存**]&#x200B;を選択します。

1. プロジェクトサイドバーで、[!UICONTROL **OAuth サーバー間**] （または&#x200B;[!UICONTROL **資格情報**]）を開き、クライアント IDとクライアント秘密鍵を`.env`に`ADOBE_IMS_CLIENT_ID`および`ADOBE_IMS_CLIENT_SECRET`としてコピーします。

IMS トークン エンドポイント （`ADOBE_IMS_URL`）は、資格情報の環境と一致する必要があります。

| 階層 | 標準`ADOBE_IMS_URL` |
| --- | --- |
| QAまたはステージング | `https://ims-na1-stg1.adobelogin.com` |
| プリプロダクションまたはプロダクション | `https://ims-na1.adobelogin.com` |

>[!NOTE]
>
>これらのURLの`na1`は、ターゲットインスタンスがプロビジョニングされている地域を表します。 インスタンスが別の地域でプロビジョニングされている場合は、適切な地域識別子に置き換えます。

`ADOBE_IMS_META_SCOPES`は、その資格情報でプロビジョニングされたスコープと一致する必要があります。 `.example.env` ファイルには、完全なコンマ区切りスコープ文字列が参照として含まれています。 Adobeが指示した場合にのみ変更します。

#### [!DNL Adobe I/O]資格情報を環境ファイルにマッピング

[!DNL Developer Console]では、OAuth サーバー間の値は、次のJSON構造に対応するクライアント IDおよびクライアントシークレットとして表示されます。

```json
{
  "client_id": "xxxxxxxxxxxxxxxxxxxxxxxxxxx",
  "client_secret": "xxxxxxxxxxxxxxxxxxxxxxxxxxx"
}
```

それらを`.env`にマッピングします（プレースホルダーの例）。

```shell-session
TARGET_ORG_ID=<org_id>@AdobeOrg
ADOBE_IMS_URL=https://ims-na1.adobelogin.com
ADOBE_IMS_CLIENT_ID=xxxxxxxxxxxxxxxxxxxxxxxxxxx
ADOBE_IMS_CLIENT_SECRET=xxxxxxxxxxxxxxxxxxxxxxxxxxx
ADOBE_IMS_META_SCOPES=AdobeID,openid,additional_info.projectedProductContext
```

SaaS API ホストは、プリプロダクションとプロダクションで異なります。 `TARGET_INSTANCE_REST_URL`と`TARGET_INSTANCE_GRAPHQL_URL`は、実稼動前または実稼動中のいずれの場合も、移行と同じCommerce API環境を使用する必要があります。 一方の階層を他の階層のCDMSまたはテナントと混在させないでください。

| 環境 | `TARGET_INSTANCE_*_URL`の一般的なホスト |
| --- | --- |
| プリプロダクションまたはサンドボックス | `https://na1-sandbox.api.commerce.adobe.com/{tenantId}` |
| 本番 | `https://na1.api.commerce.adobe.com/{tenantId}` |

>[!NOTE]
>
>これらのURLの`na1`は、ターゲットインスタンスがプロビジョニングされている地域を表します。 インスタンスが別の地域でプロビジョニングされている場合は、適切な地域識別子に置き換えます。

```shell-session
TARGET_TENANT_ID=<tenant_id>
TARGET_ORG_ID=<org_id>@AdobeOrg
ADOBE_IMS_URL=https://ims-na1.adobelogin.com
ADOBE_IMS_CLIENT_ID=<client_id>
ADOBE_IMS_CLIENT_SECRET=<client_secret>
ADOBE_IMS_META_SCOPES=AdobeID,openid,additional_info.projectedProductContext
TARGET_INSTANCE_REST_URL=https://na1-sandbox.api.commerce.adobe.com/{tenantId}
TARGET_INSTANCE_GRAPHQL_URL=https://na1-sandbox.api.commerce.adobe.com/{tenantId}/graphql
```

実稼動SaaS ホストの場合、`na1-sandbox`を`TARGET_INSTANCE_*`個のURLで`na1`に置き換えます。 前の表に示すように、その層に一致する`ADOBE_IMS_URL`を使用します。

### CDMS エンドポイントの設定

移行先の環境に一致するCDMS API ホストに移行ツールを指定します。 `.env`に`CDMS_HOST` （通常は`CDMS_PORT=443`）を設定します。 プリプロダクションまたはプロダクションのどちらか1つのホストを使用します。両方を使用しないでください。

| 環境 | 使用するタイミング | `CDMS_HOST` |
| --- | --- | --- |
| プリプロダクション | プリプロダクションまたはサンドボックススタイルの実行、非実稼動CDMS | `https://commerce-data-migration-service-preprod-external.adobe.io` |
| 本番 | 本番環境のライブ移行またはカットオーバー | `https://commerce-data-migration-service-prod-external.adobe.io` |

実行に一致するブロックを設定またはコメント解除します。

```shell-session
# Pre-production CDMS
CDMS_HOST=https://commerce-data-migration-service-preprod-external.adobe.io
CDMS_PORT=443

# Production CDMS (use for prod cutover only)
# CDMS_HOST=https://na1.api.commerce.adobe.com
# CDMS_PORT=443
```

### ストアコードの設定

`STORE_CODE`は、移行ツールでソースインスタンス REST API呼び出し、合成テスト顧客の作成、およびデータクリーンアップに使用されるストアビューコードです。 読み込み段階では、`x-store-code` ヘッダーとしても送信されます。

`STORE_CODE`のデフォルトは`.example.env`の`default`です。 これがソースインスタンスのデフォルトのストアビューコードと一致することを確認します。 確認するには、ソース [!UICONTROL Admin]で&#x200B;[!UICONTROL **Stores**] > [!UICONTROL **すべてのStores**]&#x200B;に移動し、使用するストアビューの&#x200B;[!UICONTROL **Code**]&#x200B;列を確認します。 表示されているコードが`default`でない場合は、`.env`の`STORE_CODE`を更新して一致させます。

## データベース接続ファイルの設定

>[!VIDEO](https://video.tv.adobe.com/v/3496152)

`.my.cnf` ファイルには、移行ツールの抽出側の[!DNL MySQL]接続設定が用意されています。 プロジェクト ルートの`.my.cnf.example`を`.my.cnf`にコピーして作成します。 セクション名は`.env`の`SOURCE_CONNECTION_NAME`と一致する必要があります。

オンプレミスまたはセルフホストのソースの場合：

```ini
[<connection-name>]
user=<db_user>
password='<db_password>'
host=<db_host>
port=3306
database=<db_name>
```

>[!NOTE]
>
>移行ツールを実行しているマシンは、ソースデータベースに直接ネットワークアクセスできる必要があります。 このツールは、オンプレミス接続を自動的に確立または検証しません。 移行コマンドを実行する前に、移行マシンからホスト、ポート、資格情報にアクセスできることを確認します。

[!DNL Adobe Commerce on Cloud] ソースの場合：

```ini
[<connection-name>]
id=<project_id>:<environment>
```

`id=` フィールドは、ソースが`MAGENTO_CLOUD_CLI_TOKEN`を使用したPaaSおよびトリガートンネル設定であることをツールに伝えます。 `project_id`と`environment`の値は、[!DNL Cloud Console]または`magento-cloud project:list`と`magento-cloud environment:list`のコマンドを通じて使用できます。

## ネットワークとインスタンスの準備

ストアの前のHTTP Basic Authは、APIとツールのトラフィックをブロックできます。 移行で使用されるソース URLに対して無効にするか、ツールのパスが許可されていることを確認して、RESTおよびGraphQL リクエストがストアに到達できるようにします。

### 抽出中にソースデータベースの安定性を維持する

ツールはソースデータベースからデータを抽出しますが、他のプロセスはそのデータベースに書き込む必要はありません。 同時に書き込むと、スナップショットに一貫性がなくなることがあります。

- ソース上のcron、および`bin/magento`またはその他のライターを実行するオペレーティングシステムのスケジューラーを抽出ウィンドウで停止するか、抽出中に実行できないことを確認します。
- ERP、OMS、PIM、カスタムジョブ、同じデータベースに書き込むサードパーティ APIなど、その他の統合を確認します。 抽出ウィンドウの書き込みを一時停止またはブロックして、抽出実行中にテーブルが変更されないようにします。
- これにより、メンテナンスモードとトンネルまたはデータベースへのアクセスが補完されます。 これらを組み合わせることで、ストアフロントとAPIのトラフィックを削減することができます。 Cronと統合は、明示的に制御する必要がある書き込みの個別のソースです。

### Target

移行前にターゲットカタログをクリアする必要がある場合は、カタログの重複や一括削除のタイムアウトを避けるために、一度に200など、[!UICONTROL Admin]の製品を小さなバッチで削除します。

## 移行のビルドと実行

書き込みアクセス権を持つ抽出されたプロジェクトディレクトリから作業します。

### SSH経由でセッションを維持する

SSH経由で接続する場合、ドロップされたネットワークはシェルを殺し、長い移行を中断する可能性があります。 GNU `screen` コマンドは、サーバー上でセッションを維持します。

```bash
screen -S migration          # new session named "migration"
# run ./bin/console commands here; when you want to disconnect without stopping work:
# press Ctrl+A, release, then press d   # detach
screen -ls                   # list sessions
screen -x migration          # reattach to "migration"
```

サーバーで使用可能な場合は、`tmux`を使用することもできます。

### Docker イメージのビルド

PHP、CLI、および依存関係を含む`bin/console`で使用される[!DNL Docker] イメージをビルドします。 これは最初の実行前、またはDockerfileまたはベースイメージの変更後に実行します。

```bash
./bin/console build
```

### バッキングサービスの開始

ローカル テスト データベースなどのツールの[!DNL Docker Compose] バッキング サービスを開始し、`.env`で有効にした場合は、オプションのローカル サービスを開始します。 正確なサービスは、設定によって異なります。 ビルドが成功した後、シェル、移行、または段階的なコマンドの前に、これを実行します。

```bash
./bin/console start
```

### CLI コンテナの初期化

インストール済みのプロジェクトに対して、必要に応じて[!DNL Composer]のインストールなどのセットアップを完了できるように、CLI コンテナを1回起動します。 これを1回実行してから、最初の移行を新しい環境で実行します。

```bash
./bin/console shell
exit
```

### 移行の実行

このツールは、2つの移行アプローチをサポートしています。 ユースケースに合ったものを選びましょう。

#### 単相移行

ソースインスタンスではメンテナンスモードは必要ありません。 単一のコマンドで完全な移行パイプラインを実行します。

```bash
./bin/console migration
```

このコマンドは、次の順序で、すべてのパイプラインステップをエンドツーエンドで自動的に実行します。

1. **設定チェック** – 環境変数とツール設定を検証します。
1. **環境初期化** — [!DNL Docker] サービスを開始し、（該当する場合）クラウドトンネルを開き、単体テストを実行します。
1. **統合テストとCDMS初期化** – 統合テストを実行し、CDMS API接続を初期化します。
1. **移行を作成** – 移行をCDMSに登録し、ターゲットスキーマ分析を待ちます。 移行IDは`.migration_id`に保存されます。
1. **機能テストとテストデータ生成** – 機能テストを実行し、統合性検証のためにソース上で合成テストデータを生成します（有効な場合）。
1. **データ抽出** — ソースインスタンスからデータを抽出します。
1. **ターゲットに読み込み** – 抽出されたデータをターゲット [!DNL Adobe Commerce as a Cloud Service] インスタンスに読み込みます。 ステージングビューはソース上でクリーンアップされ、ソーステストデータはロードと並行してRESTを通じて削除されます。
1. **データ統合検証** — チェックサム検証をトリガーし、ローカル API検証テストを実行します。 結果はログに記録され、失敗してもパイプラインは停止しません。
1. **Target**&#x200B;でデータのクリーンアップをテスト – ターゲットインスタンスから合成テストデータを削除します。
1. **処理結果** – 移行の概要を生成し、オプションでストレージからアーティファクトをダウンロードします。

このオプションは、エンドツーエンドのドライ実行、開発またはサンドボックス環境、または抽出中にソースがライブのままになる移行に典型的なメンテナンスウィンドウが必要ない場合に使用します。

>[!WARNING]
>
>凍結されたソースが必要な場合（たとえば、新しい注文やデータの変更が抽出中に発生しない実稼動の移行など）は、このオプションを使用しないでください。 代わりに段階的な移行を利用しましょう。 このコマンドを段階的メンテナンスワークフロー内の手順として使用しないでください。

#### メンテナンスモードを使用した多相移行

抽出時にデータの一貫性を確保するために、ソースインスタンスではメンテナンスモードが必要です。 移行は、順番に実行する必要がある個別のフェーズに分割されます。

>[!NOTE]
>
>2つの異なるCLIが含まれています。 `./bin/console` コマンドは、移行ツール プロジェクトのルートから実行されます。 `bin/magento maintenance:*` コマンドは、ソース [!DNL Adobe Commerce] アプリケーションサーバー、SSHを介してインストールルートまたは[!UICONTROL Admin]を介して実行されます。 このツールは、ユーザーに代わって[!DNL Magento] メンテナンスコマンドを発行しません。

| フェーズ | 誰が管理しているのか | Source州 |
| --- | --- | --- |
| 1. `migration:before-maintenance` | ツール | ライブ – まだメンテナンスを有効にしない |
| &#x200B;2. メンテナンスモードを有効にする | 手動 | フリーズへの移行 |
| 3. `migration:during-maintenance` | ツール | 凍結 – このフェーズではメンテナンスを無効にしないでください |
| &#x200B;4. メンテナンスモードを無効にする | 手動（条件付き） | ソースインスタンスをライブに戻す |
| &#x200B;5. `migration:cleanup` （オプション） | ツール | Live — must be out of maintenance |

**フェーズ 1 — メンテナンス前（ソースが公開されています）**

ソースインスタンスがライブでトラフィックを受け入れている間に実行します。 ソースへのRESTおよびGraphQL アクセスは、完全に使用可能である必要があります。 このフェーズが完了する前に、メンテナンスモードを有効にしないでください。

サーバーのルートに戻り、以下を実行します。

```bash
./bin/console migration:before-maintenance
```

1. **設定チェック** – 環境変数とツール設定を検証します。
1. **環境初期化** — [!DNL Docker] サービスを開始し、PaaS クラウドトンネルを開き（該当する場合）、単体テストを実行します。
1. **統合テストとCDMS初期化** – 統合テストを実行し、CDMS API接続を初期化します。
1. **移行を作成** – 移行をCDMSに登録し、ターゲットスキーマ分析を待ちます。 移行IDは`.migration_id`に保存されます。
1. **機能テスト** — ライブソースに対して機能テストを実行します。
1. **テストデータ生成** – 整合性の検証のために、ソース上で合成テストの顧客と注文を作成します（有効な場合）。

**フェーズ 2 — メンテナンスモードを有効にする（手動）**

ソースでメンテナンスモードを有効にし、スケジュールされたジョブ、サードパーティ統合、注文処理、メディアアセットの同期など、データベースに書き込むか影響を与えるすべてのアクティビティを一時停止します。

ソース Commerce サーバー（インストール ルート）で、次を実行します。

```bash
bin/magento maintenance:enable
```

**フェーズ 3 — メンテナンス中（ソースがフリーズしている）**

ソースインスタンスでメンテナンスモードで実行します。 ソースは、このフェーズの全期間にわたってフリーズしたままにする必要があります。 **フェーズ 3**&#x200B;が正常に完了するまで、メンテナンスモードを無効にしないでください。

```bash
./bin/console migration:during-maintenance
```

1. **Cloud tunnel setup** — [!DNL Adobe Commerce on Cloud] ソースインスタンスの場合、クラウドトンネルを再開し、データベース接続を確認します。 オンプレミスインスタンスの場合、自動的にスキップされます。
1. **データ抽出** – フリーズされたソースインスタンスからデータを抽出します。
1. **ステージング ビューのクリーンアップ** – 直接データベース接続（メンテナンスモードで安全）を使用して、ソースからステージング ビューを削除します。
1. **ターゲットに読み込み** – 抽出されたデータをターゲット [!DNL Adobe Commerce as a Cloud Service] インスタンスに読み込み、完了を待ちます。
1. **データ統合検証** — CDMS チェックサム検証をトリガーし、ローカル API検証テストを実行します。 結果はログに記録され、失敗してもパイプラインは停止しません。
1. **Target**&#x200B;でデータのクリーンアップをテスト – ターゲットインスタンスから合成テストデータを削除します。
1. **処理結果** – 移行の概要を生成し、オプションでストレージからアーティファクトをダウンロードします。

**フェーズ 4 — メンテナンスモードを無効にする（手動、条件付き）**

このフェーズでは、メンテナンスモードが無効になり、ソースインスタンスへのトラフィックが再度有効になります。 クリーンアップはRESTを介してソースと通信し、メンテナンスモードがアクティブな場合は`HTTP 503`で失敗するため、クリーンアップフェーズを実行する前にこの手順が必要です。

ソース Commerce サーバーで、次を実行します。

```bash
bin/magento maintenance:disable
```

**フェーズ 5 — クリーンアップ （オプション、ソースがライブである必要があります）**

**フェーズ 1**&#x200B;で作成された合成テストの顧客と注文を、RESTを介してソースインスタンスから削除します。 このフェーズは、メンテナンスモードが無効になっている場合にのみ実行できます。

>[!NOTE]
>
>`SKIP_TEST_DATA_CREATION=true`が`.env`で設定されている場合、テストデータが作成されていないため、このフェーズをスキップします。

サーバーのルートに戻り、以下を実行します。

```bash
./bin/console migration:cleanup
```

1. **データベース接続の設定** — [!DNL Adobe Commerce on Cloud] ソースインスタンスの場合、クラウドトンネルが再開されます。 オンプレミスインスタンスの場合は、データベースへの直接接続を確立および検証します。
1. **Source REST クリーンアップ** – 合成テストの顧客と注文をREST APIを介してソースから削除します。

## 移行の再開または再実行

移行ツールは、プロジェクトルートの`.migration_id` ファイルを使用して進行状況を追跡します。 このファイルは、新しい移行が開始され、現在の移行識別子が記録されるときに自動的に作成されます。

### 失敗後に再開

移行の実行が失敗したり、中断されたりした場合は、同じコマンドを再実行して、最初から再開するのではなく、最後に成功したステップ（抽出、読み込み、検証）から再開します。 既に完了した手順は自動的にスキップされます。

>[!IMPORTANT]
>
>`migration:during-maintenance` フェーズを再開する場合、ソースはメンテナンス モードのままである必要があります。 ソースがメンテナンスから取り除かれたり、実行間にデータが変更されたりした場合、移行を再開すると、一貫性のない結果が生じる可能性があります。

### 新しい移行を開始

前回の実行を破棄して完全に新しい移行を開始するには、次の移行を開始する前に`.migration_id` ファイルを削除します。

```bash
rm .migration_id
```

`.migration_id`が存在し、以前の移行が既に完了している場合、移行が既に完了したことを示すメッセージが表示され、ファイルを削除するようにアドバイスされます。

## ログの確認とデバッグ

すべての移行ログは、プロジェクトルートの`logs/` ディレクトリに書き込まれ、タイムスタンプ付きのサブディレクトリに整理されます。

```text
logs/
  2026-03-23_14-30-00/     ← one directory per run
    index.log              ← main pipeline log (start here)
    ...
```

- `index.log`はメイン パイプライン オーケストレーション ログです。 ステップが失敗した場合は、ゼロ以外のコードで終了したスクリプトとその理由が表示されます。
- `09b_run_load.log`や`11_verify_data_integrity_local.log`などのステップごとのログには、各フェーズの詳細な出力が含まれます。
