---
title: 価格台帳
description: ' [!DNL Adobe Commerce Optimizer] で価格台帳を管理する方法を説明します。'
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="SaaS のみ" type="Positive" url="https://experienceleague.adobe.com/ja/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud ServiceおよびAdobe Commerce Optimizer プロジェクトにのみ適用されます（Adobeで管理される SaaS インフラストラクチャ）。"
source-git-commit: 553490762ef10e43ccce1654acec59aeb83bb5f9
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 0%

---

# 価格台帳

この記事では、適切なデータガバナンス制御を使用して、価格台帳を定義し、カタログ表示に割り当てる方法について説明します。

Price Book API を使用してサードパーティシステムから [!DNL Adobe Commerce Optimizer] に価格台帳情報を取り込む方法については、[ 開発者向けドキュメント ](https://developer-stage.adobe.com/commerce/services/composable-catalog/data-ingestion/api-reference/#tag/Price-Books) を参照してください。

価格台帳を使用すると、価格設定カタログ・ソースを定義して、様々な顧客層および市場にわたる製品価格を管理できます。 価格台帳は階層モデルをサポートしており、各ベース価格台帳の下にネストされた子価格台帳を最大 3 レベルまで作成できます。 各価格台帳は、親価格台帳を参照し、価格設定カタログ・ソースのツリー構造を形成できます。

基本価格台帳では、それ自体とすべての子価格台帳に対して通貨が定義されます。 子の価格帳簿はこの通貨を継承し、上書きすることはできません。

## 主要な概念

| 用語 | 説明 |
|------|-------------|
| **価格台帳** | 価格カタログのソース （特定の地域、顧客層など）を定義する論理グループ化で、製品価格の管理に使用されます。 |
| **フォールバック価格台帳** | 階層内で最上位の価格台帳。 親がなく、それ自体とすべての下位価格帳簿の通貨を定義する *唯一* 価格帳簿です。<br/><br/> 価格台帳の作成中に親が定義されていない場合（API を介して）、新しいフォールバック価格台帳が作成されます。 |
| **親価格台帳** | 子供が明示的に設定されていない場合に、子供の価格台帳が価格を継承できる高レベルの価格台帳。 |
| **階層の深度** | 最大 3 レベル（フォールバック→子→孫） <br/><br/> 取り込み時に適用されません。 |
| **通貨** | フォールバック価格帳簿でのみ定義されます。 すべての子供に継承され、価格本。<br/><br/> フォールバック価格台帳の作成時に（API を通じて）通貨を指定しない場合、通貨はデフォルトで USD になります。 |
| **製品価格** | 特定の価格台帳内で製品（SKU）に割り当てられた特定の価格。 |
| **割引** | 割引は製品価格で定義されます。 継承されません。 |
