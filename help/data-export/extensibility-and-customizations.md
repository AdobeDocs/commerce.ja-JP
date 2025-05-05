---
title: SaaS データ書き出しフィードデータの拡張とカスタマイズ
description: フィードデータを拡張してカスタマイズする方法  [!DNL SaaS Data Export]  説明します。
role: Admin, Developer
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 0%

---

# SaaS データ書き出しフィードデータの拡張とカスタマイズ

[!DNL Commerce Data Export] 拡張機能を使用すると、[!DNL Commerce] アプリケーションからCommerce サービス（Live Search、カタログサービス、Product Recommendations など）にデータを書き出すことができます。 必要に応じて、フィードデータを拡張およびカスタマイズして追加の属性データを含めたり、収集したデータを変更したりできます。

属性データを追加した後、ストアフロントサービスのGraphQL スキーマの [ 属性 ](https://developer.adobe.com/commerce/services/graphql/catalog-service/products/#productviewattribute-type) フィールドからアクセスできます。

>[!NOTE]
>
>フィードデータを追加または変更すると、Commerce バックエンドのパフォーマンスと処理ロジックに影響を与える可能性があります。 実稼動環境に結合する前に、カスタマイズされたコードをテストします。 バックエンドにデータを追加する代わりに、API メッシュを使用してカタログサービスのGraphQL スキーマを拡張します。 設定について詳しくは、[ カタログサービスと API メッシュ ](../catalog-service/mesh.md) を参照してください。

## 製品フィードでのシステム属性データの拡張

製品フィードには、製品の処理に必要な、または消費者によって一般的に使用されるデフォルトのシステム属性が含まれています。 製品フィードに追加することで、製品フィードに追加のシステム属性を含めることができます。

このタスクを完了するには、`magento/catalog-data-exporter` モジュールを更新して、追加のシステム属性を [ 依存関係インジェクション設定ファイル ](https://developer.adobe.com/commerce/php/development/build/dependency-injection-file/) （`di.xml`）に追加します。

製品属性クエリに属性 `Magento\CatalogDataExporter\Model\Query\ProductAttributeQuery` 追加します。

**例**

```xml
    <type name="Magento\CatalogDataExporter\Model\Query\ProductAttributeQuery">
        <arguments>
            <argument name="systemAttributes" xsi:type="array">
                <item name="news_from_date" xsi:type="string">news_from_date</item>
                ...
                <item name="some_system_attribute_code">some_system_attribute_code</item>
            </argument>
        </arguments>
    </type>
```

## Adobe Commerceへの製品属性の追加

開発者は、次のいずれかの方法を使用して、[ 製品属性フィールド ](https://developer.adobe.com/commerce/services/graphql/catalog-service/products/#output-fields) からアクセスできる製品属性を追加できます。

- Adobe Commerce ストアフロントサービスに書き出した `products` フィードデータに含めるために、Commerceに属性を追加します。
- プラグインを使用したフィード同期プロセス中に、属性を動的に追加します。

### Adobe Commerceへの属性の追加

product 属性は、Commerce管理者から、またはカスタム PHP モジュールを使用してプログラムで追加し、属性を定義してAdobe Commerceを更新することができます。 製品属性を追加する場合は、属性と必要なメタデータをすべて追加できるので、これは最も簡単な方法です。 新しい属性とそのメタデータ プロパティは、次にスケジュールされた同期中に SaaS サービスに自動的にエクスポートされます。

#### 管理者からの製品属性の作成

1. Commerce管理者で、製品属性設定ページ（[!UICONTROL Stores]/*[!UICONTROL Attributes]*/[!UICONTROL Product]）から属性を作成します。

1. 必要に応じて、属性を属性セットに追加します。

[2&rbrace;Adobe Commerce管理ガイド ](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/product-attributes/create/attribute-product-create) 製品属性の作成 *を参照してください。*

#### プログラムによる製品属性の作成

`DataPatchInterface` を実装するデータパッチを作成してプログラムで製品属性を追加し、コンストラクター内で `EavSetup Factory` クラスのコピーをインスタンス化して、属性オプションを設定します。

属性オプションを定義する場合、`type`、`label`、`input` を除くすべての属性パラメーターはオプションです。 次の追加オプションや、デフォルト設定とは異なるその他のオプションを定義します。

- プロパティを `user_defined` = `1` に設定して、データ同期中にストアフロントサービスに書き出すようにします。
- 製品リストのデータベースクエリ内で属性に確実にアクセスできるようにするには、`used_in_product_listing` = `1` を設定します。

データパッチの作成については、『 *PHP 開発者ガイド* の [ データおよびスキーマパッチの開発 ](https://developer.adobe.com/commerce/php/development/components/declarative-schema/patches/) を参照してください。

### 製品属性の動的な追加

新しい Eav 属性を導入せずに製品属性を動的に作成する方法について詳しくは、[ 属性の動的な追加 ](add-attribute-dynamically.md) を参照してください。
