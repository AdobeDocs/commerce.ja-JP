---
title: インデックス作成
description: 製品属性プロパティ  [!DNL Live Search]  インデックスを作成する方法について説明します。
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '739'
ht-degree: 0%

---

# インデックス作成

[!DNL Live Search] のインデックス作成プロセスでは、カタログを読み取って製品属性を取得し、製品をすばやく検索、フィルタリング、提示できるようにインデックスを作成します。

製品属性プロパティ（メタデータ）によって次が決まります。

* カタログでの属性の使用方法
* ストア内の外観と動作
* データ転送操作に含まれるデータ

属性メタデータの範囲は `website/store/store view` です。

[!DNL Live Search] API を使用すると、クライアントは、Adobe Commerce管理で [storefront プロパティ ](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/product-attributes/product-attributes) が `Yes` に設定されている任意の product 属性で並べ替え `Use in Search` ことができます。 有効にすると、属性に `Search Weight` を設定できます。

[!DNL Live Search] は、削除された製品または `Not Visible Individually` に設定された製品のインデックスを作成しません。

>[!NOTE]
>
> [!DNL Live Search] を使用するCommerceのお客様は、[SaaS 価格インデクサー ](../price-index/price-indexing.md) を使用して、web サイトでの価格変更の更新と同期時間の高速化を活用できます。

## インデックス作成パイプライン

クライアントはストアフロントから検索サービスを呼び出して、（フィルタリング可能、並べ替え可能な）インデックスメタデータを取得します。 *レイヤーナビゲーションで使用* プロパティが `Filterable (with results)` に設定され、*製品リストで並べ替えに使用* が `Yes` に設定された検索可能な製品属性のみが、検索サービスによって呼び出すことができます。

動的クエリを作成するには、検索サービスが検索可能な属性とその [ 重み付け ](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/catalog/search/search-results) を把握している必要があります。 [!DNL Live Search] は、Adobe Commerce検索の重み付け（1 ～ 10、10 が最も優先度が高い）に従います。 カタログサービスで同期および共有されるデータのリストは、スキーマで見つけることができます。このスキーマは、次で定義されています。

`vendor/magento/module-catalog-data-exporter/etc/et_schema.xml`

![[!DNL Live Search] ンデックス作成クライアント検索図 ](assets/indexing-pipeline.svg)

1. [!DNL Live Search] の使用権限についてマーチャントを確認してください。
1. 属性メタデータの変更を含むストアビューを取得します。
1. インデックス属性を保存します。
1. 検索インデックスの再インデックスを実行します。

### 完全インデックス

オンボーディング中に [!DNL Live Search] を設定して同期すると、初期インデックスの作成に最大 60 分かかる場合があります。 大規模なカタログのインデックス作成には時間がかかる場合があります。 このプロセスは、フィード `cron` 送信し、実行が完了した後に開始されます。

次のイベントは、完全同期とインデックスのビルドをトリガーにします。

* オンボーディング [ カタログデータ同期 ](install.md#synchronize-catalog-data)
* 属性メタデータの変更

例えば、`color` 属性の `Use in Search` プロパティを `No` から `Yes` に変更すると、属性メタデータが `searchable=true` に変更され、フル同期と再インデックスがトリガーされます。 次の属性メタデータトリガーは、変更時に完全な同期と再インデックスを行います。

* `filterableInSearch`
* `searchable`
* `sortable`
* `visibleInSearch`

### 製品アップデートのストリーミング

[ オンボーディング ](install.md#synchronize-catalog-data) 中に初期インデックスが作成されると、次の製品の増分更新が継続的に同期され、インデックスが再作成されます。

* カタログに新しい製品が追加されました
* 製品属性値の変更

例えば、`color` 属性に新しいスウォッチ値を追加すると、ストリーミング製品の更新として処理されます。

ストリーミング更新ワークフロー：

1. 更新された製品は、Adobe Commerce インスタンスからカタログサービスに同期されます。
1. インデックス サービスは、カタログ サービスから製品の更新を継続的に検索します。 更新された製品には、カタログサービスに到着した時点でインデックスが付けられます。
1. 製品アップデートが [!DNL Live Search] で使用可能になるまで、最大 15 分かかる場合があります。

#### 製品の表示に影響するアップデート

[!DNL Live Search] Admin 設定、Adobe Commerce Admin 設定、またはカタログデータを更新した場合、それらの変更がストアフロントに表示されるまでに遅延が生じる可能性があります。

次の表に、様々な変更と、ストアフロントに表示されるまでの待ち時間のおおよその値を示します。

| 更新 | ストアフロントに表示されるまで遅延する |
|---|---|
| [!DNL Live Search] Admin は、ファセット、価格設定、検索またはカテゴリマーチャンダイジングルールを変更しました。 | 15～20 分。 |
| [!DNL Live Search] Admin で、インデックス再作成が必要な変更（言語設定または同義語）を行います。 | 再インデックスが完了してから最大 15 分後。 |
| 完全な再インデックス（検索可能、並べ替え可能またはフィルタリング可能な属性メタデータ）を必要とするAdobe Commerce管理者の変更 | 再インデックスが完了してから最大 15 分後。 |
| インデックス再作成を必要としないカタログデータの増分変更：製品在庫、価格、名前など。 | Elastic Search インデックスが最新のデータで更新されてから最大 15 分後。 |

## クライアント検索

[!DNL Live Search] API では、[storefront プロパティ ](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/product-attributes/product-attributes)、*製品リストでの並べ替えに使用* を `Yes` に設定することで、クライアントは並べ替え可能な製品属性で並べ替えることができます。 テーマによっては、この設定を使用すると、カタログページ上の [ 並べ替え基準 ](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/catalog/navigation/navigation) ページネーションコントロールに属性がオプションとして含められます。 検索およびフィルタリング可能な [ ストアフロントプロパティ ](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/product-attributes/product-attributes) を使用して、[!DNL Live Search] でインデックスを作成できる製品属性は最大 200 個です。

インデックスメタデータはインデックスパイプラインに保存され、検索サービスからアクセスできます。

イ ![[!DNL Live Search] デックスのメタデータ API の図 ](assets/index-metadata-api.svg)

### 並べ替え可能な属性ワークフロー

1. クライアントが検索サービスを呼び出します。
1. Search サービスは、Search Admin Service を呼び出します。
1. 検索サービスはインデックスパイプラインを呼び出します。

## すべての商品に対してインデックスを作成

このリストのフィールドの順序は、書き出された製品データの一般的な列の順序を反映しています。

* `environment_id`
* `website_code`
* `store_code`
* `store_view_code`
* `product_id`
* `sku`
* `name`
* `type`
* `displayable`
* `deleted`
* `url`
* `currency`
* `meta_description`
* `meta_keyword`
* `meta_title`
* `description`
* `short_description`
* `weight`
* `image`
* `small_image`
* `thumbnail_image`
* `prices`
* `in_stock`
* `low_stock`

次のフィールドは、設定可能なすべての製品に対してインデックスが作成されています。

* `childrenSkus`
