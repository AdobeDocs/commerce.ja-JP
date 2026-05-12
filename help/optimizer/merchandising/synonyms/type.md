---
title: 同義語タイプ
description: ' [!DNL Adobe Commerce Optimizer]の様々な類義語について説明します。'
badgeSaas: label="SaaSのみ" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud Serviceおよび [!DNL Adobe Commerce Optimizer]  プロジェクトにのみ適用されます（Adobeで管理されるSaaS インフラストラクチャ）。"
exl-id: a74e48ea-e069-4ccc-a67f-2f85be251fb5
TQID: https://experienceleague.adobe.com/23kmFWLruZeFMxIjKZJKbs0y9q10DDtbFG8ioLC5U-o
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
topic_v2:
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 33cd0e217447351b690646ec8d230f76060a74da
workflow-type: tm+mt
source-wordcount: 393
ht-degree: 0%

---

# 類義語の種類

一方向および双方向の類義語は、キーワードの定義を拡大します。 キーワードと互換性のあるものもあれば、キーワードのサブセットを表すものもあります。

## 双方向

双方向の類義語は同じ意味を持ち、同じ検索結果を返します。 次の例では、太字で示されている最初の単語は、カタログで使用されるキーワードで、その後に元のキーワードと同じ意味を持つ単語が続きます。 同じキーワードに対して、単純な双方向の類義語のペア、または複数の双方向の類義語のチェーンを作成できます。

**ジャケット** ![双方向セレクター](../../assets/two-way.png) コート
**パンツ** ![双方向セレクター](../../assets/two-way.png)は![双方向セレクター](../../assets/two-way.png) ズボンを緩めます

## 一方向

一方向の同義語は、キーワードのサブセットですが、より具体的な意味を持ちます。 例えば、カプリスとショートパンツはパンツですが、すべてのパンツがカプリスやショートパンツであるわけではありません。 「パンツ」はカプリス、「ショーツ」などが検索で検索された。 ただし、ショートの検索ではcaprisは返されません。

**スウェットシャツ** ![片道セレクター](../../assets/one-way.png) パーカー
**パンツ** ![一方向セレクター](../../assets/one-way.png) カプリス ![一方向セレクター](../../assets/one-way.png)ふくらはぎの長さのパンツ ![一方向セレクター](../../assets/one-way.png) ペドルプッシャー

## 複数の単語の類義語動作

複数の単語の類義語の場合、[!DNL Adobe Commerce Optimizer]は類義語をフレーズと見なします。 例えば、双方向の同義語&#x200B;**ダイニングルームテーブル** ![双方向セレクター](../../assets/two-way.png) **キッチンテーブル** ![双方向セレクター](../../assets/two-way.png) **ダイニングテーブル**&#x200B;を作成した場合、[!DNL Adobe Commerce Optimizer]はすべてのフィールドを検索して、**ダイニングルームテーブル**&#x200B;または&#x200B;**キッチンテーブル**&#x200B;または&#x200B;**ダイニングテーブル**&#x200B;が見つかるように設定されています。

同義語が作成されておらず、買い物客が&#x200B;**kitchen table**&#x200B;を検索すると、[!DNL Adobe Commerce Optimizer]は検索可能なフィールドの任意の場所で用語を検索します。例えば、「名前」フィールドの&#x200B;**table**、meta キーワードの&#x200B;**kitchen**&#x200B;などです。

同義語を作成すると、検索動作が変更され、厳密なフレーズ **キッチンテーブル**&#x200B;が検索されます。 正確なフレーズが付いた商品のみが表示されるため、結果の数が減少する可能性があります。

以前と同様に条件を個別に検索する場合は、[&#x200B; サポートチケットを作成できます](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide)。 十分な需要がある場合、[!DNL Adobe Commerce Optimizer]は、今後のリリースでこの機能を製品に追加することを検討します。
