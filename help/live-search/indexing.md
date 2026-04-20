---
title: インデックス作成
description: 製品属性プロパティを [!DNL Live Search]  インデックス作成する方法について説明します。
exl-id: 01cbbf56-2e12-4ad0-a56d-de0fe13df50f
source-git-commit: 14c4178338859d55a7391139033d51d1aa6f7678
workflow-type: tm+mt
source-wordcount: '739'
ht-degree: 0%

---

# インデックス作成

[!DNL Live Search]のインデックス作成プロセスでは、カタログ内の製品属性を読み取り、インデックスを作成して、製品を迅速に検索、フィルタリング、表示できるようにします。

製品属性のプロパティ（メタデータ）により、次のことが決定されます。

* カタログでの属性の使用方法
* 店舗での外観と行動
* データ転送操作に含まれるデータ

属性メタデータの範囲は`website/store/store view`です。

[!DNL Live Search] APIを使用すると、クライアントは、Adobe Commerce Adminで[storefront プロパティ ](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/product-attributes/product-attributes) `Use in Search`が`Yes`に設定されている任意のproduct属性で並べ替えることができます。 有効にすると、属性に`Search Weight`を設定できます。

[!DNL Live Search]は、削除された製品または`Not Visible Individually`に設定された製品をインデックス付けしません。

>[!NOTE]
>
> [!DNL Live Search]をご利用のお客様は、[SaaS価格インデクサー](../price-index/price-indexing.md)を使用して、web サイトでの迅速な価格変更と同期時間を活用できます。

## パイプラインのインデックス作成

クライアントは、ストアフロントから検索サービスを呼び出し、（フィルタリング可能で並べ替え可能な）インデックスメタデータを取得します。 検索サービスは、*レイヤーナビゲーションで使用* プロパティが`Filterable (with results)`に設定され、*製品リストで並べ替えに使用*&#x200B;が`Yes`に設定されている検索可能な製品属性のみを呼び出すことができます。

動的クエリを作成するには、検索サービスは、どの属性が検索可能で、[重み](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/catalog/search/search-results)を知っている必要があります。 [!DNL Live Search]はAdobe Commerce検索の重み付けを尊重します（1-10、10は最優先度）。 カタログサービスと同期および共有されるデータのリストは、スキーマで見つけることができます。スキーマは、次の場所で定義されています。

`vendor/magento/module-catalog-data-exporter/etc/et_schema.xml`

![[!DNL Live Search] クライアント検索図のインデックス作成](assets/indexing-pipeline.svg)

1. [!DNL Live Search]の使用権限について加盟店を確認します。
1. 属性メタデータに変更を加えてストアビューを取得します。
1. インデックス属性を保存します。
1. 検索インデックスのインデックスを再作成します。

### フルインデックス

[!DNL Live Search]が設定され、オンボーディング中に同期されると、最初のインデックスの作成に最大60分かかる場合があります。 大きなカタログのインデックス作成には時間がかかる場合があります。 プロセスは、`cron`がフィードを送信し、実行を完了した後に開始されます。

次のイベントは、完全なシンクとインデックスのビルドをトリガーします。

* [ カタログデータ同期](install.md#sync)のオンボーディング
* 属性メタデータの変更

例えば、`Use in Search`属性の`color` プロパティを`No`から`Yes`に変更すると、属性メタデータが`searchable=true`に変更され、完全な同期と再インデックスがトリガーされます。 次の属性メタデータは、完全な同期をトリガーし、変更されたときにインデックスを再作成します。

* `filterableInSearch`
* `searchable`
* `sortable`
* `visibleInSearch`

### 製品アップデートのストリーミング

[ オンボーディング ](install.md#sync)中に最初のインデックスが構築された後、次の製品の増分更新が継続的に同期され、インデックスが再作成されます。

* カタログに追加された新商品
* 製品属性値の変更

例えば、`color`属性に新しいスウォッチ値を追加すると、ストリーミング製品の更新として処理されます。

ストリーミング更新ワークフロー：

1. 更新された商品は、Adobe Commerce インスタンスからカタログサービスに同期されます。
1. インデックスサービスは、カタログサービスから製品の更新を継続的に検索します。 更新された製品は、カタログサービスに到着すると、インデックスに登録されます。
1. 製品の更新が[!DNL Live Search]で利用できるようになるまでに、最大15分かかる場合があります。

#### 製品の表示に影響するアップデート

[!DNL Live Search]管理者設定、Adobe Commerce管理者設定、またはカタログデータの更新を行う場合、これらの変更がストアフロントに表示されるまでに遅延が発生する可能性があります。

次の表に、様々な変更と、ストアフロントに表示されるまでの概算の待ち時間を示します。

| 更新 | ストアフロントに表示されるまでの遅延時間 |
|---|---|
| ファセット、価格設定、検索またはカテゴリ マーチャンダイジングルールの[!DNL Live Search]管理者による変更。 | 15～20分。 |
| インデックス再作成が必要な[!DNL Live Search]管理者の変更：言語設定または同義語。 | インデックス再作成が完了してから最大15分後です。 |
| 完全なインデックス再作成が必要なAdobe Commerce管理者の変更：検索可能、並べ替え可能、またはフィルター可能な属性メタデータ | インデックス再作成が完了してから最大15分後です。 |
| インデックス再作成が不要なカタログデータの増分変更（商品の在庫、価格、名前など）。 | Elastic Search インデックスが最新のデータで更新されてから最大15分後。 |

## クライアント検索

[!DNL Live Search] APIを使用すると、[storefront プロパティ ](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/product-attributes/product-attributes)、*製品リスト*&#x200B;から`Yes`の並べ替えに使用されるプロパティを設定して、任意の並べ替え可能な製品属性でクライアントを並べ替えることができます。 テーマに応じて、この設定を使用すると、カタログ ページの[並べ替え](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/catalog/navigation/navigation) ページネーション コントロールのオプションとして属性が含まれます。 最大200個の製品属性を[!DNL Live Search]でインデックス付けでき、検索可能でフィルタリング可能な[ ストアフロントプロパティ ](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/product-attributes/product-attributes)があります。

インデックスメタデータはインデックスパイプラインに保存され、検索サービスからアクセスできます。

![[!DNL Live Search] インデックス メタデータ API ダイアグラム ](assets/index-metadata-api.svg)

### 並べ替え可能な属性ワークフロー

1. クライアントは検索サービスを呼び出します。
1. 検索サービスは、検索管理サービスを呼び出します。
1. 検索サービスは、インデックスパイプラインを呼び出します。

## すべての製品のインデックス

このリストのフィールドの順序は、書き出された製品データの列の一般的な順序を反映しています。

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

次のフィールドは、設定可能なすべての製品に対してインデックスが作成されます。

* `childrenSkus`
