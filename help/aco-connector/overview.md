---
title: Adobe Commerce Optimizer Connector
description: Commerce クラウドまたはオンプレミス プロジェクトのデータをAdobe Commerce Optimizerに接続する方法について説明します
feature: Personalization, Integration, Configuration
badgePaas: label="PaaSのみ" type="Informative" url="https://experienceleague.adobe.com/ja/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce on Cloud プロジェクト（Adobeで管理されるPaaS インフラストラクチャ）とオンプレミス プロジェクトにのみ適用されます。"
source-git-commit: 14c4178338859d55a7391139033d51d1aa6f7678
workflow-type: tm+mt
source-wordcount: '471'
ht-degree: 0%

---


# Adobe Commerce Optimizer Connector

Adobe Commerce Optimizer コネクタは、Adobe Commerce オンクラウド インフラストラクチャまたはオンプレミス デプロイメントと[!DNL Adobe Commerce Optimizer]の間でカタログと価格データを同期する統合ブリッジです。 データをAdobe Commerce Optimizerに同期することで、動的なAI 検索、レコメンデーション、サイトの最適化、Edge Delivery Services上のAdobe Commerce ストアフロントなどの高速読み込みヘッドレスストアフロント、real-time performance analyticsなどの機能が可能になります。

## アーキテクチャと経験

Adobe Commerce Optimizer コネクタは、次の図に示すように、Commerce web サイトとストアビューをCommerce Optimizer プロジェクトにマッピングすることで機能します。

![Commerce データのAdobe Commerce Optimizerへのマッピング &#x200B;](./assets/storeview-to-catalogview-mapping.png){width="700" zoomable="yes"}

データがCommerceからCommerce Optimizerに書き出される場合：

* Commerce ストアビューは、カタログソースにマッピングされます
* web サイトは価格表に紐づけられている

関連するカタログと価格データが書き出され、後でカタログビューを作成し、オプションでポリシーを定義して、特定のビジネスユースケースのカタログと価格データをフィルタリングします。

コネクタが有効になっている場合は、[[!DNL Adobe Commerce Optimizer]  マーチャンダイジングツール &#x200B;](../optimizer/overview.md#quick-tour)を使用して、商品の発見とレコメンデーションのルールのマーチャンダイジングルールを設定および管理することもできます。Adobe Commerce インスタンスは、カタログと価格データのデータソースになります。 Commerceでデータが更新されると、更新は[!DNL Adobe Commerce Optimizer] インスタンスに同期されます。

## ワークフロー

コネクタを使用すると、いくつかの主要なワークフローが可能になります。

* **Commerce カタログデータを[!DNL Adobe Commerce Optimizer]**&#x200B;に書き出す：価格と価格表のデータは、web サイトおよび顧客グループ レベルで書き出されます。 製品および製品属性データは`store view` レベルで書き出されます。 デフォルトでは、すべてのCommerce スコープ（web サイトとストアビュー）でカタログデータの同期が有効になっています。

  このワークフローを有効にするには、`adobe-commerce/commerce-data-export-aco-adapter` PHP拡張機能をインストールし、エクスポーター設定を確認してから、Commerce管理者からCommerceとCommerce Optimizerの統合を有効にします。 詳細な手順については、[基本を学ぶ](get-started.md)を参照してください。

* **Commerce web サイトとストアビューデータを[!DNL Adobe Commerce Optimizer]**&#x200B;に書き出すようにマッピングする

  必要に応じて、書き出し設定をカスタマイズして、特定のweb サイトまたはストアビューのデータのみを同期します。 例えば、特定の市場や地域に対する検索および発見体験の最適化など、特定のユースケースに使用するカタログデータを1つのストアビューにのみ書き出すように選択できます。

* **マーチャンダイジングルールの設定と管理**

  コネクタが有効になっている場合、商品の発見とレコメンデーションのマーチャンダイジングルールは、Commerce管理者の[!DNL Adobe Commerce Optimizer] ページと[!UICONTROL Live Search] ページではなく、[!UICONTROL Product Recommendations] UIから定義および管理されます。

* **Edge Delivery ServicesでのCommerce ストアフロントのデプロイ**

  [!DNL Adobe Commerce Optimizer]との統合を設定したら、Edge Delivery ServicesにCommerce Storefrontをデプロイできます。 これにより、構成可能なAPI ドリブン型のアーキテクチャを使用して、超高速のパフォーマンス、スケーラビリティ、シームレスなコンテンツオーサリング、統合されたパーソナライゼーションを実現できます。

統合を設定し、これらのワークフローを有効にする方法について詳しくは、[開始](get-started.md)を参照してください。
