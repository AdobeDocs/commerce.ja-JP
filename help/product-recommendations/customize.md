---
title: Customize
description: 製品レコメンデーションをカスタマイズする方法を説明します。
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 0%

---

# Customize

Product Recommendations モジュールをインストールすると、Adobe Commerceによって `ProductRecommendationsLayout` ディレクトリが作成されます。 このディレクトリには、ストアフロントでのレコメンデーションの表示方法を変更するためにカスタマイズできるテンプレートファイルが含まれています。 特に、次のテンプレートを変更または上書きできます。

`<your theme>/Magento_ProductRecommendationsLayout/web/template/recommendations.html`

テンプレートファイルの変更について詳しくは、フロントエンド開発者ガイドの [ テンプレートのカスタマイズ ](https://developer.adobe.com/commerce/frontend-core/guide/templates/walkthrough/) を参照してください。

`recommendations.html` ファイルを変更する場合、Adobe Commerceがストアフロントからレコメンデーション指標を収集できるように、ファイルに次のタグを保持する必要があります。

| タグ | 使用方法 |
|---|---|
| `<div data-bind="attr : {'data-unit-id' : unitId }"...</div>` | ビューイベントを収集します。 |
| `<a data-bind="attr : {'data-sku' : sku, 'data-unit-id'}"...</a>` | クリックイベントを収集します。 <br/>**メモ：** アンカータグを追加する場合は、これらの属性を含める必要があります。 |

`recommendations.html` ファイルに加えて、`ProductRecommendationsLayout` ディレクトリには次のサブディレクトリが含まれています。

| ディレクトリ | 目的 |
|---|---|
| `layout` | 各ページタイプの `*.xml` ファイルが含まれます |
| `templates` | fetch スクリプトと render スクリプトを呼び出すファイルが含まれます |
| `web/js` | ストアのレコメンデーションを取得およびレンダリングするJavaScript ファイルが含まれます |
| `web/template` | `magento/product-recommendations` モジュールのテンプレートが含まれます |

## レコメンデーションユニットの配置

レコメンデーションを [ 作成 ](create.md) する際には、ページ上に表示される [ 場所 ](placement.md) を指定します。 レコメンデーションユニットは、メインコンテンツコンテナの上部または下部に配置できます。 ただし、このプレースメントをカスタマイズすることはできます。 ページビルダーのレコメンデーションコンテンツタイプを作成する場合は、ページビルダーツールを使用して、ページ上にレコメンデーション単位を配置します。 その他のすべてのページタイプについては、レコメンデーションの作成時に生成される `*.xml` ファイルを編集します。

1. `layout` ディレクトリに移動します。

   ```bash
   cd `<your theme>/Magento_ProductRecommendationsLayout/layout`
   ```

   次の表に、このディレクトリに存在する XML ファイルを示します。

   | ファイル名 | ページ |
   |---|---|
   | `catalog_category_view.xml` | カテゴリ |
   | `catalog_product_view.xml` | 製品の詳細 |
   | `checkout_cart_index.xml` | カート |
   | `checkout_onepage_success.xml` | チェックアウト |
   | `cms_index_index.xml` | ホーム |

   >[!NOTE]
   >
   >ストアでサードパーティの拡張機能を使用している場合、`layout` ディレクトリのファイル名が異なる可能性があります。

1. レコメンデーションユニットが製品の詳細ページの製品画像の後に表示されるように、`catalog_product_view.xml` ファイルを変更します。 この XML ファイルをカスタマイズする前に、ファイルを確認し、変更する必要があるセクションを理解してください。

   ```xml
   <?xml version="1.0"?>
   <page xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:framework:View/Layout/etc/page_configuration.xsd">
       <referenceBlock name="page.wrapper">
           <block class="Magento\Framework\View\Element\Template" before="-" name="product_recommendations_fetcher" template="Magento_ProductRecommendationsStorefront::fetcher.phtml" />
       </referenceBlock>
       <body>
           <referenceBlock name="main.content">
               <block class="Magento\ProductRecommendationsStorefront\Block\Renderer" after="-" name="product_recommendations_product_below_content" template="Magento_ProductRecommendationsStorefront::renderer.phtml">
                   <arguments>
                       <argument name="pagePlacement" xsi:type="string">below-main-content</argument>
                   </arguments>
               </block>
           </referenceBlock>
       </body>
   </page>
   ```

   上記のスニペットでは、`main.content` 参照ブロックは、レコメンデーションユニットがその要素に関連する場所に配置されることを示しています。 `block` 要素には `after="-"` 属性が含まれます。この属性は、レコメンデーションユニットがメインコンテンツブロックの後のページに表示されることを指定します。

1. 別のコンテンツブロックを指定して、このファイルを変更します。

   参照ブロック `name` を `main.content` から `product.info.media` に変更します。

   ```xml
   <?xml version="1.0"?>
   <page xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:framework:View/Layout/etc/page_configuration.xsd">
       <referenceBlock name="page.wrapper">
           <block class="Magento\Framework\View\Element\Template" before="-" name="product_recommendations_fetcher" template="Magento_ProductRecommendationsStorefront::fetcher.phtml" />
       </referenceBlock>
       <body>
           <referenceBlock name="product.info.media">
               <block class="Magento\ProductRecommendationsStorefront\Block\Renderer" after="-" name="product_recommendations_product_below_content" template="Magento_ProductRecommendationsStorefront::renderer.phtml">
                   <arguments>
                       <argument name="pagePlacement" xsi:type="string">below-main-content</argument>
                   </arguments>
               </block>
           </referenceBlock>
       </body>
   </page>
   ```

   この変更により、レコメンデーションユニットが製品の詳細ページの製品画像の後に表示されます。 レコメンデーションユニットを `product.info.media` の前に表示する場合は、`after="-"` 属性を `before="-"` に変更します。 `pagePlacement` 引数は内部引数であり、変更しないでください。

ページ上のブロックのタイプについて詳しくは、[ レイアウトの概要 ](https://developer.adobe.com/commerce/frontend-core/guide/layouts/) を参照してください。

## カスタム製品属性

開発者は、多くの場合、ストアフロントの Recommendations 単位のカスタム製品属性値にアクセスして、それらの属性に基づいて製品に視覚的処理を追加する必要があります。

例えば、店舗で一部のオーガニック製品を販売している場合、それらの製品を `Organic = Yes` として指定するカスタム属性がある可能性があります。 これらの製品が Recommendations に表示された際に特別な視覚的処理を提供できるように、ストアフロントでこの属性値にアクセスする必要がある場合があります。 同様に、これらのカスタム製品属性値にアクセスすると、製品のバッジを付けたり、サイトのプレゼンテーションレイヤーでカスタムロジックを推進したりできます。

![ バッジを追加 ](assets/unit-custom.png)

ページでレコメンデーションユニットをレンダリングする際に、カスタムの製品属性が使用可能であることを確認するには、管理者の [ 製品属性 ](https://experienceleague.adobe.com/docs/commerce-admin/catalog/product-attributes/create/attribute-product-create.html) ページで `Used in Product Listing` プロパティを `Yes` に設定します。

このプロパティを設定すると、JSON ペイロードには、属性コードと値の配列を含む `attributes` オブジェクトが含まれます。 その後、これらの属性値に基づいて、カスタムストアフロントのスタイル設定を適用できます（前述のように特別なビジュアル処理やバッジの追加など）。

>[!NOTE]
>
>製品属性の変更が JSON ペイロードに表示されるまでに最大 1 時間かかる場合があります。
