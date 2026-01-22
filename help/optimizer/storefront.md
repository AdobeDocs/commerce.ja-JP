---
title: ストアフロントの設定
description: ストアフロントの設定方法  [!DNL Adobe Commerce Optimizer]  説明します。
role: Developer
badgeSaas: label="SaaS のみ" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud Serviceおよびプロジェクトのみ（Adobe [!DNL Adobe Commerce Optimizer]  管理される SaaS インフラストラクチャ）に適用されます。"
exl-id: 2b4c9e98-a30c-4a33-b356-556de5bd721a
source-git-commit: 0cd9749574460374a8fe875f1eff54f2a4a8d614
workflow-type: tm+mt
source-wordcount: '1397'
ht-degree: 0%

---

# ストアフロントの設定

このガイドでは、Adobe Edge 配信サービスを使用して [!DNL Adobe Commerce Optimizer] インスタンスのストアフロントを設定する手順について説明します。 ストアフロントには、ボイラープレートコード、サンプルコンテンツ、製品詳細ページと製品検出（検索とフィルタリング）のサポートが含まれています。

**完了までの推定時間：** 30 ～ 45 分

## 前提条件

* リポジトリを作成でき、ローカル開発用に設定されている **GitHub アカウント** （github.com）
* サンプルデータ **[!DNL Adobe Commerce Optimizer]設定済みのカタログビューとポリシーを備えた** インスタンス
   * 設定手順については、[ サンプルデータの追加 ](get-started.md#add-sample-data) を参照してください。

### 必要なインスタンスデータ

開始する前に、[!DNL Adobe Commerce Optimizer] インスタンスから次の情報を収集します。

* **テナント ID** （インスタンス ID とも呼ばれます）
   * [ インスタンスの詳細ページ ](get-started.md#manage-instances) から使用できます。
* お使いのインスタンスの **GraphQL エンドポイント**
   * [ インスタンスの詳細ページ ](get-started.md#manage-instances) から使用できます。
* グローバル カタログ ビューの **カタログ ビュー ID**
   * [ カタログの詳細ページ ](./setup/catalog-view.md#manage-catalog-view) から使用できます
* カタログビューの **0}Source ロケール }**
   * サンプルデータのデフォルトは `en-US` です

>[!NOTE]
>
>体験版アクセスのお客様は、インスタンスの作成時に受信したお知らせメールでGraphQL エンドポイントを見つけることができます。 体験版インスタンスには、サンプルデータ、カタログビュー、ポリシーが事前に設定されています。

## ステップの設定

1. **[ストアフロントプロジェクトを作成](#create-your-storefront-project)** - [ サイト作成ツール ](https://da.live/app/adobe-commerce/storefront-tools/tools/site-creator/site-creator) を使用して、ボイラープレートコード、サンプルコンテンツ、設定ファイルを含む新しいストアフロントプロジェクトを作成します。

1. **[ストアフロント設定のカスタマイズ](#customize-the-storefront-configuration)** - リポジトリの `config.json` ファイルを更新して、[!DNL Adobe Commerce Optimizer] インスタンスに接続します。

1. **[設定を確認してください](#verify-your-setup)** （10 分）
   * ストアフロントサイトのプレビュー
   * 製品詳細ページと検索機能のテスト

## ストアフロントプロジェクトの作成

Site Creator ツールは、次のコンポーネントを含む完全なストアフロントプロジェクトを作成します。

* **サイト**：ボイラープレートコンテンツを含んだストアフロントのランディングページ
* **コード**：ボイラープレートソースファイルを含むリポジトリ
* **コンテンツ**：サイトコンテンツファイルを含むドキュメントオーサー環境
* **Commerce設定**: インスタンス固有の設定用の `config.json` ファイル

### 手順 1：プロジェクトの生成

1. [ サイト作成ツール ](https://da.live/app/adobe-commerce/storefront-tools/tools/site-creator/site-creator) を開きます。

   ![[!DNL Site Creator tool]](./assets/storefront-setup-site-creator.png){width="700" zoomable="yes"}

1. 「**新しいサイトを作成（コードとコンテンツ）**」を選択します。

1. サイト設定を完了します。

   * **GitHub 組織/ユーザー名**:GitHub のユーザー名または組織名を入力します
   * **サイト名**：ストアフロントのわかりやすい名前を選択します
   * **Commerce GraphQL エンドポイント（オプション）**：お使いの [!DNL Adobe Commerce Optimizer] インスタンスのGraphQL エンドポイントを入力します

1. **サイトを作成** をクリックして、ストアフロントのボイラープレートコードを使用して GitHub リポジトリを作成します。

   リポジトリが作成されると、サイト作成者が更新され、コード同期アプリをインストールするように求められます。

### 手順 2：コード同期アプリのインストール

1. 「**[!UICONTROL Install AEM Code Sync App]**」をクリックして、コード同期インストーラーを新しいタブで開きます。

1. コード同期アプリを設定します。
   * GitHub 組織を選択し、「**[!UICONTROL Configure]**」をクリックします。
   * コード同期インターフェイスで、「同期」をクリック **[!UICONTROL Only select repositories]** ます。
   * **[!UICONTROL Select repositories]** メニューをクリックし、作成したストアフロントコードリポジトリを選択します。
   * 「**[!UICONTROL Save]**」をクリックしてリポジトリを登録します。

1. サイト作成者が開いているブラウザーウィンドウに戻り、「**サイトを作成**」をクリックします。

   Site Creator は、ストアフロントのボイラープレートコンテンツをドキュメントオーサー環境にコピーします。 このプロセスには 1～2 分かかります。

### 手順 3：プロジェクトリンクの保存

1. 「サイトの詳細」セクションで、ストアフロントプロジェクトのリンクを確認します。

   ![[!DNL Storefront setup complete]](./assets/storefront-setup-complete.png){width="700" zoomable="yes"}

   これらのリンクを使用して、ストアフロントのコード、コンテンツ、設定を管理します。

1. 今後の参照用に、これらのリンクをコピーして保存します。**[!UICONTROL Copy] をクリックします。

## ストアフロントの設定

ストアフロント設定を更新して、[!DNL Adobe Commerce Optimizer] インスタンスに接続します。

1. ボイラープレートコードリポジトリ内の `config.json` ファイルを開きます。

   `https://github.com/<username or org>/<repo name>/config.json`

1. 設定で `cs` （カタログサービス）」セクションを見つけます。

1. プレースホルダーの値をインスタンスの値に置き換えます。 [ 前提条件 ](#prerequisites) を参照してください。

   ```json
   "cs": {
      "AC-View-ID": "{catalogViewId}",
      "AC-Source-Locale": "en-US",
      "AC-Price-Book-ID": "{priceBookId}"
   }
   ```

   >[!NOTE]
   >
   >価格台帳 ID を検索するには、Adobe Commerce Optimizerで [ カタログ表示構成詳細 ](./setup/catalog-view.md) をチェックして、割り当てられた価格台帳を確認します。 価格台帳が割り当てられていない場合は、構成ファイルからこのヘッダーを削除できます。 価格台帳がカタログ ビューに割り当てられたら、再度追加します。

1. 設定ファイルを保存します。

   設定変更が反映されるまで数分かかる場合があります。 データがすぐに表示されない場合は、2～3 分待ってからトラブルシューティングを行ってください。

## 設定を確認

ストアフロントをテストし、[!DNL Adobe Commerce Optimizer] インスタンスに正しく接続されていることを確認します。

### 手順 1：ストアフロントのホームページを表示する

1. ライブプレビュー URL に移動します。

   `https://main--{SITE}--{ORG}.aem.live`

   `{ORG}` と `{SITE}` を GitHub の組織とサイト名に置き換えます。

1. **成功基準**：ボイラープレートコンテンツが含まれたストアフロントのホームページが表示されます。

   ![[!DNL ACO storefront site with boilerplate]](./assets/aco-storefront-site-boilerplate.png){width="700" zoomable="yes"}

### 手順 2：製品の詳細ページのテスト

デフォルトの製品詳細ページを表示して、製品データが正しく読み込まれていることを確認します。

1. サンプル製品ページに移動します。
   `https://main--{SITE}--{ORG}.aem.live/products/placeholder/{sku}`

   サンプルデータから任意の SKU を使用します。例：
   `https://main--{SITE}--{ORG}.aem.live/products/placeholder/aur-flu-tir-std-2017`

   デフォルトのストアフロントの場合、ルートの `placeholder` 値を使用して製品を表示できます。 ストアフロントのカスタマイズを開始する際に、ストアフロントコードをカスタマイズして、カタログで定義された製品ルートに基づいて製品の詳細ページへのパスを設定できます。

   >[!TIP]
   >
   >[ インスタンスの ](./setup/data-sync.md) データ同期 [!DNL Adobe Commerce Optimizer] ページで使用可能な SKU を表示します。

1. **成功基準**：ページには、次が表示されます。
   * 商品名、説明、価格
   * 製品画像
   * 買い物かごに追加機能
   * [!DNL Adobe Commerce Optimizer] インスタンスから取得したデータ

   ![[!DNL Default product detail page showing a product from the sample data]](./assets/storefront-boilerplate-product-page.png){width="700" zoomable="yes"}

### 手順 3：デフォルトの検索機能のテスト

検索やフィルタリングを含む、デフォルトの製品機能をテストする。

1. 店頭ホームページで、ヘッダーの虫眼鏡アイコンをクリックします。

1. 検索文字列 `tires` を入力し、**Enter** キーを押します。

1. **成功基準**：次が表示されます。
   * タイヤ製品の検索結果ページ
   * サイドバーのフィルタリングオプション
   * 画像と価格を含む製品リスト

   ![[!DNL View search results page]](./assets/storefront-with-aco-search-results-page.png){width="675" zoomable="yes"}

1. タイヤ製品をクリックすると、詳細ページが表示されます。

   ![[!DNL View product details page]](./assets/storefront-with-aco-pdp-page.png){width="675" zoomable="yes"}

## トラブルシューティング

セットアップ中に問題が発生した場合は、web ページ検査コンソールを使用してエラーを確認します。 また、ブラウザーのキャッシュをクリアするか、別のブラウザーを使用してみてください。

一般的な問題を確認するには、次のガイダンスを使用します。

### よくある問題

| 問題 | 症状 | 解決策 |
|-------|----------|----------|
| **コード同期のインストールに失敗** | コード同期セットアップを完了できません | <ul><li>GitHub 組織に管理者アクセス権があることを確認します。</li><li>組織ではなく個人用リポジトリを使用してみてください。</li><li>GitHub の権限を確認して、もう一度試してください。</li></ul> |
| **サイトが読み込まれない** | 404 または接続エラー | <ul><li>サイトの URL 形式を確認してください：`https://main--{SITE}--{ORG}.aem.live`</li><li>コード同期アプリが正しくインストールされていることを確認します。</li><li>リポジトリが公開されているか、適切に設定されていることを確認します。</li></ul> |
| **製品データが表示されません** | 製品ページにプレースホルダーまたはエラーが表示される | <ul><li>`config.json` で設定値を確認します。</li><li>[!DNL Adobe Commerce Optimizer] インスタンスで、データ同期ページをチェックして、サンプル製品が読み込まれていることを確認します。 使用できる製品がない場合は、サンプルデータを再読み込みするか、[Data Ingestion API](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/using-the-api/#make-your-first-request) を使用して製品を追加します。 設定変更が反映されるまで数分待ちます。</li><li>[ ファイルで設定されているのと同じヘッダーを使用して、マーチャンダイジングサービス ](https://developer.adobe.com/commerce/services/optimizer/merchandising-services/use-cases/#return-product-details) 製品クエリ `config.json` を使用して製品の詳細を取得してみてください。 データを取得できる場合は、カタログ表示の設定またはインデックスエラーの問題がある可能性があります。</li></ul> |
| **検索で結果が返されない** | 空の検索結果ページ | <ul><li>[ ファイルで設定されているのと同じヘッダーを使用して、マーチャンダイジングサービス ](https://developer.adobe.com/commerce/services/optimizer/merchandising-services/use-cases/#product-search)productSearch クエリ `config.json` を使用して製品の検索結果を取得できることを確認します。 データを取得できる場合は、カタログ表示の設定またはインデックスエラーの問題がある可能性があります。</li><li>`config.json` ファイルのカタログ ビュー ID が [!DNL Adobe Commerce Optimizer] のカタログ ビュー ID と一致することを確認します。</li><li>Adobe Commerce Optimizerで、ストアフロントのヘッダー設定で使用したポリシー、ロケール、価格台帳の設定を確認します。</li><li>[ 属性メタデータ設定 ](https://developer.adobe.com/commerce/services/reference/rest/#operation/createProductMetadata) が検索に対して正しく設定されていることを確認します。</li></ul> |

### 検証チェックリスト

次の手順に進む前に、次の点を確認して、ストアフロントが正常に機能していることを確認します。

![ チェックリスト ](/help/assets/icons/Smock_CheckmarkCircleOutline_18_N.svg) 設定値がインスタンス設定と一致する <br>
![ チェックリスト ](/help/assets/icons/Smock_CheckmarkCircleOutline_18_N.svg) ストアフロントのホームページがエラーなしで読み込まれる <br>
![ チェックリスト ](/help/assets/icons/Smock_CheckmarkCircleOutline_18_N.svg)1 つ以上の製品の詳細ページに完全な情報が表示される <br>
![ チェックリスト ](/help/assets/icons/Smock_CheckmarkCircleOutline_18_N.svg) 検索機能で関連する結果が返される <br>
![ チェックリスト ](/help/assets/icons/Smock_CheckmarkCircleOutline_18_N.svg) 製品画像が正しく読み込まれている <br>
![ チェックリスト ](/help/assets/icons/Smock_CheckmarkCircleOutline_18_N.svg) 設定値がインスタンス設定と一致する <br>

### ヘルプを表示

問題が解決しない場合：

* [Adobe Commerce ストアフロントのドキュメントを確認してください ](https://experienceleague.adobe.com/developer/commerce/storefront/)
* [Adobe Commerce Optimizer開発者ガイドを確認してください ](https://developer.adobe.com/commerce/services/optimizer/)
* [Adobe Commerce サポートリソース ](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/overview) にアクセスします

## 次の手順

ストアフロントを設定して検証すると、次の操作を実行できます。

1. **[Sidekick](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/create-storefront/#install-and-configure-sidekick)** ブラウザー拡張機能をインストールして、web サイトから直接コンテンツを編集、プレビューおよび公開します。

2. **[ローカル開発環境の設定 ](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/create-storefront/#set-up-local-environment)** - ストアフロントのコードとコンテンツをカスタマイズするローカル環境を作成します。

### の学習と探索

* **[エンドツーエンドの使用例を完了](./use-case/admin-use-case.md)** - [!DNL Adobe Commerce Optimizer] を使用したストアフロントのセットアップとカタログ管理の詳細について説明します。

* **[ストアフロントのカスタマイズについて ](https://experienceleague.adobe.com/developer/commerce/storefront/setup/)** - セットアップと設定の詳細オプションについて説明します。

* **[Commerce ドロップダウンを使用してストアフロントのエクスペリエンスをカスタマイズ ](https://experienceleague.adobe.com/developer/commerce/storefront/dropins/all/introduction/)** 事前定義済みコンポーネントを追加して、ストアフロントのエクスペリエンスを強化します。

* **ストアフロント構成サービスに移行** – 初期ストアフロントを作成したら、構成サービスを使用するように構成を移行できます。このサービスは、リポジトリ構成やオーバーレイなどの高度なユースケースをサポートします。 詳しくは、Adobe Experience Managerにある [ 設定サービス ](https://www.aem.live/docs/config-service-setup) ドキュメントを参照してください。

>[!MORELIKETHIS]
>
> サイトコンテンツの更新と [Adobe Commerceのフロントエンドコンポーネントおよびバックエンドデータとの統合について詳しくは、](https://experienceleague.adobe.com/developer/commerce/storefront/)Commerce ストアフロントのドキュメントを参照してください。
