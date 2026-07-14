---
title: Adobe Experience Platformタグを使用したCommerceデータの収集
description: Adobe Experience Platform タグを使用してCommerce データを収集する方法について説明します。
role: Admin, Developer
feature: Personalization, Integration
exl-id: dab333e8-5f71-4f3e-9660-6363b0e230c8
TQID: https://experienceleague.adobe.com/7HNafiIenZfLrAhILPMwuUzRDzBVuClvDchJBGEg6bs
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: c1256247-af4b-46d8-9dca-0c654ecfa157id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: d3cdead0-685a-4489-9250-4bb709942f66id: e0eb8757-182f-49f3-94a4-1587d16f5094id: f4e6943a-c91a-4134-a2c7-f4f20cfff2f0
source-git-commit: 2362159cd352d812f60838b42ade1e98bab5a0d3
workflow-type: tm+mt
source-wordcount: 2684
ht-degree: 0%

---

# Adobe Experience Platformタグを使用したCommerceデータの収集

[!DNL Data Connection]拡張機能を使用してストアフロントイベントを公開および購読することはできますが、一部のマーチャントは、既に[Adobe Experience Platform タグ ](https://experienceleague.adobe.com/docs/platform-learn/data-collection/tags/create-a-property.html)などのデータ収集ソリューションを使用している場合があります。 これらの販売者に対して、Adobe Commerceでは、Adobe Commerce Event SDKを使用する[!DNL Data Connection]拡張機能でのみ公開オプションを提供しています。

![[!DNL Data Connection]拡張機能データフロー](assets/tags-data-flow.png)
タグ _を含む_[!DNL Data Connection]&#x200B;拡張データフロー

このトピックでは、[!DNL Data Connection]拡張機能によって提供されるストアフロントイベント値を、既に使用しているAdobe Experience Platform タグソリューションにマッピングする方法について説明します。

## Adobe Commerceからのイベントデータの収集

Commerce イベントデータを収集するには：

- [Adobe Commerce Events SDK](https://github.com/adobe/commerce-events/tree/main/packages/storefront-events-sdk)をインストールします。 PHP ストアフロントについては、[install](install.md) トピックを参照してください。 PWA Studio ストアフロントについては、[PWA Studio ガイド ](https://developer.adobe.com/commerce/pwa-studio/integrations/adobe-commerce/aep/)を参照してください。

  >[!NOTE]
  >
  > Tags for collectionを使用する場合は、Commerce管理者で組織IDとデータストリーム IDを&#x200B;**not** [configure](connect-data.md)してください。 複数のweb サイトマーチャントが、タグのプロパティまたは環境ごとにデータストリームを設定します。 Commerce Admin スコープの動作については、[Configuration scope](connect-data.md#configuration-scope)を参照してください。

## Commerce ストアフロントデータをAdobe Experience Platformにマッピングする

Commerce ストアフロントデータをAdobe Experience Platformにマッピングするには、Adobe Experience Platform タグ内から以下を設定してインストールします。

1. [Adobe Experience Platform Data Collectionでタグプロパティ ](https://experienceleague.adobe.com/docs/platform-learn/implement-in-websites/configure-tags/create-a-property.html)を設定します。

1. **オーサリング**&#x200B;で、**拡張機能**&#x200B;を選択し、次の拡張機能をインストールして設定します。

   - [Adobe Client Data Layer](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/client/client-data-layer/overview.html)

   - [Adobe Experience Platform Web SDK](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/installing-the-sdk.html)

1. [ タグ ](https://experienceleague.adobe.com/docs/experience-platform/tags/publish/overview.html)を開発環境に公開します。

1. 以下の&#x200B;**イベントマッピング**&#x200B;の手順に従って、特定のイベントのデータ要素とルールを設定します。

### イベントマッピング

タグを使用したデータ収集は、Adobe Commerce Event SDKを使用したデータ収集とは異なるため、両方のフレームワークで使用される同等の用語を理解することが重要です。

| Adobe Experience Platformのタグ用語 | Adobe Commerce イベント SDK用語 |
|---|---|
| _データ要素_ | コンテキスト |
| _ルール_ | イベント |
|  | _ルール条件_ - イベントリスナー（ACDLから） <br><br>_ルールアクション_ - イベントハンドラー（Adobe Experience Platformに送信） |

Adobe Experience Platform タグのデータ要素とルールをAdobe Commerce固有のイベントデータで更新する場合は、いくつかの一般的な手順を実行します。

例えば、Adobe Commerce `signOut` イベントをAdobe Experience Platform タグに追加します。 以下に説明する手順は、設定した特定の値を除いて、[data elements](https://experienceleague.adobe.com/docs/experience-platform/collection/e2e.html#data-element)と[rules](https://experienceleague.adobe.com/docs/experience-platform/collection/e2e.html#create-a-rule)を追加する方法を説明します。この方法は、タグに追加するすべてのAdobe Commerce イベントに適用されます。

1. データ要素の作成：

   ![新しいデータ要素を作成
   _新しいデータ要素を作成_

1. **Name**&#x200B;を`sign out`に設定します。

1. **拡張機能**&#x200B;を`Adobe Experience Platform Web SDK`に設定します。

1. **データ要素タイプ**&#x200B;を`XDM object`に設定します。

1. 更新する&#x200B;**サンドボックス**&#x200B;と&#x200B;**スキーマ**&#x200B;を選択します。

1. **userAccount** > **logout**&#x200B;の下で、**訪問者ログアウト**&#x200B;の&#x200B;**value**&#x200B;を`1`に設定します。

   ![ ログアウト値の更新
   _ログアウト値の更新_

1. **保存**&#x200B;を選択します。

1. ルールを作成します。

   ![新しいルールを作成
   _新しいルールを作成_

1. **イベント**&#x200B;の下の&#x200B;**追加**&#x200B;を選択します。

1. **拡張機能**&#x200B;を`Adobe Client Data Layer`に設定します。

1. **イベントタイプ**&#x200B;を`Data Pushed`に設定します。

1. **特定のイベント**&#x200B;を選択し、**に登録する** イベント/キーを`sign-out`に設定します。

1. 新しいルールを保存するには、**変更を保持**&#x200B;を選択します。

1. アクションを追加します。

1. **拡張機能**&#x200B;を`Adobe Experience Platform Web SDK`に設定します。

1. **アクションタイプ**&#x200B;を`Send Event`に設定します。

1. **インスタンス**&#x200B;を`Alloy`に設定します。

1. **Type**&#x200B;を`userAccount.logout`に設定します。

1. **XDM データ**&#x200B;を`%sign out%`に設定します。

1. **保存**&#x200B;をクリックします。

   Adobe Commerceから`signOut` イベントのスキーマにデータ要素を作成しました。 また、そのイベントがAdobe Commerce ストアフロントから起動されたときに発生する特定のアクションを含むルールを作成しました。

以下で説明する各Adobe Commerce イベントのタグで、上記の手順を繰り返します。

## 利用可能なイベント

次の各イベントについて、上記の手順に従って、Adobe Commerce イベントをXDMにマッピングします。

- [`signOut`](#signout)
- [`signIn`](#signin)
- [`createAccount`](#createaccount)
- [`editAccount`](#editaccount)
- [`pageView`](#pageview)
- [`productView`](#productview)
- [`searchRequestSent`](#searchrequestsent)
- [`searchResponseReceived`](#searchresponsereceived)
- [`addToCart`](#addtocart)
- [`openCart`](#opencart)
- [`viewCart`](#viewcart)
- [`removeFromCart`](#removefromcart)
- [`initiateCheckout`](#initiatecheckout)
- [`placeOrder`](#placeorder)

### signOut

買い物客がログアウトしようとしたときにトリガーされます。

#### データ要素

次のデータ要素を作成します。

1. ログアウト：

   - **名前**: `Sign out`
   - **拡張機能**: `Adobe Experience Platform Web SDK`
   - **データ要素タイプ**: `XDM object`
   - **フィールドグループ**: `userAccount` > `logout`
   - **訪問者ログアウト**: **値** = `1`

#### ルール 

- **名前**: `Sign out`
- **拡張機能**: `Adobe Client Data Layer`
- **イベントタイプ**: `Data Pushed`
- **特定のイベント**: `sign-out`

##### アクション

- **拡張機能**: `Adobe Experience Platform Web SDK`
- **アクションの種類**: `Send event`
- **種類**: `userAccount.logout`
- **XDM データ**: `%sign-out%`

### signIn

買い物客がログインしようとしたときにトリガーされます。

#### データ要素

次のデータ要素を作成します。

1. アカウントメール：

   - **名前**: `account email`
   - **拡張機能**: `Adobe Client Data Layer`
   - **データ要素タイプ**: `Data Layer Computed State`
   - **[オプション ] パス**: `accountContext.emailAddress`

1. アカウントタイプ：

   - **名前**: `account type`
   - **拡張機能**: `Adobe Client Data Layer`
   - **データ要素タイプ**: `Data Layer Computed State`
   - **[オプション ] パス**: `accountContext.accountType`

1. アカウント ID:

   - **名前**: `account id`
   - **拡張機能**: `Adobe Client Data Layer`
   - **データ要素タイプ**: `Data Layer Computed State`
   - **[オプション ] パス***: `accountContext.accountId`

1. ログイン：

   - **名前**: `sign in`
   - **拡張機能**: `Adobe Experience Platform Web SDK`
   - **データ要素タイプ**: `XDM object`
   - **フィールドグループ**: `person` > `accountID`
   - **アカウント ID**: **値** = `%account id%`
   - **フィールドグループ**: `person` > `accountType`
   - **アカウントタイプ**: **値** = `%account type%`
   - **フィールドグループ**: `person` > `personalEmailID`
   - **個人用メールアドレス**: **値** = `%account email%`
   - **フィールドグループ**: `personalEmail` > `address`
   - **アドレス**: **値** = `%account email%`
   - **フィールドグループ**: `userAccount` > `login`
   - **訪問者ログイン**: **値** = `1`

#### ルール 

- **名前**: `sign in`
- **拡張機能**: `Adobe Client Data Layer`
- **イベントタイプ**: `Data Pushed`
- **特定のイベント**: `sign-in`

##### アクション

- **拡張機能**: `Adobe Experience Platform Web SDK`
- **アクションの種類**: `Send event`
- **種類**: `userAccount.login`
- **XDM データ**: `%sign in%`

### createAccount

買い物客がアカウントを作成しようとしたときにトリガーされます。

#### データ要素

次のデータ要素を作成します。

1. アカウントメール：

   - **名前**: `account email`
   - **拡張機能**: `Adobe Client Data Layer`
   - **データ要素タイプ**: `Data Layer Computed State`
   - **[オプション ] パス**: `accountContext.emailAddress`

1. アカウントタイプ：

   - **名前**: `account type`
   - **拡張機能**: `Adobe Client Data Layer`
   - **データ要素タイプ**: `Data Layer Computed State`
   - **[オプション ] パス**: `accountContext.accountType`

1. アカウント ID:

   - **名前**: `account id`
   - **拡張機能**: `Adobe Client Data Layer`
   - **データ要素タイプ**: `Data Layer Computed State`
   - **[オプション ] パス**: `accountContext.accountId`

1. アカウントを作成：

   - **名前**: `Create account`
   - **拡張機能**: `Adobe Experience Platform Web SDK`
   - **データ要素タイプ**: `XDM object`
   - **フィールドグループ**: `person` > `accountID`
   - **アカウント ID**: **値** = `%account id%`
   - **フィールドグループ**: `person` > `accountType`
   - **アカウントタイプ**: **値** = `%account type%`
   - **フィールドグループ**: `person` > `personalEmailID`
   - **個人用メールアドレス**: **値** = `%account email%`
   - **フィールドグループ**: `personalEmail` > `address`
   - **アドレス**: **値** = `%account email%`
   - **フィールドグループ**: `userAccount` > `createProfile`
   - **アカウントプロファイル作成**: **値** = `1`

#### ルール 

- **名前**: `Create account`
- **拡張機能**: `Adobe Client Data Layer`
- **イベントタイプ**: `Data Pushed`
- **特定のイベント**: `create-account`

##### アクション

- **拡張機能**: `Adobe Experience Platform Web SDK`
- **アクションの種類**: `Send event`
- **種類**: `userAccount.createProfile`
- **XDM データ**: `%create account%`

### editAccount

買い物客がアカウントを編集しようとしたときにトリガーされます。

#### データ要素

次のデータ要素を作成します。

1. アカウントメール：

   - **名前**: `account email`
   - **拡張機能**: `Adobe Client Data Layer`
   - **データ要素タイプ**: `Data Layer Computed State`
   - **[オプション ] パス**: `accountContext.emailAddress`

1. アカウントタイプ：

   - **名前**: `account type`
   - **拡張機能**: `Adobe Client Data Layer`
   - **データ要素タイプ**: `Data Layer Computed State`
   - **[オプション ] パス**: `accountContext.accountType`

1. アカウント ID:

   - **名前**: `account id`
   - **拡張機能**: `Adobe Client Data Layer`
   - **データ要素タイプ**: `Data Layer Computed State`
   - **[オプション ] パス**: `accountContext.accountId`

1. アカウントを編集：

   - **名前**: `Edit account`
   - **拡張機能**: `Adobe Experience Platform Web SDK`
   - **データ要素タイプ**: `XDM object`
   - **フィールドグループ**: `person` > `accountID`
   - **アカウント ID**: **値** = `%account id%`
   - **フィールドグループ**: `person` > `accountType`
   - **アカウントタイプ**: **値** = `%account type%`
   - **フィールドグループ**: `person` > `personalEmailID`
   - **個人用メールアドレス**: **値** = `%account email%`
   - **フィールドグループ**: `personalEmail` > `address`
   - **アドレス**: **値** = `%account email%`
   - **フィールドグループ**: `userAccount` > `updateProfile`
   - **アカウントプロファイル作成**: **値** = `1`

#### ルール

- **名前**: `Edit account`
- **拡張機能**: `Adobe Client Data Layer`
- **イベントタイプ**: `Data Pushed`
- **特定のイベント**: `edit-account`

##### アクション

- **拡張機能**: `Adobe Experience Platform Web SDK`
- **アクションの種類**: `Send event`
- **種類**: `userAccount.updateProfile`
- **XDM データ**: `%edit account%`

### pageView

ページが読み込まれたときにトリガーされます。

#### データ要素

次のデータ要素を作成します。

1. ページ名：

   - **名前**: `page name`
   - **拡張機能**: `Adobe Client Data Layer`
   - **データ要素タイプ**: `Data Layer Computed State`
   - **[オプション ] パス**: `pageContext.pageName`

#### ルール 

- **名前**: `page view`
- **拡張機能**: `Adobe Client Data Layer`
- **イベントタイプ**: `Data Pushed`
- **特定のイベント**: `page-view`

##### アクション

- **拡張機能**: `Adobe Experience Platform Web SDK`
- **アクションの種類**: `Send event`
- **種類**: `web.webPageDetails.pageViews`
- **XDM データ**: `%page view%`

### productView

商品ページが読み込まれたときにトリガーされます。

#### データ要素

次のデータ要素を作成します。

1. 製品名：

   - **名前**: `product name`
   - **拡張機能**: `Adobe Client Data Layer`
   - **データ要素タイプ**: `Data Layer Computed State`
   - **[オプション ] パス**: `productContext.name`

1. 製品SKU:

   - **名前**: `product sku`
   - **拡張機能**: `Adobe Client Data Layer`
   - **データ要素タイプ**: `Data Layer Computed State`
   - **[オプション ] パス**: `productContext.sku`

1. 製品画像URL:

   - **名前**: `product image`
   - **拡張機能**: `Adobe Client Data Layer`
   - **データ要素タイプ**: `Data Layer Computed State`
   - **[オプション ] パス**: `productContext.mainImageUrl`

1. 製品通貨：

   - **名前**: `product currency`
   - **拡張機能**: `Adobe Client Data Layer`
   - **データ要素タイプ**: `Data Layer Computed State`
   - **[オプション ] パス**: `productContext.pricing.currencyCode`

1. 通貨コード：

   - **名前**: `currency code`
   - **拡張機能**: `Core`
   - **データ要素タイプ**: `Custom Code`
   - **エディターを開く**:

   ```bash
   return _satellite.getVar('product currency') || _satellite.getVar('storefront').storeViewCurrencyCode
   ```

1. 特別価格：

   - **名前**: `special price`
   - **拡張機能**: `Adobe Client Data Layer`
   - **データ要素タイプ**: `Data Layer Computed State`
   - **[オプション ] パス**: `productContext.pricing.specialPrice`

1. 通常価格：

   - **名前**: `regular price`
   - **拡張機能**: `Adobe Client Data Layer`
   - **データ要素タイプ**: `Data Layer Computed State`
   - **[オプション ] パス**: `productContext.pricing.regularPrice`

1. 製品価格：

   - **名前**: `product price`
   - **拡張機能**: `Core`
   - **データ要素タイプ**: `Custom Code`
   - **エディターを開く**:

   ```bash
   return _satellite.getVar('product regular price') || _satellite.getVar('product special price')
   ```

1. 製品ビュー：

   - **名前**: `product view`
   - **拡張機能**: `Adobe Experience Platform Web SDK`
   - **データ要素タイプ**: `XDM object`
   - **フィールドグループ**: `productListItems`。 「**個別のアイテムを提供**」を選択し、「**アイテムを追加**」ボタンをクリックします。 このビューはPDP用なので、1つの項目を入力できます。
   - **フィールドグループ**: `productListItems` > `name`
   - **名前**: **値** = `%product name%`
   - **フィールドグループ**: `productListItems` > `SKU`
   - **SKU**: **値** = `%product sku%`
   - **フィールドグループ**: `productListItems` > `priceTotal`
   - **価格合計**: **値** = `%product price%`
   - **フィールドグループ**: `productListItems` > `currencyCode`
   - **通貨コード**: **値** = `%currency code%`
   - **フィールドグループ**: `productListItems` > `ProductImageUrl`
   - **ProductImageUrl**: **値** = `%product image%`
   - **フィールドグループ**: `commerce` > `productViews` > `value`
   - **値**: **値** = `1`

#### ルール 

- **名前**: `product view`
- **拡張機能**: `Adobe Client Data Layer`
- **イベントタイプ**: `Data Pushed`
- **特定のイベント**: `product-page-view`

##### アクション

- **拡張機能**: `Adobe Experience Platform Web SDK`
- **アクションの種類**: `Send event`
- **種類**: `commerce.productViews`
- **XDM データ**: `%product view%`

### searchRequestSent

「入力中の検索」ポップオーバーのイベントと検索結果ページのイベントによってトリガーされます。

#### データ要素

次のデータ要素を作成します。

1. 検索入力

   - **名前**: `search input`
   - **拡張機能**: `Adobe Client Data Layer`
   - **データ要素タイプ**: `Data Layer Computed State`
   - **[オプション ] パス**: `searchInputContext.units[0]`

1. 検索入力フレーズ

   - **名前**: `search input phrase`
   - **拡張機能**: `Core`
   - **データ要素タイプ**: `Custom Code`
   - **エディターを開く**:

   ```bash
   return _satellite.getVar('search input').phrase;
   ```

1. 検索入力並べ替え

   - **名前**: `search input sort`
   - **拡張機能**: `Core`
   - **データ要素タイプ**: `Custom Code`
   - **エディターを開く**:

   ```bash
   const searchInput = _satellite.getVar('search input');
   const sortFromInput = searchInput ? searchInput.sort : [];
   const sort = sortFromInput.map((searchSort) => {
       return {
           attribute: searchSort.attribute,
           order: searchSort.direction,
       };
   });
   return sort;
   ```

1. 入力フィルターを検索

   - **名前**: `search input filters`
   - **拡張機能**: `Core`
   - **データ要素タイプ**: `Custom Code`
   - **エディターを開く**:

   ```bash
   const searchInput = _satellite.getVar('search input');
   const filtersFromInput = searchInput ? searchInput.filter : [];
   const filters = filtersFromInput.map(
       (searchFilter) => {
           let value = [];
           let isRange = false;
           if (searchFilter.eq) {
               value.push(searchFilter.eq);
           } else if (searchFilter.in) {
               value = searchFilter.in;
           } else if (searchFilter.range) {
               isRange = true;
               value.push(String(searchFilter.range.from));
               value.push(String(searchFilter.range.to));
           }
           return {
               attribute: searchFilter.attribute,
               value,
               isRange,
           };
       }
   );
   
   return filters;
   ```

1. 検索リクエスト：

   - **名前**: `search request`
   - **拡張機能**: `Adobe Experience Platform Web SDK`
   - **データ要素タイプ**: `XDM object`
   - **フィールドグループ**: `siteSearch` > `phrase`
   - **value**：まだ利用できません
   - **フィールドグループ**: `siteSearch` > `sort`。 「**オブジェクト全体を指定**」を選択します。
   - **フィールドグループ**: `siteSearch` > `filter`。 「**オブジェクト全体を指定**」を選択します。
   - **フィールドグループ**: `searchRequest` > `id`
   - **一意の識別子**: **値** = `%search request ID%`
   - **フィールドグループ**: `searchRequest` > `value`
   - **値**: **値** = `1`

#### ルール 

- **名前**: `search request sent`
- **拡張機能**: `Adobe Client Data Layer`
- **イベントタイプ**: `Data Pushed`
- **特定のイベント**: `search-request-sent`

##### アクション

- **拡張機能**: `Adobe Experience Platform Web SDK`
- **アクションの種類**: `Send event`
- **種類**: `searchRequest`
- **XDM データ**: `%search request%`

### searchResponseReceived

ライブサーチが「入力中に検索」ポップオーバーまたは検索結果ページの結果を返したときにトリガーされます。

#### データ要素

次のデータ要素を作成します。

1. 検索結果：

   - **名前**: `search results`
   - **拡張機能**: `Adobe Client Data Layer`
   - **データ要素タイプ**: `Data Layer Computed State`
   - **[オプション ] パス**: `searchResultsContext.units[0]`

1. 商品の検索結果の数：

   - **名前**: `search result number of products`
   - **拡張機能**: `Core`
   - **データ要素タイプ**: `Custom Code`
   - **エディターを開く**:

   ```bash
   return _satellite.getVar('search result').products.length;
   ```

1. 検索結果の商品：

   - **名前**: `search result products`
   - **拡張機能**: `Core`
   - **データ要素タイプ**: `Custom Code`
   - **エディターを開く**:

   ```bash
   const searchResult = _satellite.getVar('search result');
   const productsFromResult = searchResult.products ? searchResult.products : [];
   const products = productsFromResult.map(
       (product) => {
           return { SKU: product.sku, name: product.name };
       }
   );
   return products;
   ```

1. 検索結果の候補：

   - **名前**: `search result products`
   - **拡張機能**: `Core`
   - **データ要素タイプ**: `Custom Code`
   - **エディターを開く**:

   ```bash
   const searchResult = _satellite.getVar('search result');
   const suggestionsFromResult = searchResult.suggestions ? searchResult.suggestions : [];
   const suggestions = suggestionsFromResult.map((suggestion) => suggestion.suggestion);
   return suggestions;
   ```

1. 製品画像URL:

   - **名前**: `product image`
   - **拡張機能**: `Adobe Client Data Layer`
   - **データ要素タイプ**: `Data Layer Computed State`
   - **[オプション ] パス**: `productContext.mainImageUrl`

1. 検索応答：

   - **名前**: `search response`
   - **拡張機能**: `Adobe Experience Platform Web SDK`
   - **データ要素タイプ**: `XDM object`
   - **フィールドグループ**: `siteSearch` > `suggestions`。 「**オブジェクト全体を指定**」を選択します。
   - **データ要素**: `%search result suggestions%`
   - **フィールドグループ**: `siteSearch` > `numberOfResults`
   - **値**: `%search result number of products%`
   - **フィールドグループ**: `productListItems`。 「**オブジェクト全体を指定**」を選択します。
   - **フィールドグループ**: `productListItems` > `ProductImageUrl`
   - **ProductImageUrl**: **値** = `%product image%`
   - **データ要素**: `%search result products%`
   - **フィールドグループ**: `searchResponse` > `id`
   - **一意の識別子**: **値** = `%search response ID%`
   - **フィールドグループ**: `searchResponse` > `value`
   - **値**: **値** = `1`

#### ルール 

- **名前**: `search response received`
- **拡張機能**: `Adobe Client Data Layer`
- **イベントタイプ**: `Data Pushed`
- **特定のイベント**: `search-response-received`

##### アクション

- **拡張機能**: `Adobe Experience Platform Web SDK`
- **アクションの種類**: `Send event`
- **種類**: `searchResponse`
- **XDM データ**: `%search response%`

### addToCart

商品がカートに追加されたとき、またはカート内の商品の数量が増えるたびにトリガーされます。

#### データ要素

次のデータ要素を作成します。

1. 製品名：

   - **名前**: `product name`
   - **拡張機能**: `Adobe Client Data Layer`
   - **データ要素タイプ**: `Data Layer Computed State`
   - **[オプション ] パス**: `productContext.name`

1. 製品sku:

   - **名前**: `product sku`
   - **拡張機能**: `Adobe Client Data Layer`
   - **データ要素タイプ**: `Data Layer Computed State`
   - **[オプション ] パス**: `productContext.sku`

1. 通貨コード：

   - **名前**: `currency code`
   - **拡張機能**: `Adobe Client Data Layer`
   - **データ要素タイプ**: `Data Layer Computed State`
   - **[オプション ] パス**: `productContext.pricing.currencyCode`

1. 製品特別価格：

   - **名前**: `product special price`
   - **拡張機能**: `Adobe Client Data Layer`
   - **データ要素タイプ**: `Data Layer Computed State`
   - **[オプション ] パス**: `productContext.pricing.specialPrice`

1. 製品画像URL:

   - **名前**: `product image`
   - **拡張機能**: `Adobe Client Data Layer`
   - **データ要素タイプ**: `Data Layer Computed State`
   - **[オプション ] パス**: `productContext.mainImageUrl`

1. 製品の正規価格：

   - **名前**: `product regular price`
   - **拡張機能**: `Adobe Client Data Layer`
   - **データ要素タイプ**: `Data Layer Computed State`
   - **[オプション ] パス**: `productContext.pricing.regularPrice`

1. 製品価格：

   - **名前**: `product price`
   - **拡張機能**: `Core`
   - **データ要素タイプ**: `Custom Code`
   - **エディターを開く**:

   ```bash
   return _satellite.getVar('product regular price') || _satellite.getVar('product special price') 
   ```

1. 買い物かご：

   - **名前**: `cart`
   - **拡張機能**: `Adobe Client Data Layer`
   - **データ要素タイプ**: `Data Layer Computed State`
   - **[オプション ] パス**: `shoppingCartContext`

1. カート ID:

   - **名前**: `cart id`
   - **拡張機能**: `Core`
   - **データ要素タイプ**: `Custom Code`
   - **エディターを開く**:

   ```bash
   return _satellite.getVar('cart').id
   ```

1. カートに追加：

   - **名前**: `add to cart`
   - **拡張機能**: `Adobe Experience Platform Web SDK`
   - **データ要素タイプ**: `XDM object`
   - **フィールドグループ**: `productListItems`。 「**個別のアイテムを提供**」を選択し、「**アイテムを追加**」ボタンをクリックします。 このビューはPDP用なので、1つの項目を入力できます。
   - **フィールドグループ**: `productListItems` > `name`
   - **名前**: **値** = `%product name%`
   - **フィールドグループ**: `productListItems` > `SKU`
   - **SKU**: **値** = `%product sku%`
   - **フィールドグループ**: `productListItems` > `priceTotal`
   - **価格合計**: **値** = `%product price%`
   - **フィールドグループ**: `productListItems` > `currencyCode`
   - **フィールドグループ**: `productListItems` > `ProductImageUrl`
   - **ProductImageUrl**: **値** = `%product image%`
   - **通貨コード**: **値** = `%currency code%`
   - **フィールドグループ**: `commerce` > `cart` > `cartID`
   - **買い物かごID**: **値** = `%cart id%`
   - **フィールドグループ**: `commerce` > `productListAdds` > `value`
   - **値**: **値** = `1`

#### ルール 

- **名前**: `add to cart`
- **拡張機能**: `Adobe Client Data Layer`
- **イベントタイプ**: `Data Pushed`
- **特定のイベント**: `add-to-cart`

##### アクション

- **拡張機能**: `Adobe Experience Platform Web SDK`
- **アクションの種類**: `Send event`
- **種類**: `commerce.productListAdds`
- **XDM データ**: `%add to cart%`

### openCart

商品が空のカートに追加されたときに発生する、新しいカートが作成されたときにトリガーされます。

#### データ要素

次のデータ要素を作成します。

1. 買い物かごを開く：

   - **名前**: `open cart`
   - **拡張機能**: `Adobe Experience Platform Web SDK`
   - **データ要素タイプ**: `XDM object`
   - **フィールドグループ**: `commerce` > `productListOpens` > `value`
   - **値**: **値** = `1`
   - **フィールドグループ**: `commerce` > `cart` > `cartID`
   - **買い物かごID**: **値** = `%cart id%`
   - **フィールドグループ**: `productListItems`。 `productListItems`の場合、複数の項目を事前に計算できます。 **productListItems** > **配列全体**&#x200B;を選択します。

#### ルール 

- **名前**: `open cart`
- **拡張機能**: `Adobe Client Data Layer`
- **イベントタイプ**: `Data Pushed`
- **特定のイベント**: `open-cart`

##### アクション

- **拡張機能**: `Adobe Experience Platform Web SDK`
- **アクションの種類**: `Send event`
- **種類**: `commerce.productListOpens`
- **XDM データ**: `%open cart%`

### viewCart

カートページが読み込まれたときにトリガーされます。

#### データ要素

次のデータ要素を作成します。

1. ストアフロント：

   - **名前**: `storefront`
   - **拡張機能**: `Adobe Client Data Layer`
   - **データ要素タイプ**: `Data Layer Computed State`
   - **[オプション ] パス**: `storefrontInstanceContext`

1. 製品画像URL:

   - **名前**: `product image`
   - **拡張機能**: `Adobe Client Data Layer`
   - **データ要素タイプ**: `Data Layer Computed State`
   - **[オプション ] パス**: `productContext.mainImageUrl`

   1. 買い物かご：

   - **名前**: `cart`
   - **拡張機能**: `Adobe Client Data Layer`
   - **データ要素タイプ**: `Data Layer Computed State`
   - **[オプション ] パス**: `shoppingCartContext`

1. カート ID:

   - **名前**: `cart id`
   - **拡張機能**: `Core`
   - **データ要素タイプ**: `Custom Code`
   - **エディターを開く**:

   ```bash
   return _satellite.getVar('cart').id
   ```

1. 製品リストの項目：

   - **名前**: `product list items:`
   - **拡張機能**: `Core`
   - **データ要素タイプ**: `Custom Code`
   - **エディターを開く**:

   ```bash
   const storefrontContext = _satellite.getVar('storefront');
   const cart = _satellite.getVar('cart');
   
   const returnList = [];
   cart.items.forEach(item => {
       const selectedOptions = [];
       item.configurableOptions?.forEach(option => {
           selectedOptions.push({
               attribute: option.optionLabel,
               value: option.valueLabel,
           });
       });
   
       const productListItem = {
           SKU: item.product.sku,
           name: item.product.name,
           quantity: item.quantity,
           priceTotal: item.prices.price.value * item.quantity,
           currencyCode: item.prices.price.currency ? item.prices.price.currency : storefrontContext.storeViewCurrencyCode,
           selectedOptions: selectedOptions,
       };
   
       returnList.push(productListItem);
   });
   return returnList;
   ```

1. カートの表示：

   - **名前**: `view cart`
   - **拡張機能**: `Adobe Experience Platform Web SDK`
   - **データ要素タイプ**: `XDM object`
   - **フィールドグループ**: `productListItems`。 `productListItems`の場合、事前に計算された複数の項目を指定できます。 **productListItems** > **配列全体を設定**&#x200B;を選択します。
   - **データ要素**: `%product list items%`
   - **フィールドグループ**: `productListItems` > `ProductImageUrl`
   - **ProductImageUrl**: **値** = `%product image%`
   - **フィールドグループ**: `commerce` > `cart` > `cartID`
   - **買い物かごID**: **値** = `%cart id%`
   - **フィールドグループ**: `commerce` > `productListViews` > `value`
   - **値**: **値** = `1`

#### ルール

- **名前**: `view cart`
- **拡張機能**: `Adobe Client Data Layer`
- **イベントタイプ**: `Data Pushed`
- **特定のイベント**: `shopping-cart-view`

##### アクション

- **拡張機能**: `Adobe Experience Platform Web SDK`
- **アクションの種類**: `Send event`
- **種類**: `commerce.productListViews`
- **XDM データ**: `%view cart%`

### removeFromCart

買い物かごから商品が取り除かれたとき、または買い物かごに入っている商品の数量が減るたびにトリガーされます。

#### データ要素

次のデータ要素を作成します。

1. 製品名：

   - **名前**: `product name`
   - **拡張機能**: `Adobe Client Data Layer`
   - **データ要素タイプ**: `Data Layer Computed State`
   - **[オプション ] パス**: `productContext.name`

1. 製品sku:

   - **名前**: `product sku`
   - **拡張機能**: `Adobe Client Data Layer`
   - **データ要素タイプ**: `Data Layer Computed State`
   - **[オプション ] パス**: `productContext.sku`

1. 通貨コード：

   - **名前**: `currency code`
   - **拡張機能**: `Adobe Client Data Layer`
   - **データ要素タイプ**: `Data Layer Computed State`
   - **[オプション ] パス**: `productContext.pricing.currencyCode`

1. 製品特別価格：

   - **名前**: `product special price`
   - **拡張機能**: `Adobe Client Data Layer`
   - **データ要素タイプ**: `Data Layer Computed State`
   - **[オプション ] パス**: `productContext.pricing.specialPrice`

1. 製品の正規価格：

   - **名前**: `product regular price`
   - **拡張機能**: `Adobe Client Data Layer`
   - **データ要素タイプ**: `Data Layer Computed State`
   - **[オプション ] パス**: `productContext.pricing.regularPrice`

1. 製品価格：

   - **名前**: `product price`
   - **拡張機能**: `Core`
   - **データ要素タイプ**: `Custom Code`
   - **エディターを開く**:

   ```bash
   return _satellite.getVar('product regular price') || _satellite.getVar('product special price') 
   ```

1. 買い物かご：

   - **名前**: `cart`
   - **拡張機能**: `Adobe Client Data Layer`
   - **データ要素タイプ**: `Data Layer Computed State`
   - **[オプション ] パス**: `shoppingCartContext`

1. カート ID:

   - **名前**: `cart id`
   - **拡張機能**: `Core`
   - **データ要素タイプ**: `Custom Code`
   - **エディターを開く**:

   ```bash
   return _satellite.getVar('cart').id
   ```

1. 買い物かごから削除：

   - **名前**: `remove from cart`
   - **拡張機能**: `Adobe Experience Platform Web SDK`
   - **データ要素タイプ**: `XDM object`
   - **フィールドグループ**: `productListItems`。 「**個別のアイテムを提供**」を選択し、「**アイテムを追加**」ボタンをクリックします。 このビューはPDP用なので、1つの項目を入力できます。
   - **フィールドグループ**: `productListItems` > `name`
   - **名前**: **値** = `%product name%`
   - **フィールドグループ**: `productListItems` > `SKU`
   - **SKU**: **値** = `%product sku%`
   - **フィールドグループ**: `productListItems` > `priceTotal`
   - **価格合計**: **値** = `%product price%`
   - **フィールドグループ**: `productListItems` > `currencyCode`
   - **通貨コード**: **値** = `%currency code%`
   - **フィールドグループ**: `commerce` > `cart` > `cartID`
   - **買い物かごID**: **値** = `%cart id%`
   - **フィールドグループ**: `commerce` > `productListRemovals` > `value`
   - **値**: **値** = `1`

#### ルール 

- **名前**: `remove from cart`
- **拡張機能**: `Adobe Client Data Layer`
- **イベントタイプ**: `Data Pushed`
- **特定のイベント**: `remove-from-cart`

##### アクション

- **拡張機能**: `Adobe Experience Platform Web SDK`
- **アクションの種類**: `Send event`
- **種類**: `commerce.productListRemovals`
- **XDM データ**: `%remove from cart%`

### initiateCheckout

買い物客がチェックアウトボタンをクリックしたときにトリガーされます。

#### データ要素

次のデータ要素を作成します。

1. ストアフロント：

   - **名前**: `storefront`
   - **拡張機能**: `Adobe Client Data Layer`
   - **データ要素タイプ**: `Data Layer Computed State`
   - **[オプション ] パス**: `storefrontInstanceContext`

1. 製品画像URL:

   - **名前**: `product image`
   - **拡張機能**: `Adobe Client Data Layer`
   - **データ要素タイプ**: `Data Layer Computed State`
   - **[オプション ] パス**: `productContext.mainImageUrl`

1. 買い物かご：

   - **名前**: `cart`
   - **拡張機能**: `Adobe Client Data Layer`
   - **データ要素タイプ**: `Data Layer Computed State`
   - **[オプション ] パス**: `shoppingCartContext`

1. カート ID:

   - **名前**: `cart id`
   - **拡張機能**: `Core`
   - **データ要素タイプ**: `Custom Code`
   - **エディターを開く**:

   ```bash
   return _satellite.getVar('cart').id
   ```

1. 製品リストの項目：

   - **名前**: `product list items`
   - **拡張機能**: `Core`
   - **データ要素タイプ**: `Custom Code`
   - **エディターを開く**:

   ```bash
   const storefrontContext = _satellite.getVar('storefront');
   const cart = _satellite.getVar('cart');
   
   const returnList = [];
   cart.items.forEach(item => {
       const selectedOptions = [];
       item.configurableOptions?.forEach(option => {
           selectedOptions.push({
               attribute: option.optionLabel,
               value: option.valueLabel,
           });
       });
   
       const productListItem = {
           SKU: item.product.sku,
           name: item.product.name,
           quantity: item.quantity,
           priceTotal: item.prices.price.value * item.quantity,
           currencyCode: item.prices.price.currency ? item.prices.price.currency : storefrontContext.storeViewCurrencyCode,
           selectedOptions: selectedOptions,
       };
   
       returnList.push(productListItem);
   });
   return returnList;
   ```

1. チェックアウトの開始：

   - **名前**: `initiate checkout`
   - **拡張機能**: `Adobe Experience Platform Web SDK`
   - **データ要素タイプ**: `XDM object`
   - **フィールドグループ**: `productListItems`。 `productListItems`の場合、事前に計算された複数の項目を指定できます。 **productListItems** > **配列全体を設定**&#x200B;を選択します。
   - **データ要素**: `%product list items%`
   - **フィールドグループ**: `productListItems` > `ProductImageUrl`
   - **ProductImageUrl**: **値** = `%product image%`
   - **フィールドグループ**: `commerce` > `cart` > `cartID`
   - **買い物かごID**: **値** = `%cart id%`
   - **フィールドグループ**: `commerce` > `checkouts` > `value`
   - **値**: **値** = `1`

#### ルール 

- **名前**: `initiate checkout`
- **拡張機能**: `Adobe Client Data Layer`
- **イベントタイプ**: `Data Pushed`
- **特定のイベント**: `initiate-checkout`

##### アクション

- **拡張機能**: `Adobe Experience Platform Web SDK`
- **アクションの種類**: `Send event`
- **種類**: `commerce.checkouts`
- **XDM データ**: `%initiate checkout%`

### placeOrder

顧客が注文したときにトリガーされます。

#### データ要素

次のデータ要素を作成します。

1. アカウントメール：

   - **名前**: `account email`
   - **拡張機能**: `Adobe Client Data Layer`
   - **データ要素タイプ**: `Data Layer Computed State`
   - **[オプション ] パス**: `accountContext.emailAddress`

1. ストアフロント：

   - **名前**: `storefront`
   - **拡張機能**: `Adobe Client Data Layer`
   - **データ要素タイプ**: `Data Layer Computed State`
   - **[オプション ] パス**: `storefrontInstanceContext`

1. 製品画像URL:

   - **名前**: `product image`
   - **拡張機能**: `Adobe Client Data Layer`
   - **データ要素タイプ**: `Data Layer Computed State`
   - **[オプション ] パス**: `productContext.mainImageUrl`

1. 買い物かご：

   - **名前**: `cart`
   - **拡張機能**: `Adobe Client Data Layer`
   - **データ要素タイプ**: `Data Layer Computed State`
   - **[オプション ] パス**: `shoppingCartContext`

1. カート ID:

   - **名前**: `cart id`
   - **拡張機能**: `Core`
   - **データ要素タイプ**: `Custom Code`
   - **エディターを開く**:

   ```bash
   return _satellite.getVar('cart').id
   ```

1. 注文：

   - **名前**: `order`
   - **拡張機能**: `Adobe Client Data Layer`
   - **データ要素タイプ**: `Data Layer Computed State`
   - **[オプション ] パス**: `orderContext`

1. Commerce注文：

   - **名前**: `commerce order`
   - **拡張機能**: `Core`
   - **データ要素タイプ**: `Custom Code`
   - **エディターを開く**:

   ```bash
   const order = _satellite.getVar('order');
   const storefront = _satellite.getVar('storefront');
   
   if (order.payments && order.payments.length) {
       payments = order.payments.map(payment => {
           return {
               paymentAmount: payment.total,
               paymentType: payment.paymentMethodCode,
               transactionID: order.orderId.toString(),
           };
       });
   } else {
       payments = [
           {
               paymentAmount: order.grandTotal,
               paymentType: order.paymentMethodCode,
               transactionID: order.orderId.toString(),
           },
       ];
   }
   
   return {
       purchaseID: order.orderId.toString(),
       currencyCode: storefront.storeViewCurrencyCode,
       payments,
   };
   ```

1. 注文配送：

   - **名前**: `order shipping`
   - **拡張機能**: `Core`
   - **データ要素タイプ**: `Custom Code`
   - **エディターを開く**:

   ```bash
   const order = _satellite.getVar('order');
   return {
       shippingMethod: order.shipping.shippingMethod,
       shippingAmount: order.shipping.shippingAmount || 0,
   }
   ```

1. プロモーション ID:

   - **名前**: `promotion id`
   - **拡張機能**: `Core`
   - **データ要素タイプ**: `Custom Code`
   - **エディターを開く**:

   ```bash
   return _satellite.getVar('order').appliedCouponCode
   ```

1. 製品リストの項目：

   - **名前**: `product list items`
   - **拡張機能**: `Core`
   - **データ要素タイプ**: `Custom Code`
   - **エディターを開く**:

   ```bash
   const storefrontContext = _satellite.getVar('storefront');
   const cart = _satellite.getVar('cart');
   
   const returnList = [];
   cart.items.forEach(item => {
       const selectedOptions = [];
       item.configurableOptions?.forEach(option => {
           selectedOptions.push({
               attribute: option.optionLabel,
               value: option.valueLabel,
           });
       });
   
       const productListItem = {
           SKU: item.product.sku,
           name: item.product.name,
           quantity: item.quantity,
           priceTotal: item.prices.price.value * item.quantity,
           currencyCode: item.prices.price.currency ? item.prices.price.currency : storefrontContext.storeViewCurrencyCode,
           selectedOptions: selectedOptions,
       };
   
       returnList.push(productListItem);
   });
   return returnList;
   ```

1. 注文する：

   - **名前**: `place order`
   - **拡張機能**: `Adobe Experience Platform Web SDK`
   - **データ要素タイプ**: `XDM object`
   - **フィールドグループ**: `productListItems`。 `productListItems`の場合、事前に計算された複数の項目を指定できます。 **productListItems** > **配列全体を設定**&#x200B;を選択します。
   - **データ要素**: `%product list items%`
   - **フィールドグループ**: `productListItems` > `ProductImageUrl`
   - **ProductImageUrl**: **値** = `%product image%`
   - **フィールドグループ**: `commerce` > `order`
   - **一意の識別子**: **値** = `%commerce order%`
   - **フィールドグループ**: `commerce` > `shipping`
   - **一意の識別子**: **値** = `%order shipping%`
   - **フィールドグループ**: `commerce` > `promotionID`
   - **プロモーション ID**: **値** = `%promotion id%`
   - **フィールドグループ**: `commerce` > `purchases` > `value`
   - **値**: **値** = `1`
   - **個人用メールアドレス**: **値** = `%account email%`
   - **フィールドグループ**: `personalEmail` > `address`
   - **アドレス**: **値** = `%account email%`

#### ルール 

- **名前**: `place order`
- **拡張機能**: `Adobe Client Data Layer`
- **イベントタイプ**: `Data Pushed`
- **特定のイベント**: `place-order`

##### アクション

- **拡張機能**: `Adobe Experience Platform Web SDK`
- **アクションの種類**: `Send event`
- **種類**: `commerce.order`
- **XDM データ**: `%place order%`

## ストアフロントイベントでのID設定

ストアフロントイベントには、`personalEmail` （アカウントイベントの場合）および`identityMap` （その他のすべてのストアフロントイベントの場合）フィールドに基づくプロファイル情報が含まれます。 [!DNL Data Connection]拡張機能は、これら2つのフィールドに基づいてプロファイルを結合して生成します。 ただし、各フィールドには、プロファイルを作成するための様々な手順があります。

>[!NOTE]
>
>異なるフィールドに依存する以前の設定がある場合は、引き続きこれらのフィールドを使用できます。

- `personalEmail` - アカウントイベントにのみ適用されます。 [上記](#createaccount)の手順、ルール、アクションに従います
- `identityMap` – 他のすべてのストアフロントイベントに適用されます。 次の例を参照してください。

### 例

次の手順は、[!DNL Data Connection]拡張機能で`identityMap`を使用して`pageView` イベントを設定する方法を示しています。

1. ECIDのカスタムコードを使用したデータ要素の設定：

   ![ カスタムコードでデータ要素を設定
   _カスタムコードを使用したデータ要素の設定_

1. [!UICONTROL Open Editor]を選択し、次のカスタムコードを追加します。

   ```javascript
   return alloy("getIdentity").then((result) => {
       var identityMap = {
           ECID: [
           {
               id: ecid,
               primary: true
           }
           ],
           email: [
           {
               id: email,
               primary: false
           }
           ]
       };
     _satelite.setVar("identityMap", identityMap);
   });
   ```

1. `identityMap`をECIDとして設定してXDM スキーマを更新します：

   ![IDMapをECIDとして設定
   _IDMapをECID_&#x200B;として設定

1. ECIDを取得するルールアクションを定義します。

   ![ECIDの取得
   _ECIDを取得_

## バックオフィスイベントでIDを設定する

ECIDを使用してプロファイル情報をIDおよびリンクするストアフロントイベントとは異なり、バックオフィスのイベントデータはSaaS ベースであるため、ECIDは利用できません。 バックオフィスイベントの場合は、買い物客を特定するために電子メールを利用する必要があります。 この節では、バックオフィスのイベントデータをメールを使用してECIDにリンクする方法について説明します。

1. ID マップ要素を作成します。

   ![ バックオフィス ID マップ
   _バックオフィス ID マップの作成_

1. [!UICONTROL Open Editor]を選択し、次のカスタムコードを追加します。

```javascript
const IdentityMap = {
  "ECID": [
    {
      id:  _satellite.getVar('ECID'),
      primary: true,
    },
  ],
};
 
if (_satellite.getVar('account email')) {
    IdentityMap.email = [
        {
            id: _satellite.getVar('account email'),
            primary: false,
        },
    ];
}
return IdentityMap;
```

1. この新しい要素を各`identityMap` フィールドに追加します。

   ![各IDMapを更新
   _各ID マップを更新_

## 同意の設定

Adobe Commerceに[!DNL Data Connection]拡張機能をインストールすると、データ収集の同意がデフォルトで有効になります。 オプトアウトは[`mg_dnt` Cookie](https://experienceleague.adobe.com/docs/commerce-admin/start/compliance/privacy/compliance-cookie-law.html)を通じて管理されます。 `mg_dnt`を使用して同意を管理することを選択した場合は、ここに記載されている手順に従ってください。 [Adobe Experience Platform Web SDK ドキュメント ](https://experienceleague.adobe.com/docs/experience-platform/edge/consent/supporting-consent.html)には、同意管理に関するオプションが追加されています。

1. `mg_dnt` Cookieの&#x200B;**コアカスタムコード** データ要素（`%do not track cookie%`）を作成します。

   ![作成はデータ要素を追跡しません
   _作成がデータ要素を追跡しません_

1. Cookieが設定されている場合は`out`を返し、それ以外の場合は`in`を返す&#x200B;**コアカスタムコード** データ要素（`%consent%`）を作成します。

   ![同意データ要素の作成
   _同意データ要素の作成_

1. Adobe Experience Platform Web SDK拡張機能を`%consent%` データ要素で設定します。

   ![同意を得てSDKを更新する
   _同意を得てSDKを更新_

## 警告

- Experience Platform コレクションをオフにする手順に従わないと、イベントが二重カウントされます
- このトピックで説明したようにマッピングやイベントを設定しないと、Adobe Analytics ボードに影響を与える可能性があります
- データ収集が無効になっている場合は、[!DNL Data Connection]拡張機能を使用してTargetを設定できません
