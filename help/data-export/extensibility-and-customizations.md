---
title: SaaS データ書き出しフィードデータの拡張とカスタマイズ
description: ' [!DNL SaaS Data Export]  フィード データを拡張してカスタマイズする方法について説明します。'
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
exl-id: 694bd281-12c5-415c-a251-b4251e2edea7
TQID: https://experienceleague.adobe.com/T71zNl7WOrqzEsz4H8A8arx--q6w1B0h33CF2Q0VI4A
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047id: b974b164-8a4e-43b8-a9e2-8e67ec131677id: cdf0c6dd-1717-4e20-9530-a24eee57088bid: de2e2e68-c5d7-4efe-be7b-27528698f06b
feature_v2: id: d1e21356-0064-4f48-9089-16e3f0dbd2a6id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
source-git-commit: 182aa9ce819807d1ede85c4fa459714e7dfe0478
workflow-type: tm+mt
source-wordcount: 815
ht-degree: 0%

---

# SaaS データ書き出しフィードデータの拡張とカスタマイズ

[!DNL Commerce Data Export]拡張機能を使用すると、[!DNL Commerce] アプリケーションから、ライブサーチ、カタログサービス、商品レコメンデーションなどのCommerce サービスにデータを書き出すことができます。 必要であれば、フィードデータを拡張してカスタマイズし、属性データを追加したり、収集したデータを変更したりできます。

属性データを追加すると、ストアフロントサービスのGraphQL スキーマの[属性フィールド ](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/products/#productviewattribute-type)からアクセスできるようになります。

>[!NOTE]
>
>フィードデータを追加または変更すると、Commerce バックエンドのパフォーマンスと処理ロジックに影響を与える可能性があります。 本番環境にマージする前に、カスタマイズしたコードをテストします。 バックエンドにデータを追加する代わりに、API メッシュを使用してCatalog Service GraphQL スキーマを拡張します。 設定の詳細については、[ カタログサービスとAPI メッシュ ](../catalog-service/mesh.md)を参照してください。

## 製品フィードのシステム属性データの拡張

製品フィードには、製品処理に必要な、または消費者が一般的に使用するデフォルトのシステム属性が含まれています。 製品フィードに追加することで、製品フィードに追加のシステム属性を含めることができます。

このタスクを完了するには、`magento/catalog-data-exporter` モジュールを更新して、[依存関係インジェクション設定ファイル ](https://developer.adobe.com/commerce/php/development/build/dependency-injection-file/) （`di.xml`）に追加のシステム属性を追加します。

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

開発者は、次のいずれかの方法を使用して、[製品属性フィールド ](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/products/#output-fields)からアクセスできる製品属性を追加できます。

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

データパッチの作成について詳しくは、*PHP開発者ガイド*&#x200B;の[ データおよびスキーマパッチの開発](https://developer.adobe.com/commerce/php/development/components/declarative-schema/patches/)を参照してください。

### product属性を動的に追加します

新しいEAV属性を導入せずに製品属性を動的に作成する方法について詳しくは、[製品属性を動的に追加](add-attribute-dynamically.md)を参照してください。

## フィード スキーマの概要（`et_schema.xml`） {#feed-schema-overview}

各フィードデータ構造は、単純なXML DSLを使用して`etc/et_schema.xml`で宣言されます。 このフレームワークは、このファイルを読み取り、収集するフィールドと呼び出すPHP プロバイダークラスを決定します。

```xml
<record name="Product">
  <field name="sku" type="ID" />
  <field name="name" type="String" />
  <field name="attributes" type="Attribute" repeated="true"
         provider="Magento\CatalogDataExporter\Model\Provider\Product\Attributes">
    <using field="productId" />
    <using field="storeViewCode" />
  </field>
</record>
```

主な要素：

- `<record>` - フィード エンティティを定義します
- `<field>` - データフィールドを宣言します。`provider`属性は、データを取得する`DataProcessorInterface`を実装するPHP クラスを指します
- `repeated="true"` - フィールドはオブジェクトの配列です
- `<using>` – 親レコードコンテキストからプロバイダーに渡された入力パラメーター

>[!IMPORTANT]
>
>`et_schema.xml`に新しいフィールドを追加すると、[!DNL Adobe Commerce]がローカルで収集するもののみが変更されます。 また、受信するSaaS サービスも、ストアフロントに影響を与える前に、新しいフィールドを受け入れて処理するように更新する必要があります。

## 送信後のデータの監視 {#observe-data-after-submission}

[!DNL SaaS Data Export]は、SaaS サービスにバッチ送信が成功するたびに`data_sent_outside` イベントをディスパッチします。 このイベントは、監査ログ、Webhook トリガー、または指標の収集に使用します。

**イベント：** `data_sent_outside`

**使用可能なデータ：**

| キー | 説明 |
|---|---|
| `timestamp` | 送信のUnix タイムスタンプ |
| `type` | フィード名（例：`products`、`prices`） |
| `data` | 送信されたフィード ペイロード |

**例オブザーバー：**

```php
<?php
namespace My\Module\Observer;

use Magento\Framework\Event\Observer;
use Magento\Framework\Event\ObserverInterface;

class DataSentOutsideObserver implements ObserverInterface
{
    public function execute(Observer $observer): void
    {
        $feedName = $observer->getData('type');
        $timestamp = $observer->getData('timestamp');
        $data = $observer->getData('data');

        // Custom logic: audit logging, webhook, metrics
    }
}
```

オブザーバーを`etc/events.xml`に登録します：

```xml
<event name="data_sent_outside">
    <observer name="my_module_data_sent_outside"
              instance="My\Module\Observer\DataSentOutsideObserver" />
</event>
```

イベントとオブザーバーの一般的な情報については、Adobe Commerce Developer ドキュメントの[ イベントとオブザーバー](https://developer.adobe.com/commerce/php/development/components/events-and-observers){target="_blank"}を参照してください。

## 送信前にデータをフィルタリング

データがSaaS サービスに送信される前に、`Magento\SaaSCommon\Model\DataFilter`拡張ポイントを使用して、機密フィールドを墨消しするか、特定のエンティティをスキップします。 これは、GDPRやPCIなどのコンプライアンス要件で、特定のフィールドがCommerce インスタンスを離れてはならない場合に便利です。

インターフェイスを実装し、`etc/di.xml`のDI環境設定を介してワイヤー接続します。

```xml
<preference for="Magento\SaaSCommon\Model\DataFilter"
            type="My\Module\Model\MyDataFilter" />
```

>[!NOTE]
>
>フィルタリングはデータ収集後に適用されます。 `PERSIST_EXPORTED_FEED=1`が設定されている場合、フィード テーブルには、フィルタリングが実行される前に、フィルタリングされていないペイロードが格納されます。

>[!MORELIKETHIS]
>
> - [製品属性を動的に追加](add-attribute-dynamically.md)
> - [税区分、属性セットおよび在庫メタデータを追加](add-tax-attribute-set-inventory-attributes.md)
> - [同期の仕組み](sync-overview.md)
