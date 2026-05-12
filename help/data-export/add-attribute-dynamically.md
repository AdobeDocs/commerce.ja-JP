---
title: 製品属性の動的な追加
description: データ同期プロセス中に、カスタム製品属性をデータ書き出しフィードに動的に追加する方法について説明します。
role: Admin, Developer
exl-id: d5ed7497-4be1-440a-a567-81b64fdc54fc
TQID: https://experienceleague.adobe.com/SZWtLSvxb-w-968f4wqWrPTBn1c9IEuthvhIv86Pvss
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: d1e21356-0064-4f48-9089-16e3f0dbd2a6id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
source-git-commit: 33cd0e217447351b690646ec8d230f76060a74da
workflow-type: tm+mt
source-wordcount: 297
ht-degree: 0%

---

# データの同期中に製品属性を動的に追加

Adobe Commerceに登録せずに製品属性を拡張するには、データ同期プロセス中に属性を追加するプラグインを作成します。

>[!NOTE]
>
>製品属性を拡張する最適な方法は、[Adobe Commerce](extensibility-and-customizations.md#add-product-attributes-to-adobe-commerce)に追加し、Commerce管理者から設定および管理できるようにすることです。 Commerce ストアフロントサービスにのみ必要で、Adobe Commerceに登録しない場合にのみ、動的に追加します。 また、[API Meshとカタログサービス ](../catalog-service/mesh.md)を使用してカスタム属性を管理し、カタログサービスのGraphQL スキーマを拡張することもできます。

## 製品属性の追加

`customer_attribute`を`Magento\CatalogDataExporter\Model\Provider\Product\Attributes` クラスに追加するプラグインを作成します。

1. [依存関係インジェクション設定ファイル ](https://developer.adobe.com/commerce/php/development/build/dependency-injection-file/) （`di.xml`）を更新して、プラグインを定義します。

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

   ```
   bin/magento saas:resync --feed=products
   ```

## カスタム製品属性メタデータの宣言

カスタム製品属性を動的に作成し、ストアフロントサービスでの表示、検索、フィルタリングに使用する場合は、製品属性メタデータを追加してストアフロントの動作を設定します。

1. [依存関係インジェクション設定ファイル ](https://developer.adobe.com/commerce/php/development/build/dependency-injection-file/) （`di.xml`）を更新して、製品属性メタデータのプラグインを定義します。

   ```xml
   <type name="\Magento\CatalogDataExporter\Model\Provider\ProductMetadata">
     <plugin name="product_customer_attributes_metadata" type="Vendor\CatalogDataExporter\Model\Plugin\AddAttributeMetadata"/>
   </type>
   ```

1. 次のプロバイダー`\Magento\CatalogDataExporter\Model\Provider\ProductMetadata`にプラグインを作成します。

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

   ```
   bin/magento saas:resync --feed=productattributes
   ```

