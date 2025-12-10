---
title: '[!DNL Storefront Popover]'
description: は  [!DNL Live Search storefront popover]  推奨される製品とサムネールを動的に返します。
exl-id: 240a5333-15e9-4178-ba3c-ae6c62c2238c
source-git-commit: c6725fc524e9d239ccc0f16701e92ad5d2fc7729
workflow-type: tm+mt
source-wordcount: '415'
ht-degree: 0%

---

# [!DNL Storefront Popover]

[!DNL Live Search] が [ インストール済み ](install.md) になると、買い物客が [!DNL popover] 検索 [ ボックスに入力したときに ](https://experienceleague.adobe.com/docs/commerce-admin/catalog/catalog/search/search.html#quick-search) がストアフロントに表示されます。 各文字を入力すると、検索結果の候補となる製品やサムネール画像が [!DNL popover] に表示されます。

[!DNL Live Search] は、2 文字以上のクエリの結果を返します。 部分一致の場合、1 単語あたりの最大文字数は 20 文字です。 「入力中の検索」クエリの文字数は設定できません。

![[!DNL Live Search popover]](assets/storefront-search-as-you-type.png)

>[!TIP]
>
>製品属性を検索可能として設定する方法については、「[Live Search の設定 ](workspace.md) 記事を参照してください。

## [!DNL Popover] ページサイズ

[!DNL popover] ージのページサイズによって、オートコンプリートされた商品を返せるライン数が決まります。 Live Search のインストール中、`page_size` の値は [ カタログ検索 ](https://experienceleague.adobe.com/docs/commerce-admin/config/catalog/catalog.html) - `Autocomplete Limit` 設定の現在の値に変更されます。

デフォルトでは、「カタログ検索 – オートコンプリートの制限」の値は 8 行（1 行）に設定されています。 [!DNL popover] ージのページサイズを変更するには、次の手順を実行します。

1. *管理者* サイドバーで、**ストア**/設定/**設定** に移動します。
1. 左側のパネルで、「**カタログ**」を展開し、設定のリストから **カタログ** を選択します。
1. 「*カタログ検索*」セクションを展開します。
1. 「**オートコンプリート制限**」を、[!DNL popover] ージで許可する行数に設定します。
1. 完了したら、「**設定を保存**」をクリックします。

## スタイル設定 [!DNL Popover] 例

[!DNL Popover] ウィジェットのルックアンドフィールは、会社のスタイルやブランディングガイドラインに合わせてカスタマイズできます。

[!DNL storefront popover] には常に製品 `name` と `price` が表示され、フィールドの選択は設定できません。 ただし、[!DNL popover] 要素は [CSS](https://developer.adobe.com/commerce/frontend-core/guide/css/) クラスを使用してスタイルを設定できます。 例えば、次の宣言は、[!DNL popover] のコンテナとフッターの背景色を変更します。

```css
.livesearch.popover-container {
    background-color: lavender;
}

.livesearch.view-all-footer {
    background-color: magenta;
}
```

## コンテナの表示

`.livesearch.popover-container` の親コンポーネントは `.search-autocomplete` です。  `.active` クラスは、コンテナの表示を示します。 `.active` クラスは、[!DNL popover] が開いている場合に条件付きで追加されます。

```css
.search-autocomplete.active   /* visible */
.search-autocomplete          /* not visible */
```

ストアフロント要素のスタイル設定について詳しくは、『 [ フロントエンド開発者ガイド ](https://developer.adobe.com/commerce/frontend-core/guide/css/) のカスケーディングスタイルシート（CSS） [ を参照してください ](https://developer.adobe.com/commerce/frontend-core/guide/)。

## クラスセレクター

次のクラスセレクターを使用して、コンテ [!DNL popover] 内のコンテナおよび製品要素のスタイルを設定できます。

- `.livesearch.popover-container`
- `.livesearch.view-all-footer`
- `.livesearch.products-container`
- `.livesearch.product-result`
- `.livesearch.product-name`
- `.livesearch.product-price`

### コンテナクラスセレクター

#### .livesearch.popover-container

![[!DNL Popover] コンテナ ](assets/livesearch-popover-container.png)

#### .livesearch.view-all-footer

![ すべてのフッターを表示 ](assets/livesearch-view-all-footer.png)

### 製品クラスセレクター

#### .livesearch.products-container

![ 製品コンテナ ](assets/livesearch-product-container.png)

#### .livesearch.product-result

![ 製品結果 ](assets/livesearch-product-result.png)

#### .livesearch.product-name

![ 製品名 ](assets/livesearch-product-name.png)

#### .livesearch.product-price

![ 製品価格 ](assets/livesearch-product-price.png)

#### .livesearch product-link

![ 製品結果 ](assets/livesearch-product-link.png)

## 変更したテーマの操作 {#working-with-modified-theme}

カスタマイズした [!DNL storefront popover] テーマ [ で ](https://developer.adobe.com/commerce/frontend-core/guide/themes/) を使用し、必要なファイルを *Luma* から継承することができます。 `top.search` モジュールの `header-wrapper` の `Magento_Search` ブロックは変更できません。

```html
<referenceContainer name="header-wrapper">
   <block class="Magento\Framework\View\Element\Template" name="top.search" as="topSearch" template="Magento_Search::form.mini.phtml">
      <arguments>
         <argument name="configProvider" xsi:type="object">Magento\Search\ViewModel\ConfigProvider</argument>
      </arguments>
   </block>
</referenceContainer>
```

## [!DNL popover] の無効化

[!DNL popover] を無効にして標準の [ クイック検索 ](https://experienceleague.adobe.com/docs/commerce-admin/catalog/catalog/search/search.html#quick-search) 機能を復元するには、次のコマンドを入力します。

```bash
bin/magento module:disable Magento_LiveSearchStorefrontPopover
```

## ヘッドレス実装

ヘッドレス実装を使用するユーザーの場合は、[!DNL Live Search popover]npm パッケージ [ を使用して ](https://www.npmjs.com/package/@magento/ds-livesearch-storefront-utils) をインストールできます。
