---
title: プライスブック
description: '[!DNL Adobe Commerce Optimizer]の価格表の管理方法について説明します。'
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="SaaSのみ" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud Serviceおよび[!DNL Adobe Commerce Optimizer]件のプロジェクト（Adobeが管理するSaaS インフラストラクチャ）にのみ適用されます。"
exl-id: a1849830-3d0e-4df9-ab73-380659c3f9dc
TQID: https://experienceleague.adobe.com/-vL79MMePcUdhE-gPwjFJZStZUtNLKAUxpePm4Fvmfk
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
topic_v2:
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
    internal-label: Personalization
source-git-commit: cde6d0c92f4c169588164c22c948d1b287873bdd
workflow-type: tm+mt
source-wordcount: '595'
ht-degree: 0%
---
# プライスブック

価格表：顧客層と市場をまたいで、カタログソースの製品価格を定義します。 階層モデルをサポートしており、各基本価格表の下にネストされた子価格表を最大3 レベルまで表示できます。 各価格表は親価格表を参照し、価格表カタログ ソースのツリー構造を形成できます。

![価格表の階層](../assets/price-book-hier.png)

基本価格表は、それ自体とそのすべての子価格表の通貨を定義します。 子価格表はこの通貨を継承し、上書きできません。

## 主要な概念

| 条件 | 説明 |
| ------ | ------------- |
| **価格表** | カタログソースの価格を定義する論理グループ（特定の地域や顧客層など）。製品価格の管理に使用されます。 |
| **フォールバック価格表** | 階層の最上位の価格表。 親は持たず、*のみ*&#x200B;の価格表で、それ自体とそのすべての子孫の価格表の通貨を定義します。<br/><br/>価格表の作成中に（APIを介して）親が定義されていない場合、新しいフォールバック価格表が作成されます。 |
| **親価格表** | 子で明示的に設定されていない場合に、子の価格表が価格を継承できる、より上位レベルの価格表。 |
| **階層の深さ** | 最大3つのレベル（フォールバック/子/孫） <br/><br/>取り込み時に適用されません。 |
| **通貨** | フォールバック価格表にのみ定義されます。 すべての児童価格本に継承されます。<br/><br/> フォールバック価格表の作成中に（APIを介して）通貨が指定されていない場合、通貨はデフォルトでUSDになります。 |
| **製品価格** | 特定の価格表の中の製品（SKU）に割り当てられた特定の価格。 |
| **割引** | 割引は商品価格で定義されています。 継承しない。 |

## 価格表の導入

価格表の導入は、Commerceの導入によって異なります。

* サードパーティのCommerce バックエンドを持つAdobe Commerce Optimizer インスタンスでは、価格表はData Ingestion REST APIを使用して作成されます。 Commerce Optimizer Studioのカタログビューワークスペースから割り当てて管理します。

* コンポーザブルカタログデータモデル（CCDM）を使用するAdobe Commerce as a Cloud Serviceでは、価格表はAdobe Commerce カタログと価格表からマッピングされます。 Commerce管理者から各カタログビューに割り当てられた価格表を表示できます。

* Adobe Commerce オンクラウドインフラストラクチャまたはAdobe Commerce Optimizer コネクタを使用したオンプレミスのデプロイメントでは、価格表もAdobe Commerce カタログと価格表データからマッピングされます。 各カタログビューに割り当てられた価格表は、接続されたCommerce Optimizer インスタンスのカタログビューワークスペースから表示できます。

## 価格表を追加

価格表APIを使用して[!DNL Adobe Commerce Optimizer]に価格表を追加します。 [!DNL Adobe Commerce Optimizer]の価格表を作成、更新、削除する方法については、[開発者ドキュメント ](https://developer.adobe.com/commerce/services/reference/rest/)を参照してください。

## 価格表の表示

価格表を[!DNL Adobe Commerce Optimizer]に取り込むと、**カタログ ビュー** ページに価格表のリストと対応するIDが表示されます。

>[!NOTE]
>
>プライベートカタログビュー（[!UICONTROL Catalog Protection]が有効なビュー）は、1つの価格表のみを参照できます。 プライベートカタログビューの[価格表の制限](private-catalog-view.md#price-book-restriction-on-private-catalog-views)を参照してください。

1. _ストア設定_&#x200B;に移動し、**[!UICONTROL Catalog views]**&#x200B;をクリックします。

1. **[!UICONTROL Create catalog view]**&#x200B;をクリックします。 &#x200B;

   カタログビューの詳細を設定で、使用可能な価格表のいずれかを選択します。

   ![価格書名とID](../assets/price-book-name-ids.png)

## 価格表の可用性の設定

各ビューの価格台帳の可用性を設定することで、各カタログビューで使用できる価格データを指定します。

1. **カタログ ビュー** ワークスペースから、設定するカタログ ビューを選択します。

1. 「[!UICONTROL Price Books]」セクションで、価格表オプションを選択して、カタログビューに基づくストアで使用できる価格を設定します。

1. **[!UICONTROL Save]**&#x200B;をクリックして、変更をカタログ ビューに適用します。
