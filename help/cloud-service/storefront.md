---
title: ストアフロントの設定
description: 基礎ツールを実行してストアフロントを設定する方法  [!DNL Adobe Commerce as a Cloud Service]  説明します。
role: Developer
exl-id: 02928dc4-1777-483e-b0ee-b04fc813864d
source-git-commit: 022e3474b8f2839d2501c46def21733a8d4ad9cc
workflow-type: tm+mt
source-wordcount: '548'
ht-degree: 0%

---

# ストアフロントの設定

{{accs-early-access}}

次の手順は、`aio commerce init` コマンドを使用してEdge Deliveryを搭載したAdobe Commerce Storefront をすばやく設定する方法を示しています。 このプロセスにより、次の設定が行われます。

* [Edge Delivery ServicesによるCommerce ストアフロント ](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/?lang=ja) - Adobe Edge Delivery Servicesを活用した、パフォーマンス、拡張性、安全性の高いストアフロントです。
* [Adobe Developer App Builderの API メッシュ ](https://developer.adobe.com/graphql-mesh-gateway/mesh/) – 複数のデータソースを 1 つのGraphQL エンドポイントに組み合わせることができる API プラットフォーム。 API メッシュは、1 つのゲートウェイを介してサードパーティ API とAdobe API を統合します。 1 つのGraphQL エンドポイントに対する 1 つのクエリで、複数のソースから結果を返すことができます。
* [Adobe Developer Console](https://developer.adobe.com/developer-console/docs/guides/) - Adobe アプリケーション用のプロジェクトを構築するために使用できる、API、イベント、ランタイム関数、プラグインへのアクセスを備えたデベロッパーツールのコレクションです。
* [Adobe I/O Runtime](https://developer.adobe.com/runtime/docs/) - クラウド内のイベントに応答し、関数を実行するカスタムコードをデプロイするためのサーバーレスエンジン。

## 前提条件

`aio commerce init` コマンドを実行する前に、次の前提条件を満たす必要があります。

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

1. [Adobe I/O Runtime CLI](https://developer.adobe.com/runtime/docs/guides/tools/cli_install/) をインストールします。

   ```bash
   npm install -g @adobe/aio-cli
   ```

1. Adobe I/O API メッシュ プラグインをインストールします。

   ```bash
   aio plugins:install @adobe/aio-cli-plugin-api-mesh
   ```

1. Adobe I/O Commerce プラグインをインストールします。

   ```bash
   aio plugins:install https://github.com/adobe-commerce/aio-cli-plugin-commerce
   ```

1. 既存のプラグインを更新します。

   ```bash
   aio plugins:update
   ```

1. Adobe Experience Cloud アカウントにログインします。

   ```bash
   aio login
   ```

1. IMS 組織、プロジェクト、ワークスペースを選択します。 矢印キーを使用し、**Enter** キーを押して、選択を行います。 `aio` コマンドについて詳しくは、[Adobe I/O CLI ドキュメント ](https://github.com/adobe/aio-cli-plugin-console?tab=readme-ov-file#commands) を参照してください。

   ```bash
   aio console org select
   ```

   ```bash
   aio console project select
   ```

   ```bash
   aio console workspace select
   ```

1. まだ承認していない場合は、Adobe Developer コンソールでhttps://developer.adobe.com/console/homeに移動し、「同意して続行 **をクリックして、デベロッパー利用規約に同意してくだ** い。

## `aio commerce init` コマンドを実行します。

次のコマンドを実行すると、Commerce ストアフロントの基礎モードが作成されます。 この基礎モードは、ストアフロントの構築と理解に最適な出発点となります。 ストアフロントの操作について詳しくは、[Adobe Commerce ストアフロントのドキュメント ](https://experienceleague.adobe.com/developer/commerce/storefront/?lang=ja) を参照してください。


1. `init` コマンドを実行します。

   ```bash
   aio commerce init
   ```

1. 既に GitHub にログインしている場合は、`Y` と入力して、ユーザー名の下にリポジトリを作成します。

1. 作成するリポジトリの名前を入力します。

1. 次のいずれかのオプションを選択します。

   * **デモ Adobe Commerce テナントを使用** - デモテナントを使用します。
      * このオプションを選択すると、ブラウザーウィンドウにAEM Code Sync ボットをインストールするように求められます。 作成したリポジトリを指定し、ボットを認証する必要があります。 CLI に戻り、`y` と入力して、AEM Code Sync ボットのインストールを確認します。
   * **使用可能なAdobe Commerce テナントを選択** – 選択した組織内の既存のCommerce テナントを選択します。
      * このオプションを選択した場合、メッシュを作成するプロジェクトとワークスペースを選択する必要があります。
   * **独自のAdobe Commerce テナント API URL を指定** – 早期アクセスプログラムの参加者の場合は、このオプションを選択します。 Adobeのオンボーディングメールで提供された API URL を入力します。

   >[!NOTE]
   >
   >「`Pick an available API (Mesh -> SaaS)`」オプションを選択する場合は、Adobe Developer Consoleに既存のプロジェクトとWorkspaceが必要です。 [ テンプレート化されたプロジェクトを作成 ](https://developer.adobe.com/developer-console/docs/guides/projects/projects-template/) し、「App Builder」を選択すると、必要なワークスペースが自動的に作成されます。

1. プロセスが完了したら、次の方法でストアフロントをカスタマイズできます。

   * コードのカスタマイズ：`https://github.com/<username or org>/<repo name>`
   * コンテンツを編集：`https://da.live/#/<username or org>/<repo name>`
   * 設定を管理：`https://da.live/sheet#/<username or org>/<repo name>/configs-stage`
   * ストアフロントのプレビュー：`https://main--<repo name>--<username or org>.aem.page/`
   * ローカルで実行：`aio commerce:dev`

ストアフロントをカスタマイズするには、[Adobe Commerce ストアフロントのドキュメント ](https://experienceleague.adobe.com/developer/commerce/storefront/?lang=ja) を参照してください。
