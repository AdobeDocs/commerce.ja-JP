---
title: シノニムのタイプ
description: 一方向同義語と双方向同義語を使用すると  [!DNL Live Search]  キーワードの定義が拡張されます。
exl-id: f5522428-c7cc-4627-a09b-d9148918c127
source-git-commit: 81bde302463a70e41318b494565694929703dff9
workflow-type: tm+mt
source-wordcount: '581'
ht-degree: 0%

---

# シノニムのタイプ

一方向同義語と双方向同義語は、キーワードの定義を拡大します。 キーワードに置き換えられる場合もあれば、キーワードのサブセットを表す場合もあります。

## 双方向

双方向同義語は同じ意味を持ち、同じ検索結果を返します。 次の例では、太字で示されている最初の単語はカタログで使用されるキーワードであり、その後に元のキーワードと同じ意味を持つ単語が続きます。 単純な双方向同義語のペアを作成することも、同じキーワードに対して複数の双方向同義語のチェーンを作成することもできます。

**ジャケット**![ 双方向セレクター ](assets/btn-two-way.png) コート
**パンツ**![ 双方向セレクター ](assets/btn-two-way.png) スラックス ![ 双方向セレクター ](assets/btn-two-way.png) ズボン

## 一方向

一方向の同義語は、キーワードのサブセットですが、より具体的な意味を持ちます。 例えば、カプリスとショートパンツはパンツですが、すべてのパンツがカプリスやショートパンツというわけではありません。 パンツの検索には、カプリスとショートパンツが含まれています。 ただし、ショートパンツを検索してもカプリスは返されません。

**sweatshirt**![ 一方向セレクター ](assets/btn-one-way.png) パーカー
**パンツ**![ 一方向セレクター ](assets/btn-one-way.png) カプリス ![ 複数一方向セレクター ](assets/btn-multiple-one-way.png) ふくらはぎ長パンツ ![ 複数一方向セレクター ](assets/btn-multiple-one-way.png) ペドルプッシャー

## ベストプラクティス

同義語を最大限に活用するには、次のベストプラクティスに注意 [!DNL Live Search] てください。

### ストップワードの回避

[!DNL Live Search] は、次のような一般的な英語の「ストップワード」を同義語から除外します。

a、an、and、are、as、at、be、but、by、for、if、in、into、is、it、no、not、of、on、or、such、that、the、their、then、there、these、they、this、to、was、will、with

ストップワードは、同義語をより意味のあるものにするのではなく、処理する必要があるデータの量を増やします。

### 単数および複数形の使用

単語の単数形と複数形の両方を同義語として定義する必要はありません。 カタログ内の用語が単数と複数の場合、正しい商品セットが検索されます。 例えば、製品名に「pant」という単語を使用し、買い物客が「pants」を検索すると、正しい商品セットが返され、提案として「pant」という単数形の単語が提供されます。 ファッション業界や小売業では単数形の「パンツ」が使われることが多いが、一部の地域では複数形の「パンツ」が一般的に使われている。 （パンツとは厳密には片方の足を覆う衣服の一部を指し、そのため両足を覆う「パンツ」が必要になります。

### 一貫性

カタログ内での用語の使用方法に一貫性を持たせます。 使用には地域による違いがあり、場合によっては業界内でも違いがあることに注意してください。

## 複数ワードの同義語の動作

複数語の同義語の場合、Commerceは同義語をフレーズと見なします。 例えば、双方向同義語 **ダイニングルームテーブル**![ 双方向セレクター ](assets/btn-two-way.png)**キッチンテーブル**![ 双方向セレクター ](assets/btn-two-way.png)**ダイニングテーブル** を作成した場合、Commerceは検索可能に設定されたすべてのフィールドで **ダイニングルームテーブル**、**キッチンテーブル** または **ダイニングテーブル** を検索します。

同義語が作成されず、買い物客が **kitchen table** を検索する場合、Commerceは、検索可能なフィールドの任意の場所で用語を検索します。例えば、name フィールドに **table**、meta キーワードに **kitchen** など、異なるフィールド間でも検索されます。

同義語を作成した後、検索動作が変わり、正確な語句 **キッチンテーブル** が検索されます。 これにより、完全に一致する語句を含んだ製品のみが表示されるので、結果の数が減少する可能性があります。

以前と同様に用語を個別に検索する場合は、[ サポートチケットを作成 ](https://experienceleague.adobe.com/ja/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide) できます。 十分な需要がある場合、Commerceは将来のリリースでこの機能を製品に追加することを検討します。
