---
title: SaaS データ書き出しフィードデータの拡張とカスタマイズ
description: ' [!DNL SaaS Data Export]  フィード データを拡張してカスタマイズする方法について説明します。'
role: Admin, Developer
exl-id: 694bd281-12c5-415c-a251-b4251e2edea7
TQID: https://experienceleague.adobe.com/T71zNl7WOrqzEsz4H8A8arx--q6w1B0h33CF2Q0VI4A
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
source-git-commit: 33cd0e217447351b690646ec8d230f76060a74da
workflow-type: tm+mt
source-wordcount: 542
ht-degree: 0%

---

# SaaS データ書き出しフィードデータの拡張とカスタマイズ

[!DNL Commerce Data Export]拡張機能を使用すると、[!DNL Commerce] アプリケーションから、ライブサーチ、カタログサービス、商品レコメンデーションなどのCommerce サービスにデータを書き出すことができます。 必要であれば、フィードデータを拡張してカスタマイズし、属性データを追加したり、収集したデータを変更したりできます。

属性データを追加すると、ストアフロントサービスのGraphQL スキーマの[属性フィールド &#x200B;](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/products/#productviewattribute-type)からアクセスできるようになります。

>[!NOTE]
>
>フィードデータを追加または変更すると、Commerce バックエンドのパフォーマンスと処理ロジックに影響を与える可能性があります。 本番環境にマージする前に、カスタマイズしたコードをテストします。 バックエンドにデータを追加する代わりに、API メッシュを使用してCatalog Service GraphQL スキーマを拡張します。 設定の詳細については、[&#x200B; カタログサービスとAPI メッシュ &#x200B;](../catalog-service/mesh.md)を参照してください。

## 製品フィードのシステム属性データの拡張

製品フィードには、製品処理に必要な、または消費者が一般的に使用するデフォルトのシステム属性が含まれています。 製品フィードに追加することで、製品フィードに追加のシステム属性を含めることができます。

このタスクを完了するには、`magento/catalog-data-exporter` モジュールを更新して、[依存関係インジェクション設定ファイル &#x200B;](https://developer.adobe.com/commerce/php/development/build/dependency-injection-file/) （`di.xml`）に追加のシステム属性を追加します。

製品属性クエリ（`Magento\CatalogDataExporter\Model\Query\ProductAttributeQuery`）に属性を追加します。

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

## Adobe Commerceへの商品属性の追加

開発者は、次のいずれかの方法を使用して、[製品属性フィールド &#x200B;](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/products/#output-fields)からアクセスできる製品属性を追加できます。

- Commerce ストアフロントサービスに書き出された`products` フィードデータに含める属性をAdobe Commerceに追加します。
- プラグインを使用して、フィード同期プロセス中に属性を動的に追加します。

### Adobe Commerceへの属性の追加

Commerce Adminからproduct属性を追加するか、カスタム PHP モジュールを使用してプログラムで属性を定義し、Adobe Commerceを更新できます。 Commerce管理者から属性を追加すると、属性と必要なすべてのメタデータを一度に追加できるため、最も簡単な方法です。 新しい属性とそのメタデータプロパティは、次にスケジュールされた同期中に、自動的にSaaS サービスに書き出されます。

#### 管理者から製品属性を作成します

1. Commerce管理者から、製品属性設定ページ（[!UICONTROL Stores] > *[!UICONTROL Attributes]* > [!UICONTROL Product]）から属性を作成します。

1. 必要に応じて、属性を属性セットに追加します。

*Adobe Commerce管理ガイド*&#x200B;の「[製品属性を作成](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/product-attributes/create/attribute-product-create)」を参照してください。

#### プログラムによる製品属性の作成

`DataPatchInterface`を実装するデータパッチを作成して、プログラムで製品属性を追加し、コンストラクター内の`EavSetup Factory` クラスのコピーをインスタンス化して、属性オプションを設定します。

属性オプションを定義する場合、`type`、`label`および`input`を除くすべての属性パラメーターはオプションです。 次の追加パラメーターと、デフォルト設定と異なるその他のパラメーターを定義します。

- **`user_defined`=`1`** - データ同期中にストアフロントサービスに属性をエクスポートします
- **`used_in_product_listing`=`1`** – 製品リスト データベース クエリ内で属性にアクセスできるようにします

データパッチの作成について詳しくは、*PHP開発者ガイド*&#x200B;の[&#x200B; データおよびスキーマパッチの開発](https://developer.adobe.com/commerce/php/development/components/declarative-schema/patches/)を参照してください。

### product属性を動的に追加します

新しいEAV属性を導入せずに製品属性を動的に作成する方法について詳しくは、[属性を動的に追加](add-attribute-dynamically.md)を参照してください。
