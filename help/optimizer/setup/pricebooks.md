---
title: 価格台帳
description: ' [!DNL Adobe Commerce Optimizer] で価格台帳を管理する方法を説明します。'
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="SaaS のみ" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud ServiceおよびAdobe Commerce Optimizer プロジェクトにのみ適用されます（Adobeで管理される SaaS インフラストラクチャ）。"
exl-id: a1849830-3d0e-4df9-ab73-380659c3f9dc
source-git-commit: 1c720bc3ba755639eff2f17912fb3a3446e367f6
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 0%

---

# 価格台帳

価格台帳を使用すると、様々な顧客層や市場をまたいでカタログソースの製品価格を定義できます。 価格台帳は階層モデルをサポートしており、各ベース価格台帳の下にネストされた子価格台帳を最大 3 レベルまで作成できます。 各価格台帳は、親価格台帳を参照し、価格設定カタログ・ソースのツリー構造を形成できます。

![&#x200B; 価格台帳階層 &#x200B;](../assets/price-book-hier.png)

基本価格台帳では、それ自体とすべての子価格台帳に対して通貨が定義されます。 子の価格帳簿はこの通貨を継承し、上書きすることはできません。

## Commerce Optimizerへの価格台帳の追加

価格台帳は、価格台帳 API を使用してCommerce Optimizerに追加します。 [&#x200B; の価格帳簿を作成、更新、削除する方法については、](https://developer.adobe.com/commerce/services/reference/rest/) 開発者向けドキュメント [!DNL Adobe Commerce Optimizer] を参照してください。

## Commerce Optimizerで価格台帳を表示します。

価格台帳をCommerce Optimizerに取り込むと、価格台帳のリストと対応する ID が「**カタログ・ビュー**」ページに表示されます。

1. _ストアの設定_ に移動し、「**[!UICONTROL Catalog views]**」をクリックします。

1. 「**[!UICONTROL Create catalog view]**」をクリックします。&#x200B;

   カタログ表示の詳細を設定で、使用可能な価格台帳の 1 つを選択します。

   ![&#x200B; 価格簿名及び ID](../assets/price-book-name-ids.png)

## 主要な概念

| 用語 | 説明 |
|------|-------------|
| **価格台帳** | カタログソース（特定の地域や顧客層など）の価格を定義する論理グループ化で、製品価格の管理に使用されます。 |
| **フォールバック価格台帳** | 階層内で最上位の価格台帳。 親がなく、それ自体とすべての下位価格帳簿の通貨を定義する *唯一* 価格帳簿です。<br/><br/> 価格台帳の作成中に親が定義されていない場合（API を介して）、新しいフォールバック価格台帳が作成されます。 |
| **親価格台帳** | 子に明示的に設定されていない場合に、子の価格台帳が価格を継承できる上位レベルの価格台帳。 |
| **階層の深度** | 取り込み時に最大 3 つのレベル（フォールバック/子/孫） <br/><br/> 適用されません。 |
| **通貨** | フォールバック価格帳簿に対してのみ定義します。 すべての児童価格帳簿に引き継がれます。<br/><br/> フォールバック価格台帳の作成時に（API を通じて）通貨を指定しない場合、通貨はデフォルトで USD になります。 |
| **製品価格** | 特定の価格台帳内で製品（SKU）に割り当てられた特定の価格。 |
| **割引** | 割引は製品価格で定義されます。 継承されません。 |
