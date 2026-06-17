---
title: カタログソース
description: カタログソースとは何か、および検索、フィルター、並べ替え動作の製品、属性、カテゴリの権限範囲を定義するカタログソースについて説明します。
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="SaaSのみ" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud Serviceおよび [!DNL Adobe Commerce Optimizer]  プロジェクトにのみ適用されます（Adobeで管理されるSaaS インフラストラクチャ）。"
autotag-review: '2026-06-09T19:36:23.516Z'
TQID: 'https://experienceleague.adobe.com/MiLbuYx6Pf95n3jvrgvou05Ery9XHXskx8p6KrN6CYg'
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: d1e21356-0064-4f48-9089-16e3f0dbd2a6id: dac87252-6066-4d6e-a9d2-f6d84c323de7id: c18ed297-2187-4aec-affb-9d9654eca6fc
subfeature_v2: id: ae62cf09-5996-4921-bda8-fbe67b62e470
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: b23e006f-0a29-4f1d-8fd0-77aa56f3d12bid: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: 94ba07437d532d0d101c166f58114c2aa0bd4be4
workflow-type: tm+mt
source-wordcount: 446
ht-degree: 0%

---

# カタログソース

カタログソース：製品、属性、カテゴリーの権限範囲を表します。 通常、言語、オーディエンス、原産地系の境界にマッピングし、検索、フィルター、並べ替えの動作を決定します。

## カタログソースと関連する概念

カタログソースが他の[!DNL Adobe Commerce Optimizer]概念とどのように関連しているかを理解すると、データを正しくモデル化できます。

* **カタログ ソース** – 製品情報を提供する基礎となるデータ コンテキスト。 カタログソースは、通常、ロケール（`en-US`、`fr-CA`など）またはPIMやERPなどの外部システムです。 製品、属性、メタデータ、およびカテゴリはすべて、カタログソースごとに範囲が設定されます。 カタログソースは、生のカタログデータの出所が&#x200B;*どこから*&#x200B;か、商品の発見（検索結果、フィルタリング、並べ替え動作）に影響を与える方法が&#x200B;*どのように*&#x200B;と考えることができます。

* **[カタログ ビュー](catalog-view.md)** – 特定のビジネス ニーズに合わせてカタログの設定済みビュー。 カタログビューを作成する際に、使用するカタログソース（またはロケール）を選択し、[ ポリシー](policies.md)を追加して、表示される製品をフィルタリングし、[価格表](pricebooks.md)をリンクして価格設定を制御します。 単一のカタログソースを使用すると、多数のカタログビューを利用できます（例えば、ブランドや地域ごとに別々のカタログビューを持つ1つの`en-US` ソース）。 カタログビューは、そのデータをストアフロント、チャネル、オーディエンスに公開する&#x200B;*方法*&#x200B;と考えてください。

* **[カタログレイヤー](catalog-layer.md)** - ソースデータを変更せずに製品属性（名前、説明、画像、メタデータ）を変更するために、ベースカタログデータの上に適用されるレイヤー。 カタログレイヤーは、ストアフロントの表示のみに影響し、商品の発見に影響を与えない場合に使用します。

## ルールと制限

* 各カタログソースは、Data Ingestion APIを使用して製品を取り込むことで作成されます。 詳しくは、[開発者ドキュメント – データ収集](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/)を参照してください。
* 製品の一意性は、SKU + カタログソースで決まります。
* 買い物客はカタログソースに直接アクセスすることはありません。 カタログデータは、[ カタログビュー](catalog-view.md)を介してストアフロントに公開されます。

## モデリングガイダンス

カタログソースの構成方法を決定する際には、次のガイダンスを使用します。

* カタログ言語ごとに個別のカタログソースを作成します。
* 製品と属性の違いが検索、フィルタリング、または並べ替え動作に影響する必要がある場合は、別々のカタログソースを使用します（例えば、同じ属性に対して異なる検索性、フィルタリング可能性、またはファセット設定など）。
* 製品と属性の違いがストアフロントの表示のみに影響し、製品の検出に影響しない必要がある場合は、[ カタログレイヤー](catalog-layer.md)を使用します。

>[!MORELIKETHIS]
>
> * [ カタログ ビュー](catalog-view.md) - カタログ ソースの上にフィルターされた価格ビューを設定します
> * [ カタログレイヤー](catalog-layer.md) - ソースデータを変更せずに製品プレゼンテーションを変更する
> * [ ポリシー](policies.md) - カタログ ビューの属性ベースのフィルターを作成します
> * [価格表](pricebooks.md) – 様々な顧客セグメントの価格構成を管理します

