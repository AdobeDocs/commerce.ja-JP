---
title: ストアフロントの設定
description: ストアフロントの設定方法  [!DNL Adobe Commerce Optimizer]  説明します。
role: Developer
badgeSaas: label="SaaS のみ" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud ServiceおよびAdobe Commerce Optimizer プロジェクトにのみ適用されます（Adobeで管理される SaaS インフラストラクチャ）。"
source-git-commit: 3131cc27a25d1bf958071b973f1d4bf1a68be152
workflow-type: tm+mt
source-wordcount: '923'
ht-degree: 0%

---

# ストアフロントの設定

このチュートリアルでは、[Edge Delivery Servicesを利用したAdobe Commerce Storefront を設定および使用して ](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/)[!DNL Adobe Commerce Optimizer] インスタンスのデータを利用して、パフォーマンス、拡張性、安全性の高いCommerce Storefront を作成する方法について説明します。


## 前提条件

- リポジトリを作成できる GitHub アカウント（github.com）があり、ローカル開発用に設定されていることを確認します。

- Adobe Commerce ストアフロントのドキュメントの [ 概要 ](https://experienceleague.adobe.com/developer/commerce/storefront/get-started) を確認して、Adobe Edge 配信サービスでCommerce ストアフロントを開発するための概念とワークフローについて説明します。
- 開発環境の設定


### 開発環境の設定

Edge Delivery Servicesで [!DNL Adobe Commerce Optimizer] ストアフロントを開発およびテストするために必要な Node.js とSidekick ブラウザー拡張機能をインストールします。

#### Node.js のインストール

Node Version Manager （NVM）と必要な Node.js バージョン（22.13.1 LTS）をインストールします。

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
>[!DNL Adobe Commerce Optimizer] ソリューションを拡張およびカスタマイズするためのその他のリソースは、[Adobe CommerceのApp Builder](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/adobe-developer-app-builder/introduction-to-app-builder) および [Adobe Developer App Builderの API メッシュ ](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/adobe-developer-app-builder/api-mesh/getting-started-api-mesh) を通じて利用できます。 アクセスおよび使用方法について詳しくは、Adobe アカウント担当者にお問い合わせください。

#### Sidekickのインストール

Sidekick ブラウザー拡張機能をインストールして、コンテンツを編集、プレビューおよびストアフロントに公開します。 [Sidekickのインストール手順 ](https://www.aem.live/docs/sidekick#installation) を参照してください。

## ストアフロントの作成

[!DNL Adobe Commerce Optimizer] プロジェクト用に作成するストアフロントでは、Edge Delivery Services ストアフロントボイラープレート上のAdobe Commerceのカスタマイズバージョンを使用します。 ボイラープレートは、ストアフロント開発の出発点となるファイルとフォルダーのセットです。 この設定プロセスは、Edge Delivery Services ストアフロント上の [Adobe Commerce](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/) の標準の設定プロセスとは異なります。

>[!NOTE]
>
>このチュートリアルでは、macOS、Chrome、Visual Studio Code を開発環境として使用します。 画面のキャプチャと指示には、その設定が反映されています。 別のオペレーティングシステム、ブラウザー、コードエディターを使用することもできますが、表示される UI と実行する手順は、それに応じて異なります。

### ワークフローの概要

[!DNL Adobe Commerce Optimizer] で使用するストアフロントを設定するには、次の手順に従います。

1. **[コードリポジトリを作成](#step-1-create-site-code-repository)** - Adobe Commerce + Edge Delivery Services ボイラープレートテンプレートから GitHub リポジトリーを作成します。 ソースリポジトリからすべてのブランチを含めます。
1. **[ストアフロントボイラープレートを更新](#step-2-update-the-storefront-boilerplate)** - `aco` ブランチのカスタムボイラープレートテンプレートを更新して、コンテンツフォルダーをストアフロントに接続します。
1. **[変更をデプロイ](#step-3-deploy-changes)** - `aco` ブランチからの更新されたコードで `main` ブランチのコードを上書きします。
1. **[CodeSync アプリを追加](#step-5-add-the-aem-code-sync-app)** します。リポジトリをEdge Delivery サービスに接続します。 ソースコードのカスタマイズが完了し、コードを `main` ブランチにプッシュするまで、コード同期アプリを接続しないでください。
1. **[コンテンツを追加](#step-6-add-content)** - デモコンテンツのクローンツールを使用して、`https://da.live` でホストされているドキュメント作成者環境でストアフロントコンテンツを作成および初期化します。
1. **[デモサイトをプレビュー](#step-7-preview-demo-site)** - ストアフロントサイトに接続して、[!DNL Adobe Commerce Optimizer] デモインスタンスのサンプルコンテンツとデータを表示します。
1. **[ローカル環境で開発します](#step-8-develop-in-your-local-environment)** – 必要な依存関係をインストールします。 ローカル開発サーバーを起動し、Adobeでプロビジョニングされた [!DNL Adobe Commerce Optimizer] インスタンスに接続するようにストアフロント設定を更新します。
1. **[次の手順](#next-steps)** - ストアフロントでのコンテンツとデータの管理および表示に関する詳細情報。


### 手順 1：サイトコードリポジトリを作成する

Edge Delivery Services + Adobe Commerce Boilerplate テンプレートを使用して、ストアフロントのサイトボイラープレートコード用の GitHub リポジトリを作成します。

1. GitHub アカウントにログインします。

1. [aem-boilerplate-commerce](https://github.com/hlxsites/aem-boilerplate-commerce) GitHub リポジトリに移動します。

1. **このテンプレートを使用** を選択してから、ドロップダウンメニューから **新しいリポジトリを作成** を選択します。

   ![[!DNL Create github repo from storefront boilerplate template]](./assets/storefront-create-github-repo.png){width="700" zoomable="yes"}

   リポジトリ設定ページが表示されます。

   ![[!DNL Configure github repo to pull all branches from boilerplate repo]](./assets/storefront-configure-github-repo.png){width="700" zoomable="yes"}

1. 設定フォームに次の詳細を入力します。

   - **リポジトリテンプレート** - `hlxsites/aem-boilerplate-commerce` （デフォルト）。
   - **すべてのブランチを含める** – すべてのブランチを含める場合は、このオプションを選択します。
   - **所有者** – 組織またはアカウント（必須）。
   - **リポジトリ名** – 新しいリポジトリの一意の名前（必須）。
   - **説明** - リポジトリの簡単な説明（オプション）。
   - **パブリックまたはプライベート** - Adobeでは、パブリック（デフォルト）をお勧めします。

1. 「**リポジトリを作成**」を選択します。

   数分後、新しいリポジトリが開きます。

   GitHub ユーザーインターフェイスに表示されたプルリクエスト通知を無視します。

### 手順 2：ストアフロントボイラープレートの更新

ストアフロントのボイラープレートコードを更新するには、次の情報が必要です。

- **手順 2 の GitHub リポジトリ URL**— `github.com/{ORG}/{SITE}`
   - `{ORG}` は、リポジトリの組織名またはユーザー名です。
   - `{SITE}` はリポジトリ名です。
- **手順 1 のコンテンツフォルダー URL** - `https://drive.google.com/drive/folders/{YOUR_FOLDER_ID}`
   - `{YOUR_FOLDER_ID}` は、サンプルコンテンツデータを使用して作成したフォルダーの ID です。

#### リポジトリをドキュメントオーサー環境にリンクします。

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

1. ストアフロント設定ファイルのマウントポイントを更新して、コンテンツの URL を指定します。

   1. [fstab.yaml](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/#vocabulary) 設定ファイルを開きます。

      ```yaml
      mountpoints:
        /:
          url: https://content.da.live/{org}/{site}/
          type: markup
      
      folders:
       /products/: /products/default
      ```

   1. `{ORG}` および `{SITE}` の文字列を、ボイラープレートコードに対して作成した GitHub リポジトリーの値に置き換えます。

      例えば、更新されたコードは次のようになります。

      ```yaml
      mountpoints:
        /:
          url: https://content.da.live/owner-name/aco-storefront/
          type: markup
      ```

   1. ファイルを保存します。

#### Sidekick拡張機能の設定

1. Sidekick拡張機能のプロジェクト設定を追加します。 この設定により、Sidekickを使用してストアフロントプロジェクトのコンテンツを管理できるようになります。

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

   - `{ORG}` の文字列を、リポジトリの組織またはユーザー名に置き換えます。

   - `{SITE}` の文字列をリポジトリ名に置き換えます

   +++更新した設定ファイルの例

   GitHub リポジトリの名前が `aco-storefront` で、組織の名前が `early-adopter` の場合、更新された URL は次のようになります。

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
         "url": "https://main--aco-storefront--early-adopter.aem.live/tools/picker/dist/index.html",
         "isPalette": true,
         "paletteRect": "top: 54px; left: 5px; bottom: 5px; width: 300px; height: calc(100% - 59px); border-radius: var(--hlx-sk-button-border-radius); overflow: hidden; resize: horizontal;"
       },
       {
         "id": "personalisation",
         "title": "Personalisation",
         "environments": [
           "edit"
         ],
         "url": "https://main--aco-storefront--early-adopter.aem.live/tools/segments/dist/index.html",
         "isPalette": true,
         "paletteRect": "top: 54px; left: 5px; bottom: 5px; width: 300px; height: calc(100% - 59px); border-radius: var(--hlx-sk-button-border-radius); overflow: hidden; resize: horizontal;"
       }
     ]
   }
   ```
