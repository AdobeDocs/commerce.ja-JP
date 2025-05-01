---
title: ストアフロントの設定
description: ストアフロントの設定方法  [!DNL Adobe Commerce Optimizer]  説明します。
role: Developer
source-git-commit: 425c801a852de566120504563e256b0351df588e
workflow-type: tm+mt
source-wordcount: '2287'
ht-degree: 0%

---

# ストアフロントの設定

>[!NOTE]
>
>このドキュメントでは、製品の早期アクセス開発について説明しており、一般提供を目的とした機能のすべてを反映しているわけではありません。

このチュートリアルでは、[Edge Delivery Servicesを利用したAdobe Commerce Storefront を設定および使用して ](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/)[!DNL Adobe Commerce Optimizer] インスタンスのデータを利用して、パフォーマンス、拡張性、安全性の高いCommerce Storefront を作成する方法について説明します。


## 前提条件

* リポジトリを作成できる GitHub アカウント（github.com）があり、ローカル開発用に設定されていることを確認します。

* Adobe Commerce ストアフロントドキュメントの [ 概要 ](https://experienceleague.adobe.com/developer/commerce/storefront/get-started) を確認して、Adobe Edge 配信サービスのストアフロントを作成するのに関連する基本的なワークフローと語彙について理解します。
* 開発環境の設定


### 開発環境の設定

開発環境を設定するには、必要なバージョンの Node.js とSidekick ブラウザー拡張機能をインストールします。

#### Node.js のインストール

Edge Delivery Services プロジェクトで [!DNL Adobe Commerce Optimizer] ストアフロントをローカルに開発およびテストするには、Node.js バージョン 22.13.1 LTS が必要です。

必要に応じて、次の手順を実行して Node Version Manager （NVM）と必要な Node.js のバージョンをインストールします。

1. ノードバージョンマネージャー（NVM）をインストールします。

   ```bash
   curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.1/install.sh | bash
   ```

1. Node.js と NPM をインストールします。 詳しくは、[Node.js](https://nodejs.org/en/) を参照してください。

   ```bash
   nvm install 22
   ```

   ```bash
   npm install -g npm
   ```

1. インストールを確認します。

   ```bash
   npm -v
   ```

>[!TIP]
>
>この設定は、[!DNL Adobe Commerce Optimizer] およびAdobe Commerce Edge Delivery サービスのストアフロントを使用して開発するためのものです。 [!DNL Adobe Commerce Optimizer] ソリューションを拡張およびカスタマイズするためのその他のリソースは、[Adobe CommerceのApp Builder](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/adobe-developer-app-builder/introduction-to-app-builder) および [Adobe Developer App Builderの API メッシュ ](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/adobe-developer-app-builder/api-mesh/getting-started-api-mesh) を通じて利用できます。 アクセスおよび使用方法について詳しくは、Adobe アカウント担当者にお問い合わせください。

#### Sidekickのインストール

ストアフロントコンテンツを編集、プレビュー、公開するためのSidekick ブラウザー拡張機能をインストールします。 [Sidekickのインストール手順 ](https://www.aem.live/docs/sidekick#installation) を参照してください。


## ストアフロントの作成

[!DNL Adobe Commerce Optimizer] プロジェクト用に作成するストアフロントは、カスタマイズされたバージョンのAdobe Commerce on Edge Delivery Services ストアフロントボイラープレートを使用して構築されます。 ボイラープレートは、ストアフロントを構築するための出発点となるファイルとフォルダーのセットです。

このストアフロントのセットアッププロセスは、特に [!DNL Adobe Commerce Optimizer] のプロジェクト用にカスタマイズされています。 フローが、Edge Delivery Services ストアフロントの標準 [Adobe Commerce](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/) 設定のフローと異なります。

>[!NOTE]
>
>このチュートリアルでは、macOS、Chrome、Visual Studio Code を開発環境として使用します。 画面のキャプチャと指示には、その設定が反映されています。 別のオペレーティングシステム、ブラウザーおよびコードエディターを使用できますが、表示される UI と実行する必要がある手順は、それに応じて異なります。

### ワークフローの概要

Adobe Commerce Optimizerで使用するストアフロントを設定するには、次の手順に従います。

1. **[コンテンツフォルダーの作成](#step-1-create-a-content-folder)** - Google Drive または Sharepoint で共有コンテンツフォルダーを作成します。 このフォルダーには、ストアフロントのサンプルコンテンツとアセットが含まれています。

1. **[コードリポジトリを作成](#step-1-create-a-code-repository)** - Adobe Commerce + Edge Delivery Services ボイラープレートテンプレートから GitHub リポジトリーを作成します。 ソースリポジトリからすべてのブランチを含めます。
1. **[ストアフロントボイラープレートの更新](#step-2-update-the-storefront-boilerplate)** - リポジトリーの `aco` ブランチのカスタムボイラープレートテンプレートを更新して、コンテンツフォルダーをストアフロントに接続し、Adobe Commerce Optimizer デモインスタンスからストアフロントにデータを配信するストアフロント設定を確認します。
1. **[更新したストアフロントのボイラープレートコードをアップロードします](#step-3-upload-the-updated-boilerplate-code)**-`main` 分岐のコードを、`aco` 分岐の更新したコードで上書きします。
1. **[CodeSync アプリを追加](#step-4-add-the-aem-code-sync-app)** します。リポジトリをEdge Delivery サービスに接続します。 ソースコードのカスタマイズが完了し、コードを `main` ブランチにプッシュする準備が整うまでは、コード同期アプリを接続しないでください。
1. **[コンテンツのプレビューと公開](#step-5-preview-and-publish-your-content)** - Sidekick拡張機能を使用して、コンテンツフォルダーからストアフロントにサイトコンテンツをプレビューして公開します。
1. **[サイトのプレビューとサンプルデータの表示](#step-6-preview-your-site-and-view-sample-data)** ストアフロントサイトに接続して、[!DNL Adobe Commerce Optimizer] デモインスタンスのサンプルコンテンツとサンプルデータを表示します。
1. **[ローカル環境でストアフロントを開発します](#step-7-develop-the-storefront-in-your-local-environmentdevelop-the-storefront-in-your-local-environment)** – 必要な依存関係をインストールします。 ローカル開発サーバーを起動し、Adobeでプロビジョニングされた [!DNL Adobe Commerce Optimizer] インスタンスに接続するようにストアフロント設定を更新します。
1. **[サイトコンテンツの管理](#step-8-manage-site-content)** - サイトコンテンツの更新と管理の詳細を説明します。

### 手順 1：コンテンツフォルダーの作成

Adobe Commerce Storefront のドキュメントの手順に従って、Google Drive または SharePoint に共有コンテンツフォルダーを追加し、サンプルコンテンツを追加します。 サンプルコンテンツには、画像、テキスト、およびサイトを構成するその他のアセットが含まれます。

* [Google ドライブまたは Sharepoint フォルダーの作成と共有 ](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/#create-and-share-folder)
* [ サンプルコンテンツを読み込む ](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/#add-sample-content) フォルダーに。

### 手順 2：コードリポジトリの作成

Edge Delivery ServicesとAdobe Commerceのボイラープレートテンプレートを使用して、GitHub にコードリポジトリーを作成します。 このテンプレートは、ストアフロントのボイラープレートコードを提供します。

1. GitHub アカウントにログインします。

1. [aem-boilerplate-commerce](https://github.com/hlxsites/aem-boilerplate-commerce) GitHub リポジトリに移動します。

1. **このテンプレートを使用** を選択してから、ドロップダウンメニューから **新しいリポジトリを作成** を選択します。

   ![[!DNL Create github repo from storefront boilerplate template]](./assets/storefront-create-github-repo.png){width="700" zoomable="yes"}

   これにより、リポジトリ設定ページが開きます。

   ![[!DNL Configure github repo to pull all branches from boilerplate repo]](./assets/storefront-configure-github-repo.png){width="700" zoomable="yes"}

1. 設定フォームに次の詳細を入力します。

   * **リポジトリテンプレート** - `hlxsites/aem-boilerplate-commerce` （デフォルト）。
   * **すべてのブランチを含める** – すべてのブランチを含める場合は、このオプションを選択します。
   * **所有者** – 組織またはアカウント（必須）。
   * **リポジトリ名** – 新しいリポジトリの一意の名前（必須）。
   * **説明** - リポジトリの簡単な説明（オプション）。
   * **パブリックまたはプライベート** - Adobeでは、パブリック（デフォルト）をお勧めします。

1. 「**リポジトリを作成**」を選択します。

   1 ～ 2 分後、新しいリポジトリが開きます。

   新しいリポジトリに表示されるプル要求通知を無視します。

### 手順 3：ストアフロントボイラープレートの更新

このセクションでは、次のタスクを実行します。

* [!DNL Adobe Commerce Optimizer] のプロジェクトのカスタムボイラープレートテンプレートを更新するには、リポジトリの `aco` ブランチをチェックアウトします
* コンテンツフォルダーを指すように `fstab.yaml` ファイルを更新して、コンテンツフォルダーをストアフロントに接続します。
* ストアフロント設定ファイル、`config.json` を確認します。
* Sidekick拡張機能を設定して、共有コンテンツフォルダーのコンテンツを編集、プレビュー、公開します。

これらの手順を完了するには、次の情報が必要です。

* **手順 2 の GitHub リポジトリ URL**— `github.com/{ORG}/{SITE}`

   * `{ORG}` は、リポジトリの組織名またはユーザー名です。

   * `{SITE}` はリポジトリ名です。

* **手順 1 のコンテンツフォルダー URL** - `https://drive.google.com/drive/folders/{YOUR_FOLDER_ID}`

  `{YOUR_FOLDER_ID}` は、サンプルコンテンツデータを使用して作成したフォルダーの ID です。

#### コンテンツフォルダーに接続するようにボイラープレートコードを更新します。

1. ローカルマシンにリポジトリのクローンを作成します。

   ```bash
   git clone https://github.com/{ORG}/{SITE}.git
   ```

   リポジトリのクローン作成時にエラーが発生した場合は、GitHub ドキュメントの [ クローニングエラーのトラブルシューティング ](https://docs.github.com/en/repositories/creating-and-managing-repositories/troubleshooting-cloning-errors) を参照してください。

1. ターミナルまたは IDE でリポジトリを開きます。

1. `aco` ブランチを確認します。

   ```bash
   git checkout aco
   ```

1. `default-fstab.yaml` ファイルを `fstab.yaml` にコピーして、設定ファイルを作成します。

   ```bash
   cp default-fstab.yaml fstab.yaml
   ```

1. ストアフロント設定ファイルを更新して、コンテンツの URL を指定します。

   1. [fstab.yaml](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/#vocabulary) 設定ファイルを開きます。

      ```json
      mountpoints:
       /: {YOUR_MOUNTPOINT_URL}
      
      folders:
       /products/: /products/default
      ```

   1. `{YOUR_MOUNTPOINT_URL}` をコンテンツ管理システムの URL に置き換えます。

      例えば、Google Drive を使用している場合、更新されたコードは次のようになります。

      ```json
       mountpoints:
        /: https://drive.google.com/drive/folders/{YOUR_FOLDER_ID}
      ```

   1. ファイルを保存します。

#### データ接続設定を確認する

データ接続により、Adobe Commerce Optimizerとストアフロントの間のやり取りが確立され、カタログデータがシームレスにストアフロントに送られます。 このプロセスでは、検索コンポーネント、製品リスト、ア [!DNL Adobe Commerce Optimizer] ットに必要な製品詳細ページなど、様々なストアフロントインターフェイスが設定されます。

ストアフロントの初期設定では、AdobeにはAdobe Commerce Optimizer デモインスタンスにサンプルデータで接続するデフォルトの設定ファイルが用意されています。

```json
{
  "public": {
    "default": {
      "commerce-core-endpoint": "https://www.aemshop.net/graphql",
      "commerce-endpoint": "https://na1-sandbox.api.commerce.adobe.com/Fwus6kdpvYCmeEdcCX7PZg/graphql",
      "headers": {
        "cs": {
          "ac-channel-id": "9ced53d7-35a6-40c5-830e-8288c00985ad",
          "ac-environment-id": "Fwus6kdpvYCmeEdcCX7PZg",
          "ac-price-book-id": "west_coast_inc",
          "ac-scope-locale": "en-US"
        }
      },
      "analytics": {
        "base-currency-code": "USD",
        "environment": "Production",
        "store-id": 1,
        "store-name": "ACO Demo",
        "store-url": "https://www.aemshop.net",
        "store-view-id": 1,
        "store-view-name": "Default Store View",
        "website-id": 1,
        "website-name": "Main Website"
      }
    }
  }
}
```

データ接続がどのように確立されるかを理解するには、リポジトリのストアフロント設定ファイルを確認します。

1. コードリポジトリで、ルートディレクトリに移動します。

1. `config.json` ファイルを開きます。

   このファイルで、次のキー値は接続先のAdobe Commerce Optimizer インスタンスを指定し、ストアフロントに送られるデータを判断します。

   * 接続先 `commerce-endpoint`Adobe Commerce Optimizer インスタンスを定義します。
   * ストアフロントに送られるデータを決定で `headers` ます。
      * `ac-channel-id` は `west_coast_inc` に設定されています
      * `ac-price-book-id` は `west_coast_inc` に設定されています
      * `ac-scope-locale` は `en-US` に設定されています
      * `ac-price-book-id` は `west_coast_inc` に設定されています

   これらの値は、チャネル ID、ロケール、価格台帳 ID を設定して、カタログデータを特定の販売チャネルに送信し、指定されたロケールと価格台帳の値に基づいてそのデータをフィルタリングします。 その後、Adobe Commerce Optimizer インスタンスを変更し、ヘッダーを更新して、ストアフロントに配信するデータを定義する方法について説明します。

1. ファイルを確認したら、ファイルを閉じてチュートリアルを続行します。


#### Sidekick拡張機能の設定

Sidekick拡張機能のプロジェクト設定を追加します。 Sidekickを使用すると、ストアフロントのコンテンツを編集、プレビュー、公開できます。 この設定により、Sidekickを使用して、共有コンテンツフォルダー内のコンテンツと、ステージング環境および実稼動環境に公開されたサイトページ内のコンテンツを管理できるようになります。

>[!NOTE]
>
>ブラウザーに [Sidekick拡張機能 ](https://www.aem.live/docs/sidekick#installation) がインストールされていることを確認します。

1. `tools/sidekick/config.json` ファイルを開きます。

   +++Sidekick設定ファイル

   ```json
   {
     "project": "Boilerplate",
     "plugins": [
       {
         "id": "cif",
         "title": "Commerce",
         "environments": [
           "edit"
         ],
         "url": "https://main--{SITE}--{ORG}.aem.live/tools/picker/dist/index.html",
         "isPalette": true,
         "paletteRect": "top: 54px; left: 5px; bottom: 5px; width: 300px; height: calc(100% - 59px); border-radius: var(--hlx-sk-button-border-radius); overflow: hidden; resize: horizontal;"
       },
       {
         "id": "personalisation",
         "title": "Personalisation",
         "environments": [
           "edit"
         ],
         "url": "https://main--{SITE}--{ORG}.aem.live/tools/segments/dist/index.html",
         "isPalette": true,
         "paletteRect": "top: 54px; left: 5px; bottom: 5px; width: 300px; height: calc(100% - 59px); border-radius: var(--hlx-sk-button-border-radius); overflow: hidden; resize: horizontal;"
       }
     ]
   }
   ```

   詳しくは、[Sidekick ライブラリのドキュメント ](https://www.aem.live/docs/sidekick-library) 参照してください。

+++

1. `url` キーの値を GitHub リポジトリの値で更新します。

   * `{ORG}` は、コードリポジトリの名前またはユーザー名です。

   * `{SITE}` はリポジトリ名です。

1. ファイルを保存します。

### 手順 4：更新したボイラープレートコードのアップロード

カスタマイズしたストアフロントのボイラープレートコードを使用するには、更新内容を反映して `main` ブランチのコードを上書きします。

1. エディターまたは IDE から、更新したファイルをコミットして保存します。

   ```bash
   git add .
   ```

   ```bash
   git commit -m "Update storefront boilerplate for Adobe Commerce Optimizer"
   ```

1. `aco` 分岐の変更をプッシュし、`main` 分岐を上書きします。

   ```bash
   git push origin aco:main -f
   ```

### 手順 5:AEM コード同期アプリの追加

AEM コード同期 GitHub アプリをリポジトリに追加して、リポジトリをEdge Delivery サービスに接続します。

>[!IMPORTANT]
>
>更新されたボイラープレートコードを GitHub リポジトリの main ブランチにアップロードするまで、コード同期アプリを接続しないでください。

1. 「[AEM コード同期アプリ ](https://github.com/apps/aem-code-sync)」設定ページを開きます。

1. **設定** を選択し、作成したリポジトリを含む **組織** または **アカウント** を使用して認証します。

1. フォームから「**リポジトリのみを選択**」を選択し、作成したリポジトリを選択します。

1. 「**インストール**」を選択して、AEM コード同期アプリをリポジトリに追加します。

   アプリケーションが正常にインストールされたことを示すメッセージが表示されます。

### 手順 6：コンテンツのプレビューと公開

ストアフロントにコンテンツを追加するには、Sidekick拡張機能を使用してコンテンツをプレビューし、公開する必要があります。

1. コンテンツフォルダーをGoogle ドライブまたは Sharepoint で開きます。

1. ブラウザーツールバーのSidekick アイコンをクリックして、Sidekickをオンにします。

   ![[!DNL Turn on Sidekick from browser toolbar]](./assets/storefront-enable-sidekick-toolbar.png){width="700" zoomable="yes"}

1. Sidekick ツールバーを使用して、コンテンツをプレビューおよび公開します。

   ![[ プレビューして公開するファイルを選択 ]](./assets/storefront-content-preview-publish.png){width="700" zoomable="yes"}

1. 各フォルダーのファイルを別々に選択し、Sidekick ツールバーを使用してすべてのファイルをプレビューおよび公開します。

   * **プレビュー** - ステージング環境にコンテンツをアップロードします。 ストアフロントのステージング URL は `.aem.page` で終わります。

   * **公開** – 実稼動環境にコンテンツをアップロードします。 実稼動 URL の末尾は `aem.live` です。

詳しくは、Adobe Experience Manager [Sidekick](https://www.aem.live/docs/sidekick) ドキュメントを参照してください。

### 手順 7：サイトのプレビュー

サイトをプレビューして、サンプルコンテンツとAdobe Commerce Optimizer デモデータの両方が正しく表示されていることを確認します。

* **サンプルコンテンツ** は、共有コンテンツフォルダーから提供されます。 Sidekickを使用して公開したページレイアウト、バナーおよびその他のコンテンツが含まれます。
* **サンプルデータ** は、[!DNL Adobe Commerce Optimizer] デモインスタンスから提供されます。 データには、製品属性、画像、製品の説明および価格が、ストアフロント設定ファイル `config.json` で指定された値に基づいて入力された製品データが含まれています。


#### サイトに接続して、サンプルコンテンツとサンプルデータを表示する

1. に移動して、サイトに接続し `https://main--{SITE}--{ORG}.aem.live` す。

   `{ORG}` および `{SITE}` を、ボイラープレートリポジトリの組織と名前に置き換えます。

   ![[!DNL ACO storefront site with boilerplate]](./assets/aco-storefront-site-boilerplate.png){width="700" zoomable="yes"}

   ページが 404 を返す場合は、Sidekick拡張機能を使用してコンテンツを公開していることを確認してください。 また、更新した `fstab.yaml` ファイルがコンテンツフォルダーの URL を使用していることを再確認します。

1. Commerce Optimizer デモインスタンスからのサンプルカタログデータを表示します。

   1. `tires` を検索して、使用可能なタイヤ製品のドロップダウンリストを表示します。

   ![[!DNL Discover Adobe Commerce Optimizer products]](./assets/storefront-site-with-aco-data.png){width="700" zoomable="yes"}

   検索コンポーネントは、ストアフロントボイラープレートコードの一部です。 検索結果データは、ストアフロントの設定に基づいて入力されます。

   1. **Enter** キーを押して、製品リストページを表示します。

      ![[!DNL View product details page]](./assets/storefront-with-aco-pdp-page.png){width="675" zoomable="yes"}

   1. ページでタイヤ製品を選択して、製品の詳細ページを表示します。

      ストアフロントを探索する場合は、一部のコンポーネントが機能しないことに注意してください。 例えば、買い物かごに製品を追加するとエラーが返され、アカウント管理コンポーネントが機能しません。 これは、これらのコンポーネントがCommerce バックエンドからデータを受け取るように設定されていないためです。 Adobe Commerce Optimizer インスタンスからのデータは、検索コンポーネントページ、商品リストページおよび商品詳細ページにのみ入力されます。

   1. ストアフロントを探索した後、チュートリアルを続行します。


### 手順 8：ローカル環境でのストアフロントの開発

この節では、Adobeがプロビジョニングした [!DNL Adobe Commerce Optimizer] インスタンスにストアフロントを接続することで、ローカル開発環境でストアフロント設定を試します。

接続するには、オンボーディングメールで提供されたマーチャンダイジングサービス用のGraphQL エンドポイントが必要です。

```text
https://na1-sandbox.api.commerce.adobe.com/{tenantId}/graphql
```

#### ローカル開発を開始

1. IDE で GitHub コードリポジトリの main ブランチをチェックアウトします。

   ```bash
   git checkout main
   ```

1. 必要な依存関係をインストールします。

   ```bash
   npm install
   ```

1. ローカル開発サーバーを起動します。

   ```bash
   npm start
   ```

   ボイラープレートのストアフロントの最初のページが、ブラウザーの `http://localhost:3000` に表示されるはずです。

![[!DNL Configure github repo to pull all branches from boilerplate repo]](./assets/aco-storefront-local-dev-env.png){width="700" zoomable="yes"}


#### ストアフロント設定の更新

ストアフロント設定ファイルを更新し、ローカル開発環境で変更内容をプレビューします。


1. IDE でストアフロント設定を更新して、Adobeによってプロビジョニングされた [!DNL Adobe Commerce Optimizer] インスタンスに接続します。

   1. `config.json` ファイルを開きます。

   1. [!DNL Adobe Commerce Optimizer] インスタンスのエンドポイントを使用して、次の値を更新します。

      * **`commerce-endpoint`** – 既存の値をエンドポイント URL に置き換えます。

        ```json
        "commerce-endpoint": "https://na1-sandbox.api.commerce.adobe.com/{tenantId}/graphql"
        ```

      * **`ac-environment-id`** – 既存の値を、エンドポイント URL のテナント ID に置き換えます。

        ```json
        "ac-environment-id": "{tenantId}"
        ```

   1. ファイルを保存します。

      ローカルプレビューが正しく動作している場合、更新はローカルのストアフロントに適用されます。

1. 設定変更の結果をサイトで確認します。

   1. ブラウザーで `http://localhost:3000` に移動し、ページを更新します。

   1. ストアフロントのヘッダーで、虫眼鏡をクリックして `tires` を検索します。

      ![ タイヤの検索 ](./assets/storefront-header-empty-search-list.png){width="675" zoomable="yes"}

      ドロップダウンリストには値が入力されません。

   1. **Enter** キーを押して、製品リストページを表示します。

      ![ 無効なヘッダー値を含む空の検索結果 ](./assets/storefront-configuration-with-incorrect-headers.png){width="675" zoomable="yes"}

      ストアフロント設定ファイルのヘッダーは、デモインスタンスに基づくヘッダー値を使用しているので、検索で結果が返されません。 設定が、プロビジョニングされた [!DNL Adobe Commerce Optimizer] インスタンスを指すようになったので、これらの値は無効です。

### 次の手順

[!DNL Adobe Commerce Optimizer] インスタンスの値を使用してストアフロント設定を更新してストアフロントにコンテンツを表示する方法については ](./use-case/admin-use-case.md) ストアフロントおよびカタログ管理者のエンドツーエンドのユースケース [ を参照してください。

>[!MORELIKETHIS]
>
>* サイトコンテンツの更新と、Adobe Commerceのフロントエンドコンポーネントやバックエンドデータとの統合について詳しくは、[Adobe Experience Manager Commerce ストアフロントのドキュメント ](https://experienceleague.adobe.com/developer/commerce/storefront/) を参照してください。[!DNL Adobe Commerce Optimizer]
></br></br>
>* Adobe Commerce バックエンドで [!DNL Adobe Commerce Optimizer] を使用する予定がある場合は、[Adobe Commerce Storefront のドキュメント ](https://experienceleague.adobe.com/developer/commerce/storefront/) を参照して、コンテンツを更新する方法、アカウント管理、チェックアウトなどの機能のためにストアフロントコンポーネントを設定する方法を確認してください。
