---
title: プライスブック
description: ' [!DNL Adobe Commerce Optimizer]の価格表の管理方法について説明します。'
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="SaaSのみ" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud Serviceおよび [!DNL Adobe Commerce Optimizer]  プロジェクトにのみ適用されます（Adobeで管理されるSaaS インフラストラクチャ）。"
exl-id: a1849830-3d0e-4df9-ab73-380659c3f9dc
TQID: https://experienceleague.adobe.com/-vL79MMePcUdhE-gPwjFJZStZUtNLKAUxpePm4Fvmfk
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 33cd0e217447351b690646ec8d230f76060a74da
workflow-type: tm+mt
source-wordcount: 384
ht-degree: 0%

---

# プライスブック

価格表：様々な顧客層や市場をまたいで、カタログソースの製品価格を定義できます。 プライスブックは階層モデルをサポートしており、各ベースプライスブックの下にネストされた子プライスブックを最大3つのレベルで表示できます。 各価格表は親価格表を参照し、価格表カタログ ソースのツリー構造を形成できます。

![価格表の階層](../assets/price-book-hier.png)

基本価格表は、それ自体とそのすべての子価格表の通貨を定義します。 子価格表はこの通貨を継承し、上書きできません。

## 価格表を[!DNL Adobe Commerce Optimizer]に追加

価格表APIを使用して[!DNL Adobe Commerce Optimizer]に価格表を追加します。 [!DNL Adobe Commerce Optimizer]の価格表を作成、更新、削除する方法については、[開発者ドキュメント &#x200B;](https://developer.adobe.com/commerce/services/reference/rest/)を参照してください。

## [!DNL Adobe Commerce Optimizer]の価格表を表示

価格表を[!DNL Adobe Commerce Optimizer]に取り込むと、**カタログ ビュー** ページに価格表のリストと対応するIDが表示されます。

1. _ストア設定_&#x200B;に移動し、**[!UICONTROL Catalog views]**&#x200B;をクリックします。

1. **[!UICONTROL Create catalog view]**&#x200B;をクリックします。 &#x200B;

   カタログビューの詳細を設定で、使用可能な価格表のいずれかを選択します。

   ![価格書名とID](../assets/price-book-name-ids.png)

## 主要な概念

| 条件 | 説明 |
|------|-------------|
| **価格表** | カタログソースの価格を定義する論理グループ（特定の地域や顧客層など）。製品価格の管理に使用されます。 |
| **フォールバック価格表** | 階層の最上位の価格表。 親は持たず、*のみ*&#x200B;の価格表で、それ自体とそのすべての子孫の価格表の通貨を定義します。<br/><br/>価格表の作成中に（APIを介して）親が定義されていない場合、新しいフォールバック価格表が作成されます。 |
| **親価格表** | 子で明示的に設定されていない場合に、子の価格表が価格を継承できる、より上位レベルの価格表。 |
| **階層の深さ** | 最大3つのレベル（フォールバック/子/孫） <br/><br/>取り込み時に適用されません。 |
| **通貨** | フォールバック価格表にのみ定義されます。 すべての児童価格本に継承されます。<br/><br/> フォールバック価格表の作成中に（APIを介して）通貨が指定されていない場合、通貨はデフォルトでUSDになります。 |
| **製品価格** | 特定の価格表の中の製品（SKU）に割り当てられた特定の価格。 |
| **割引** | 割引は商品価格で定義されています。 継承しない。 |
