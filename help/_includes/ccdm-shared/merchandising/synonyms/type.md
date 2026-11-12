---
source-git-commit: 18c4528fade63545415135808d2d40ac2b95e86d
workflow-type: tm+mt
source-wordcount: '347'
ht-degree: 0%
---
一方向および双方向の類義語は、キーワードの定義を拡大します。 キーワードと互換性のあるものもあれば、キーワードのサブセットを表すものもあります。

## 双方向

双方向の類義語は同じ意味を持ち、同じ検索結果を返します。 次の例では、太字で示されている最初の単語は、カタログで使用されるキーワードで、その後に元のキーワードと同じ意味を持つ単語が続きます。 同じキーワードに対して、単純な双方向の類義語のペア、または複数の双方向の類義語のチェーンを作成できます。

**ジャケット** ![双方向セレクター](/help/assets/ccdm-shared/synonyms/two-way.png) コート
**パンツ** ![双方向セレクター](/help/assets/ccdm-shared/synonyms/two-way.png)は![双方向セレクター](/help/assets/ccdm-shared/synonyms/two-way.png) ズボンを緩めます

## 一方向

一方向の同義語は、キーワードのサブセットですが、より具体的な意味を持ちます。 例えば、カプリスとショートパンツはパンツですが、すべてのパンツがカプリスやショートパンツであるわけではありません。 「パンツ」はカプリス、「ショーツ」などが検索で検索された。 ただし、ショートの検索ではcaprisは返されません。

**スウェットシャツ** ![片道セレクター](/help/assets/ccdm-shared/synonyms/one-way.png) パーカー
**パンツ** ![一方向セレクター](/help/assets/ccdm-shared/synonyms/one-way.png) カプリス ![一方向セレクター](/help/assets/ccdm-shared/synonyms/one-way.png)ふくらはぎの長さのパンツ ![一方向セレクター](/help/assets/ccdm-shared/synonyms/one-way.png) ペドルプッシャー

## 複数の単語の類義語動作

複数の単語の類義語の場合、システムは類義語をフレーズと見なします。 例えば、双方向の同義語&#x200B;**ダイニングルームテーブル** ![双方向セレクター](/help/assets/ccdm-shared/synonyms/two-way.png) **キッチンテーブル** ![双方向セレクター](/help/assets/ccdm-shared/synonyms/two-way.png) **ダイニングテーブル**&#x200B;を作成した場合、システムは&#x200B;**ダイニングルームテーブル**&#x200B;または&#x200B;**キッチンテーブル**&#x200B;または&#x200B;**ダイニングテーブル**&#x200B;の出現を検索できるように設定されたすべてのフィールドを検索します。

同義語が作成されておらず、買い物客が&#x200B;**kitchen table**&#x200B;を検索すると、システムは、検索フィールド内の任意の場所で、検索フィールドを検索します。例えば、「名前」フィールドの&#x200B;**table**、meta キーワードの&#x200B;**kitchen**&#x200B;などです。

同義語を作成すると、検索動作が変更され、厳密なフレーズ **キッチンテーブル**&#x200B;が検索されます。 正確なフレーズが付いた商品のみが表示されるため、結果の数が減少する可能性があります。

以前と同様に条件を個別に検索する場合は、[ サポートチケットを作成できます](https://experienceleague.adobe.com/en/docs/support-resources/adobe-support-tools-guide/adobe-commerce-support/adobe-commerce-help-center-user-guide)。
