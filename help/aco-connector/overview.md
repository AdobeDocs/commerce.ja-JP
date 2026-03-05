---
title: Adobe Commerce Optimizer コネクタ
description: Commerce Cloud またはオンプレミスプロジェクトからAdobe Commerce Optimizerにデータを接続する方法について説明します
feature: Personalization, Integration, Configuration
badgePaas: label="PaaS のみ" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce on Cloud プロジェクト（Adobeが管理する PaaS インフラストラクチャ）およびオンプレミスプロジェクトにのみ適用されます。"
source-git-commit: 11bb5df2488a017065db44504f35612fe54e284c
workflow-type: tm+mt
source-wordcount: '471'
ht-degree: 0%

---


# Adobe Commerce Optimizer コネクタ

Adobe Commerce Optimizer コネクタは、クラウドインフラストラクチャー上のAdobe Commerceまたはオンプレミスのデプロイメントと [!DNL Adobe Commerce Optimizer] ースの間でカタログと価格データを同期させる統合ブリッジです。 データをAdobe Commerce Optimizerに同期すると、動的AI 検索、Recommendations、サイトの最適化、高速読み込みのヘッドレスストアフロント（Edge Delivery ServicesのAdobe Commerce ストアフロントや real-time performance analytics など）などの機能が可能になります。

## アーキテクチャとエクスペリエンス

次の図に示すように、Adobe Commerce Optimizer Connector は、Commerceの web サイトとストアビューをCommerce Optimizer プロジェクトにマッピングすることで機能します。

![Commerce データのAdobe Commerce Optimizerへのマッピング &#x200B;](./assets/storeview-to-catalogview-mapping.png){width="700" zoomable="yes"}

データがCommerceからCommerce Optimizerに書き出される場合：

* Commerce ストア表示は、カタログソースにマッピングされます。
* Web サイトは価格台帳にマッピングされる

関連するカタログおよび価格データが書き出され、後でカタログビューを作成するために使用され、オプションで、特定のビジネスユースケース向けにカタログおよび価格データをフィルタリングするためのポリシーを定義できます。

コネクタを有効にすると、商品検出用のマーチャンダイジングルールと、[[!DNL Adobe Commerce Optimizer]  マーチャンダイジングツール &#x200B;](../optimizer/overview.md#quick-tour) を使用したレコメンデーション用のルールを設定および管理することもできます。Adobe Commerce インスタンスは、カタログおよび価格データのデータソースになります。 Commerceでデータが更新されると、更新内容が [!DNL Adobe Commerce Optimizer] インスタンスに同期されます。

## ワークフロー

コネクタにより、次の主要なワークフローが可能になります。

* **Commerce カタログデータの[!DNL Adobe Commerce Optimizer]** への書き出し – 価格および価格台帳のデータは、web サイトおよび顧客グループレベルで書き出されます。 製品および製品属性データは、`store view` レベルで書き出されます。 デフォルトでは、すべてのCommerce スコープ（web サイトおよびストアビュー）でカタログデータ同期が有効になっています。

  このワークフローを有効にするには、`adobe-commerce/commerce-data-export-aco-adapter` PHP 拡張機能をインストールし、エクスポーター設定を確認して、Commerce管理者からCommerceとCommerce Optimizerの統合を有効にします。 手順について詳しくは、[&#x200B; はじめに &#x200B;](#get-started) を参照してください。

* **Commerceの web サイトとストアビューデータを[!DNL Adobe Commerce Optimizer]** に書き出すためにマッピングする

  必要に応じて、書き出し設定をカスタマイズし、特定の web サイトまたはストアビューのデータのみを同期します。 例えば、特定の市場や地域の検索および検出エクスペリエンスの最適化など、特定のユースケースに使用するために、1 つのストアビューのカタログデータのみをエクスポートするように選択できます。

* **マーチャンダイジングルールの設定と管理**

  コネクターを有効にすると、商品検出およびレコメンデーションのマーチャンダイジングルールが、Commerce管理の [!DNL Adobe Commerce Optimizer] ページや [!UICONTROL Live Search] ページではなく、[!UICONTROL Product Recommendations] UI から定義および管理されるようになります。

* **Edge Delivery ServicesにCommerce ストアフロントをデプロイする**

  [!DNL Adobe Commerce Optimizer] との統合を設定したら、Edge Delivery ServicesにCommerce ストアフロントをデプロイできます。 これにより、コンポーザブルな API 駆動型アーキテクチャを使用して、超高速パフォーマンス、スケーラビリティ、シームレスなコンテンツオーサリングおよび統合されたパーソナライゼーションが実現されます。

統合のセットアップ方法とこれらのワークフローの有効化方法について詳しくは、[&#x200B; はじめに &#x200B;](get-started.md) を参照してください。
