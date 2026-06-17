---
title: 製品属性の動的な追加
description: データ同期プロセス中に、カスタム製品属性をデータ書き出しフィードに動的に追加する方法について説明します。
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
exl-id: d5ed7497-4be1-440a-a567-81b64fdc54fc
TQID: https://experienceleague.adobe.com/SZWtLSvxb-w-968f4wqWrPTBn1c9IEuthvhIv86Pvss
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
source-git-commit: 182aa9ce819807d1ede85c4fa459714e7dfe0478
workflow-type: tm+mt
source-wordcount: 267
ht-degree: 0%

---

# 製品属性の動的な追加

データ同期プロセス中に属性を追加するプラグインを作成することで、製品属性を[!DNL Adobe Commerce]に登録せずに拡張できます。

>[!NOTE]
>
>製品属性を拡張する最適な方法は、[!DNL Catalog Service] [!DNL GraphQL] スキーマを拡張するために [!DNL Catalog Service][&#128279;](../catalog-service/mesh.md)で [!DNL Adobe Commerce][&#128279;](extensibility-and-customizations.md#add-product-attributes-to-adobe-commerce) where you can configure and manage them from the Commerce Admin. Only add them dynamically if you need them solely for Commerce storefront services and do not want to register them in [!DNL Adobe Commerce]. You also have the option to manage custom attributes using [!DNL API Mesh] に追加することです。

## 製品属性の追加

`customer_attribute`を`Magento\CatalogDataExporter\Model\Provider\Product\Attributes` クラスに追加するプラグインを作成します。

1. [依存関係インジェクション設定ファイル &#x200B;](https://developer.adobe.com/commerce/php/development/build/dependency-injection-file/) （`di.xml`）を更新して、プラグインを定義します。

   ```xml
   <type name="Magento\CatalogDataExporter\Model\Provider\Product\Attributes">
     <plugin name="product_customer_attributes" type="Vendor\CatalogDataExporter\Model\Plugin\AddAttribute"/>
   </type>
   ```

1. プラグインの作成。

   ```php
    <?php
    declare(strict_types=1);
   
    namespace Vendor\CatalogDataExporter\Model\Plugin;
   
    use Magento\CatalogDataExporter\Model\Provider\Product\Attributes;
   
    class AddAttribute {
   
         /**
          * @param Attributes $subject
          * @param array $result
          * @param $arguments
          * @return array
          * @throws \Zend_Db_Statement_Exception
          */
          public function afterGet(Attributes $subject, array $result, $arguments): array
          {
              $additionalAttributes = [];
              $attributeCode = 'customer_attribute';
              foreach ($result as $product) {
                  if (!isset($product['productId']) || !isset($product['storeViewCode'])) {
                      continue;
                  }
                  // HINT: if needed, do filtration by "storeViewCode" and or "productId"
   
                  $productId = $product['productId'];
                  $storeViewCode = $product['storeViewCode'];
   
                  $newKey = \implode('-', [$product['storeViewCode'], $product['productId'], $attributeCode]);
                  if (isset($additionalAttributes[$newKey])) {
                      continue;
                  }
                  $additionalAttributes[$newKey] = [
                      'productId' => $productId,
                      'storeViewCode' => $storeViewCode,
                      'attributes' => [
                          'attributeCode' => $attributeCode,
                          // provide single or multiple values for the attribute
                          'value' => [
                              rand(1, 42)
                          ]
                      ]
                  ];
   
              }
   
              return array_merge($result, $additionalAttributes);
          }
    }
   ```

   プラグインを追加すると、次にスケジュールされた同期中に、変更が接続されたストアフロントサービスに同期されます。 更新をすぐに送信するには、次のCLI コマンドを使用して同期プロセスを手動で開始します。

   ```shell
   bin/magento saas:resync --feed=products
   ```

## カスタム製品属性メタデータの宣言

カスタム製品属性を動的に作成し、ストアフロントサービスでの表示、検索、フィルタリングに使用する場合は、製品属性メタデータを追加してストアフロントの動作を設定します。

1. [依存関係インジェクション設定ファイル &#x200B;](https://developer.adobe.com/commerce/php/development/build/dependency-injection-file/) （`di.xml`）を更新して、製品属性メタデータのプラグインを定義します。

   ```xml
   <type name="Magento\CatalogDataExporter\Model\Provider\ProductMetadata">
     <plugin name="product_customer_attributes_metadata" type="Vendor\CatalogDataExporter\Model\Plugin\AddAttributeMetadata"/>
   </type>
   ```

1. 次のプロバイダー`Magento\CatalogDataExporter\Model\Provider\ProductMetadata`のプラグインを作成します。

   必須フィールドについては、`vendor/magento/module-catalog-data-exporter/etc/et_schema.xml`の`ProductAttributeMetadata`を確認してください。

   ```php
    <?php
    declare(strict_types=1);
   
    namespace Vendor\CatalogDataExporter\Model\Plugin;
   
    use Magento\CatalogDataExporter\Model\Provider\ProductMetadata;
   
    class AddAttributeMetadata {
   
         /**
          * @param ProductMetadata $subject
          * @param array $result
          * @param $arguments
          * @return array
          * @throws \Zend_Db_Statement_Exception
          */
         public function afterGet(ProductMetadata $subject, array $result, $arguments): array
         {
              $result[] = [
                'id' => '123',
                // provide storeCode, websiteCode and storeViewCode applicable for your AC instance
                'storeCode' => 'default',
                'websiteCode' => 'base',
                'storeViewCode' => 'default',
                // specify the customer attribute code - should be the same as used in the products attributes plugin
                'attributeCode' => 'customer_attribute',
                // only product attributes are supported
                'attributeType' => 'catalog_product',
                // specify the data type
                'dataType' => 'int',
                'multi' => false,
                'label' => 'Customer Attribute',
                'frontendInput' => 'select',
                'required' => false,
                'unique' => false,
                'global' => true,
                'visible' => true,
                'searchable' => true,
                'filterable' => true,
                // This value must be set to true to export it to the storefront services
                'visibleInCompareList' => true,
                'visibleInListing' => true,
                'sortable' => true,
                'visibleInSearch' => true,
                'filterableInSearch' => true,
                'searchWeight' => 1.0,
                'usedForRules' => true,
                'boolean' => false,
                'systemAttribute' => false,
                'numeric' => false,
                // specify the list of attribute options
                'attributeOptions' => [
                    'option1',
                    'option2',
                    'option3'
                ]
             ];
   
              return $result;
         }
      }
   ```

   プラグインを追加すると、次にスケジュールされた同期中に、変更が接続されたストアフロントサービスに同期されます。 更新をすぐに送信するには、次のCLI コマンドを使用して同期プロセスを手動で開始します。

   ```shell
   bin/magento saas:resync --feed=productAttributes
   ```

>[!MORELIKETHIS]
>
> * [SaaS データ書き出しフィードの拡張とカスタマイズ &#x200B;](extensibility-and-customizations.md)
> * [Commerce CLIを使用してフィードを同期](data-export-cli-commands.md)
> * [同期の仕組み](sync-overview.md) – 同期モードとスケジュール済み再同期と手動再同期の違いについて説明します。
> * [&#x200B; ログの確認とトラブルシューティング &#x200B;](troubleshooting/logging.md)
