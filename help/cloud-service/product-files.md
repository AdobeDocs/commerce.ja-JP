---
title: 製品へのファイルの追加
description: ' [!DNL Adobe Commerce as a Cloud Service]のファイル形式の製品属性を使用して、PDF、マニュアル、データシートなどのファイルを製品に添付する方法を説明します。'
feature: Catalog Management, Products, Integration
role: Admin, Developer
level: Intermediate
badgeSaas: label="SaaSのみ" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud ServiceおよびAdobe Commerce Optimizer プロジェクト（Adobeが管理するSaaS インフラストラクチャ）にのみ適用されます。"
source-git-commit: 848ba518d170c9a0270b2513fdc8efb6813f6845
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 0%

---

# 製品へのファイルの追加

[!DNL Adobe Commerce as a Cloud Service]は、販売者がファイル（PDF、マニュアル、証明書、データシートなど）を製品に直接添付できる「ファイル」 [製品属性入力タイプ &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/product-attributes/attributes-input-types){target="_blank"}をサポートしています。 ファイルはAmazon S3 メディアストレージに保存され、GraphQLを使用してストアフロントからアクセスすることも、REST APIを使用して統合を介してアクセスすることもできます。

製品ファイル属性にファイルをアップロードするには、次の3つの方法があります。

* [管理者UI](#upload-through-the-admin) – 製品編集ページでファイルを手動でアップロードします。
* [REST API](#upload-through-the-rest-api) - S3事前署名済みURLを使用して、REST APIを介してファイルをアップロードします。
* [製品インポート &#x200B;](#upload-through-product-import) - CSVで外部URLを指定して、ファイルを一括インポートします。

## 前提条件

ファイルをアップロードする前に、ファイル属性を作成し、属性セットに割り当てる必要があります。

* [&#x200B; ファイル属性を作成](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/product-attributes/create/attribute-product-create){target="_blank"} - **[!UICONTROL Catalog Input Type for Store Owner]**&#x200B;を&#x200B;**[!UICONTROL File]**&#x200B;に設定します。

* [属性を属性セットに割り当てる](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/product-attributes/create/attribute-sets#create-an-attribute-set){target="_blank"} – 新しいファイル属性を目的のグループにドラッグします。

* [製品ファイル属性](https://experienceleague.adobe.com/en/docs/commerce-admin/config/catalog/product-file-attributes)設定で許可されるファイルタイプとサイズを設定します。

## 管理者を介したファイルのアップロード

[&#x200B; ファイル属性](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/product-attributes/create/attribute-product-create){target="_blank"}を作成して属性セットに割り当てたら、製品編集ページから直接ファイルをアップロードできます。

1. _管理者_ サイドバーで、**[!UICONTROL Catalog]** > **[!UICONTROL Products]**&#x200B;に移動します。

1. 編集する製品を開きます。

1. ファイル属性フィールドを探し、**[!UICONTROL Upload]**&#x200B;をクリックしてファイルを選択します。

![管理者](./assets/upload-file.png){width="600" zoomable="yes"}の「ファイルをアップロード」ボタン

1. **[!UICONTROL Save]**&#x200B;をクリックします。

ファイルを置き換えるには、既存のファイルを削除し、新しいファイルをアップロードします。 アップロードされたファイルは、Amazon S3 メディアストレージに保存されます。

## REST APIを介したアップロード

[S3事前署名済みURL フロー](https://developer.adobe.com/commerce/webapi/rest/saas-integrations/s3-uploads/){target="_blank"}を使用して、REST APIを介してプログラムでファイルをアップロードします。 このプロセスは、カテゴリ画像や顧客属性ファイルなどの他のメディアタイプと同様に、製品ファイル属性に対して機能します。

プロセスには4つのステップがあります。

1. ファイル名と製品ファイル属性の`POST V1/media/initiate-upload`を使用して`media_resource_type`を呼び出します。
1. 返された事前署名済みURLを`PUT`に使用して、ファイルを直接Amazon S3に送信します。
1. `POST V1/media/finish-upload`に電話して、アップロードを確認してください。
1. 返されたキーを`PUT /V1/products/{sku}`を通じて製品のファイル属性に割り当て、キーを[&#x200B; カスタム属性](https://developer.adobe.com/commerce/webapi/rest/modules/custom-attributes/)値として渡します。

## 製品の読み込みを通じてアップロード

[import API](https://developer.adobe.com/commerce/webapi/rest/modules/import/){target="_blank"}または管理者インポート UIを使用して、製品にファイルを一括で添付できます。 製品ファイル属性では、外部URLからの読み込みのみがサポートされます。これは、製品画像の読み込み[の](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/import/data-import-product-images#method-2-import-images-from-external-server){target="_blank"}方法2と同じ方法です。 Commerceは、指定されたURLからファイルをダウンロードし、S3 メディアストレージに保存します。

>[!NOTE]
>
>ローカル サーバーパス （方法1）からのファイルの読み込みは、直接のファイル システム アクセスがないので、[!DNL Adobe Commerce as a Cloud Service]ではサポートされていません。

### 専用の列にURLを指定します

属性コードをCSV列ヘッダーとして、完全なURLを値として使用します。 例えば、属性コードが`file_upload`の場合、CSVは次のようになります。

```csv
sku,name,file_upload
ADB112,"My Product",https://example.com/files/manual.pdf
```

### `additional_attributes`にURLを指定してください

または、`additional_attributes`列にファイル属性を含めます。

```csv
sku,name,additional_attributes
ADB112,"My Product",file_upload=https://example.com/files/manual.pdf
```

いずれの場合も、URLは一般にアクセス可能である必要があり、ファイル拡張子とサイズは[設定された制限](https://experienceleague.adobe.com/en/docs/commerce-admin/config/catalog/product-file-attributes){target="_blank"}に準拠している必要があります。

## GraphQLによるファイルの取得

[!DNL Adobe Commerce as a Cloud Service]では、[Catalog Service GraphQL](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/products/){target="_blank"} エンドポイントが商品データを提供します。 ファイル属性は`attributes`の`ProductView` フィールドに表示され、`value`にはファイルの完全なパブリック URLが含まれています。

```graphql
{
  products(skus: ["ADB112"]) {
    sku
    name
    attributes(roles: []) {
      name
      label
      value
    }
  }
}
```

応答には、パブリック URLを含むファイル属性が含まれます。

```json
{
  "data": {
    "products": [
      {
        "sku": "ADB112",
        "name": "Example product",
        "attributes": [
          {
            "name": "file",
            "label": "FILE",
            "value": "https://<host>/media/catalog/product_file/manual.pdf",
          }
        ]
      }
    ]
  }
}
```

>[!NOTE]
>
>このクエリには、`Magento-Website-Code`および`Magento-Store-View-Code`個のヘッダーが必要です。 詳しくは、[&#x200B; カタログサービス製品のクエリ &#x200B;](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/products/){target="_blank"}を参照してください。

## REST APIを使用したファイルの取得

[REST API](https://developer.adobe.com/commerce/webapi/reference/rest/saas/){target="_blank"} （`GET /V1/products/{sku}`）を介して製品を取得する場合、ファイル属性は`custom_attributes`配列に表示され、ファイル名は次の値になります。

```json
{
  "custom_attributes": [
    {
      "attribute_code": "file_upload",
      "value": "manual_7aa0b2d63f6d3dbf.pdf"
    }
  ]
}
```
