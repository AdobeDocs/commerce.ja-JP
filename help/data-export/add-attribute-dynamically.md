---
title: 製品属性の動的な追加
description: データの同期処理中にカスタム製品属性をデータ書き出しフィードに動的に追加する方法を説明します。
role: Admin, Developer
exl-id: d5ed7497-4be1-440a-a567-81b64fdc54fc
source-git-commit: bf45670a0bc5fb02dd229a9e3d7af7f2676c5a1f
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 0%

---

# データ同期中に製品属性を動的に追加

データの同期処理中に属性を追加するプラグインを作成することで、Adobe Commerceに属性を登録することなく、製品属性を拡張できます。

>[!NOTE]
>
>製品属性を拡張する最適な方法は、[Adobe Commerceに追加 ](extensibility-and-customizations.md#add-product-attributes-to-adobe-commerce) することです。この場合、Commerce管理者から設定および管理できます。 動的に追加するのは、Commerce ストアフロントサービス専用で必要であり、Adobe Commerceには登録しない場合のみです。 また、カタログサービスを使用した [API メッシュ ](../catalog-service/mesh.md) を使用してカスタム属性を管理し、カタログサービスのGraphQL スキーマを拡張するオプションもあります。

## 製品属性の追加

`Magento\CatalogDataExporter\Model\Provider\Product\Attributes` クラスに `customer_attribute` を追加するプラグインを作成します。

1. [ 依存関係挿入設定ファイル ](https://developer.adobe.com/commerce/php/development/build/dependency-injection-file/) （`di.xml`）を更新して、プラグインを定義します。

   ```xml
   <type name="Magento\CatalogDataExporter\Model\Provider\Product\Attributes">
     <plugin name="product_customer_attributes" type="Vendor\CatalogDataExporter\Model\Plugin\AddAttribute"/>
   </type>
   ```

1. プラグインを作成します。

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

   プラグインを追加すると、次回スケジュールされた同期中に、変更内容が接続されたストアフロントサービスに同期されます。 更新を直ちに送信するには、次の CLI コマンドを使用して同期プロセスを手動で開始します。

   ```
   bin/magento saas:resync --feed=products
   ```

## カスタム製品属性メタデータの宣言

カスタムの製品属性を動的に作成し、それをストアフロントサービスでの表示、検索またはフィルタリングに使用する場合は、製品属性メタデータを追加して、ストアフロントの動作を設定します。

1. [ 依存関係挿入設定ファイル ](https://developer.adobe.com/commerce/php/development/build/dependency-injection-file/) （`di.xml`）を更新して、製品属性メタデータのプラグインを定義します。

   ```xml
   <type name="\Magento\CatalogDataExporter\Model\Provider\ProductMetadata">
     <plugin name="product_customer_attributes_metadata" type="Vendor\CatalogDataExporter\Model\Plugin\AddAttributeMetadata"/>
   </type>
   ```

1. 次のプロバイダー `\Magento\CatalogDataExporter\Model\Provider\ProductMetadata` にプラグインを作成します。

   必須フィ `ProductAttributeMetadata` ルドの `vendor/magento/module-catalog-data-exporter/etc/et_schema.xml` をチェックインします。

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

   プラグインを追加すると、次回スケジュールされた同期中に、変更内容が接続されたストアフロントサービスに同期されます。 更新を直ちに送信するには、次の CLI コマンドを使用して同期プロセスを手動で開始します。

   ```
   bin/magento saas:resync --feed=productattributes
   ```
