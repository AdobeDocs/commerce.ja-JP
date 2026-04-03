---
title: ストアフロントの設定
description: ' [!DNL Adobe Commerce Optimizer]  ストアフロントの設定方法について説明します。'
role: Developer
badgeSaas: label="SaaSのみ" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud Serviceおよび [!DNL Adobe Commerce Optimizer]  プロジェクトにのみ適用されます（Adobeで管理されるSaaS インフラストラクチャ）。"
exl-id: 2b4c9e98-a30c-4a33-b356-556de5bd721a
source-git-commit: b6f7286f223c6253ab9edbead63a4bc4a9baddfe
workflow-type: tm+mt
source-wordcount: '1420'
ht-degree: 0%

---

# ストアフロントの設定

このガイドでは、Adobe Edge Delivery Servicesを使用して[!DNL Adobe Commerce Optimizer] インスタンスのストアフロントを設定する方法について説明します。 ストアフロントには、定型文コード、サンプルコンテンツ、商品詳細ページおよび商品発見（検索とフィルタリング）のサポートが含まれます。

**完了までの推定時間：** 30 ～ 45分

## 前提条件

* リポジトリを作成でき、ローカル開発用に設定されている&#x200B;**GitHub アカウント** （github.com）
* サンプルデータと設定されたカタログビューとポリシーを含む&#x200B;**[!DNL Adobe Commerce Optimizer]インスタンス**
   * 設定手順については、[ サンプルデータの追加](get-started.md#add-sample-data)を参照してください。

### 必要なインスタンスデータ

開始する前に、[!DNL Adobe Commerce Optimizer] インスタンスから次の情報を収集します。

* **テナント ID** （インスタンス IDとも呼ばれます）
   * [ インスタンスの詳細ページ ](get-started.md#manage-instances)から入手できます
* インスタンスの&#x200B;**GraphQL エンドポイント**
   * [ インスタンスの詳細ページ ](get-started.md#manage-instances)から入手できます
* グローバル カタログ ビューの&#x200B;**カタログ ビューID**
   * [ カタログの詳細ページ ](./setup/catalog-view.md#manage-catalog-view)から入手できます
* カタログ ビューの&#x200B;**Source ロケール**
   * サンプルデータのデフォルトは`en-US`です

>[!NOTE]
>
>体験版アクセスのお客様は、インスタンスの作成時に受信したようこそメールにGraphQL エンドポイントを見つけることができます。 体験版インスタンスには、サンプルデータ、カタログビュー、ポリシーが事前に設定されています。

## ステップの設定

1. **[ストアフロントプロジェクトを作成](#create-your-storefront-project)**-[ サイト作成ツール ](https://da.live/app/adobe-commerce/storefront-tools/tools/site-creator/site-creator)を使用して、定型文コード、サンプルコンテンツ、設定ファイルを含む新しいストアフロントプロジェクトを作成します。

1. **[ストアフロント設定をカスタマイズ](#configure-your-storefront)** – リポジトリ内の`config.json` ファイルを更新して、[!DNL Adobe Commerce Optimizer] インスタンスに接続します。

1. **[設定を確認](#verify-your-setup)** （10分）
   * ストアフロントサイトのプレビュー
   * 商品詳細ページと検索機能のテスト

## ストアフロントプロジェクトの作成

サイト作成ツールは、次のコンポーネントを含む完全なストアフロントプロジェクトを作成します。

* **サイト**：ボイラープレートコンテンツを含むストアフロントのランディングページ
* **コード**：定型文ソースファイルを含むリポジトリ
* **コンテンツ**: サイト コンテンツ ファイルを含むドキュメント オーサー環境
* **Commerce Config**: [Commerce ストアフロント設定](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/commerce-configuration/){target="_blank"} （インスタンス固有の設定）

### ステップ 1：プロジェクトの生成

1. [ サイト作成者ツール ](https://da.live/app/adobe-commerce/storefront-tools/tools/site-creator/site-creator)を開きます

   ![[!DNL Site Creator tool]](./assets/storefront-setup-site-creator.png){width="700" zoomable="yes"}

1. **新しいサイトを作成（コードとコンテンツ）**&#x200B;を選択します。

1. サイト設定を完了します。

   * **GitHub Organization/Username**: GitHub ユーザー名または組織名を入力してください
   * **サイト名**: ストアフロントにわかりやすい名前を選択します
   * **Commerce GraphQL エンドポイント （オプション）**: [!DNL Adobe Commerce Optimizer] インスタンスのGraphQL エンドポイントを入力します

1. 「**サイトを作成**」をクリックして、ストアフロントのボイラープレートコードを使用してGitHub リポジトリを作成します。

   リポジトリが作成されると、サイト作成者が更新され、Code Sync アプリのインストールを求めるメッセージが表示されます。

### 手順2:Code Sync アプリのインストール

1. 「**[!UICONTROL Install AEM Code Sync App]**」をクリックして、Code Sync インストーラーを新しいタブで開きます。

1. Code Sync アプリを設定します。
   * GitHub組織を選択し、**[!UICONTROL Configure]**&#x200B;をクリックします。
   * コード同期インターフェイスで、**[!UICONTROL Only select repositories]**&#x200B;をクリックします。
   * **[!UICONTROL Select repositories]** メニューをクリックし、作成したストアフロントコードリポジトリを選択します。
   * **[!UICONTROL Save]**&#x200B;をクリックしてリポジトリを登録します。

1. サイト作成者が開いているブラウザーウィンドウに戻り、**サイトを作成**&#x200B;をクリックします。

   サイト作成者は、ストアフロントのボイラープレートコンテンツをDocument Author環境にコピーします。 このプロセスには1～2分かかります。

### 手順3：プロジェクトリンクの保存

1. 「サイトの詳細」セクションで、ストアフロントプロジェクトのリンクを確認します。

   ![[!DNL Storefront setup complete]](./assets/storefront-setup-complete.png){width="700" zoomable="yes"}

   これらのリンクを使用して、ストアフロントコード、コンテンツ、設定を管理します。

1. 将来の参照のために、これらのリンクをコピーして保存します：**[!UICONTROL Copy]をクリックします。

## ストアフロントの設定

ストアフロント設定を更新して、[!DNL Adobe Commerce Optimizer] インスタンスに接続します。

1. `config.json` ファイルをボイラープレートコードリポジトリで開きます。

   `https://github.com/<username or org>/<repo name>/config.json`

1. 設定の`cs` （カタログサービス）セクションを探します。

1. プレースホルダーの値をインスタンスの値に置き換えます。 [前提条件](#prerequisites)を参照してください。

   ```json
   "cs": {
      "AC-View-ID": "{catalogViewId}",
      "AC-Source-Locale": "en-US",
      "AC-Price-Book-ID": "{priceBookId}"
   }
   ```

   >[!NOTE]
   >
   >価格表IDを見つけるには、[の](./setup/catalog-view.md) カタログ表示設定の詳細[!DNL Adobe Commerce Optimizer]を確認して、割り当てられた価格表を確認します。 価格表が割り当てられていない場合は、このヘッダーを設定ファイルから削除できます。 価格表がカタログ ビューに割り当てられたときに再度追加します。

1. 設定ファイルを保存します。

   設定の変更が反映されるまでに数分かかる場合があります。 データがすぐに表示されない場合は、トラブルシューティングの2～3分前に待ってください。

## 設定を確認

ストアフロントをテストして、[!DNL Adobe Commerce Optimizer] インスタンスに正しく接続されていることを確認します。

### ステップ 1：ストアフロントホームページを表示する

1. ライブプレビューURLに移動します。

   `https://main--{SITE}--{ORG}.aem.live`

   `{ORG}`と`{SITE}`をGitHub組織とサイト名に置き換えます。

1. **成功基準**：定型文のコンテンツを含むストアフロントのホームページが表示されます。

   ![[!DNL ACO storefront site with boilerplate]](./assets/aco-storefront-site-boilerplate.png){width="700" zoomable="yes"}

### ステップ 2：商品詳細ページのテスト

デフォルトの製品詳細ページを表示して、製品データが正しく読み込まれていることを確認します。

1. サンプル製品ページに移動します。
   `https://main--{SITE}--{ORG}.aem.live/products/placeholder/{sku}`

   サンプルデータから任意のSKUを使用します。例えば、次のようになります。
   `https://main--{SITE}--{ORG}.aem.live/products/placeholder/aur-flu-tir-std-2017`

   デフォルトのストアフロントでは、ルートの`placeholder`値を使用して製品を表示できます。 ストアフロントのカスタマイズを開始する際には、ストアフロントコードをカスタマイズして、カタログで定義された製品ルートに基づいて、製品詳細ページへのパスを設定できます。

   >[!TIP]
   >
   >[ インスタンスの](./setup/data-sync.md) データ同期[!DNL Adobe Commerce Optimizer] ページから使用可能なSKUを表示します。

1. **成功基準**: ページに次の情報を表示する必要があります：
   * 製品名、説明、価格
   * 製品画像
   * カートに追加機能
   * [!DNL Adobe Commerce Optimizer] インスタンスから取得したデータ

   ![[!DNL Default product detail page showing a product from the sample data]](./assets/storefront-boilerplate-product-page.png){width="700" zoomable="yes"}

### 手順3：デフォルトの検索機能をテストする

検索やフィルタリングなど、商品のデフォルト機能をテストできます。

1. ストアフロントのホームページで、ヘッダーの虫眼鏡アイコンをクリックします。

1. 検索文字列`tires`を入力し、**Enter**&#x200B;を押します。

1. **成功基準**：次が表示されます。
   * タイヤ商品の検索結果ページ
   * サイドバーのフィルターオプション
   * 画像と価格設定が掲載された商品リスト

   ![[!DNL View search results page]](./assets/storefront-with-aco-search-results-page.png){width="675" zoomable="yes"}

1. 任意のタイヤ製品をクリックして、その詳細ページを表示します。

   ![[!DNL View product details page]](./assets/storefront-with-aco-pdp-page.png){width="675" zoomable="yes"}

## トラブルシューティング

設定中に問題が発生した場合は、web ページインスペクターコンソールを使用してエラーを確認します。 また、ブラウザーのキャッシュをクリアするか、別のブラウザーを使用してみてください。

一般的な問題を確認するには、次のガイダンスを使用します。

### 一般的な問題

| イシュー | 症状 | Solution |
|-------|----------|----------|
| **Code Syncのインストールに失敗しました** | Code Sync設定を完了できません | <ul><li>GitHub組織への管理者アクセス権があることを確認します。</li><li>組織の代わりに個人リポジトリを使用してみてください。</li><li>GitHub権限を確認して、もう一度試してください。</li></ul> |
| **サイトが読み込まれていません** | 404または接続エラー | <ul><li>サイト URL形式を確認してください：`https://main--{SITE}--{ORG}.aem.live`</li><li>Code Sync アプリが適切にインストールされていることを確認します。</li><li>リポジトリが公開されているか、適切に設定されていることを確認します。</li></ul> |
| **商品データが表示されていません** | 製品ページにプレースホルダーまたはエラーが表示される | <ul><li>`config.json`で設定値を確認してください</li><li>[!DNL Adobe Commerce Optimizer] インスタンスで、データ同期ページを確認して、サンプル製品が読み込まれていることを確認します。 使用可能な製品がない場合は、サンプルデータをリロードするか、[Data Ingestion API](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/using-the-api/#make-your-first-request){target="_blank"}を使用して製品を追加します。 設定変更が反映されるまで数分待ちます。</li><li>マーチャンダイジングサービス [製品クエリ ](https://developer.adobe.com/commerce/services/optimizer/merchandising-services/use-cases/#return-product-details){target="_blank"}を使用して、`config.json` ファイルで設定されているのと同じヘッダーを使用して、製品の詳細を取得してみてください。 データを取得できる場合は、カタログビューの設定に関する問題またはインデックスエラーが発生している可能性があります。</li></ul> |
| **検索で結果が返されない** | 検索結果ページが空です | <ul><li>マーチャンダイジングサービス [productSearch クエリ ](https://developer.adobe.com/commerce/services/optimizer/merchandising-services/use-cases/#product-search){target="_blank"}を使用して、`config.json` ファイルで設定された同じヘッダーを使用して、製品検索結果を取得できることを確認します。 データを取得できる場合は、カタログビューの設定に関する問題またはインデックスエラーが発生している可能性があります。</li><li>`config.json` ファイルのカタログビューIDが[!DNL Adobe Commerce Optimizer]のカタログビューIDと一致することを確認します。</li><li>Adobe Commerce Optimizerで、ストアフロントヘッダー設定で使用したポリシー、ロケール、価格表の設定を確認します。</li><li>[属性メタデータ設定](https://developer.adobe.com/commerce/services/reference/rest/#operation/createProductMetadata){target="_blank"}が検索用に正しく設定されていることを確認します。</li></ul> |

### 検証チェックリスト

次の手順に進む前に、次の点を確認して、ストアフロントが正しく機能していることを確認します。

![ チェックリスト ](/help/assets/icons/Smock_CheckmarkCircleOutline_18_N.svg)設定値がインスタンス設定<br>と一致しています
![ チェックリスト ](/help/assets/icons/Smock_CheckmarkCircleOutline_18_N.svg) ストアフロントのホームページがエラーなく読み込まれる<br>
![ チェックリスト ](/help/assets/icons/Smock_CheckmarkCircleOutline_18_N.svg)少なくとも1つの製品詳細ページに完全な情報が表示される<br>
![ チェックリスト ](/help/assets/icons/Smock_CheckmarkCircleOutline_18_N.svg)検索機能が関連する結果を返します<br>
![ チェックリスト ](/help/assets/icons/Smock_CheckmarkCircleOutline_18_N.svg)製品画像が正しく読み込まれています<br>
![ チェックリスト ](/help/assets/icons/Smock_CheckmarkCircleOutline_18_N.svg)設定値がインスタンス設定と一致しています<br>

### ヘルプを表示

問題が解決しない場合：

* [Adobe Commerce Storefront ドキュメントを確認](https://experienceleague.adobe.com/developer/commerce/storefront/){target="_blank"}
* [Adobe Commerce Optimizer開発者向けガイド ](https://developer.adobe.com/commerce/services/optimizer/){target="_blank"}を確認する
* [Adobe Commerce サポートリソース ](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/overview){target="_blank"}にアクセス

## 次のステップ

* **[ローカル開発環境の設定](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/create-storefront/#set-up-local-environment){target="_blank"}** – ローカル環境を作成して、ストアフロントコードとコンテンツをカスタマイズします。
* **[ユニバーサルエディターを有効にする](https://experienceleague.adobe.com/developer/commerce/storefront/merchants/quick-start/universal-editor/){target="_blank"}**- ユニバーサルエディターを使用すると、レンダリングされたページのコンテキストでストアフロントコンテンツを編集できます。 コンテンツはドキュメント作成（DA.live）プロジェクトに保存され、ローカライゼーション、一括公開、スナップショットなど、ほとんどのコンテンツオーケストレーションアプリを使用できます。

### 学習と探索

* **[エンドツーエンドのユースケースを完了](./use-case/admin-use-case.md)**-[!DNL Adobe Commerce Optimizer]を使用したストアフロントの設定とカタログ管理について詳しく説明します。

* **[ストアフロントのカスタマイズ ](https://experienceleague.adobe.com/developer/commerce/storefront/setup/){target="_blank"}**&#x200B;の詳細な設定と設定オプションについて説明します。

* **[Commerce ドロップインを使用してストアフロント エクスペリエンスをカスタマイズする](https://experienceleague.adobe.com/developer/commerce/storefront/dropins/all/introduction/){target="_blank"}** – 事前定義済みコンポーネントを追加して、ストアフロント エクスペリエンスを強化します。

* **ストアフロント設定サービスへの移行** – 最初のストアフロントを作成した後、設定を移行して、再帰設定やオーバーレイなどの高度なユースケースをサポートする設定サービスを使用できます。 詳しくは、Adobe Experience Managerの[Configuration Service](https://www.aem.live/docs/config-service-setup){target="_blank"} ドキュメントを参照してください。

>[!MORELIKETHIS]
>
> サイトコンテンツの更新と、Commerce フロントエンドコンポーネントおよびバックエンドデータとの統合について詳しくは、[Adobe Commerce Storefront ドキュメント ](https://experienceleague.adobe.com/developer/commerce/storefront/){target="_blank"}を参照してください。
