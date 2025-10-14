---
title: シノニム・タイプ
description: ' [!DNL Adobe Commerce Optimizer] の様々なタイプの同義語について説明します。'
badgeSaas: label="SaaS のみ" type="Positive" url="https://experienceleague.adobe.com/ja/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud ServiceおよびAdobe Commerce Optimizer プロジェクトにのみ適用されます（Adobeで管理される SaaS インフラストラクチャ）。"
source-git-commit: 3131cc27a25d1bf958071b973f1d4bf1a68be152
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 0%

---

# シノニムのタイプ

一方向同義語と双方向同義語は、キーワードの定義を拡大します。 キーワードに置き換えられる場合もあれば、キーワードのサブセットを表す場合もあります。

## 双方向

双方向同義語は同じ意味を持ち、同じ検索結果を返します。 次の例では、太字で示されている最初の単語はカタログで使用されるキーワードであり、その後に元のキーワードと同じ意味を持つ単語が続きます。 単純な双方向同義語のペアを作成することも、同じキーワードに対して複数の双方向同義語のチェーンを作成することもできます。

**ジャケット**![&#x200B; 双方向セレクター &#x200B;](../../assets/btn-two-way.png) コート
**パンツ**![&#x200B; 双方向セレクター &#x200B;](../../assets/btn-two-way.png) スラックス ![&#x200B; 双方向セレクター &#x200B;](../../assets/btn-two-way.png) ズボン

## 一方向

一方向の同義語は、キーワードのサブセットですが、より具体的な意味を持ちます。 例えば、カプリスとショートパンツはパンツですが、すべてのパンツがカプリスやショートパンツというわけではありません。 パンツの検索には、カプリスとショートパンツが含まれています。 ただし、ショートパンツを検索してもカプリスは返されません。

**sweatshirt**![&#x200B; 一方向セレクター &#x200B;](../../assets/btn-one-way.png) パーカー
**パンツ**![&#x200B; 一方向セレクター &#x200B;](../../assets/btn-one-way.png) カプリス ![&#x200B; 複数一方向セレクター &#x200B;](../../assets/btn-multiple-one-way.png) ふくらはぎ長パンツ ![&#x200B; 複数一方向セレクター &#x200B;](../../assets/btn-multiple-one-way.png) ペドルプッシャー

## 複数ワードの同義語の動作

複数の単語の同義語の場合、[!DNL Adobe Commerce Optimizer] は同義語をフレーズとみなします。 例えば、双方向同義語 **ダイニングルームテーブル**![&#x200B; 双方向セレクター &#x200B;](../../assets/btn-two-way.png)**キッチンテーブル**![&#x200B; 双方向セレクター &#x200B;](../../assets/btn-two-way.png)**ダイニングテーブル** を作成した場 [!DNL Adobe Commerce Optimizer]、すべてのフィールドで検索が可能に設定され、**ダイニングルームテーブル** または **キッチンテーブル** または **ダイニングテーブル** が発生したとします。

同義語が作成されず、買い物客が **kitchen table** を検索す [!DNL Adobe Commerce Optimizer] と、検索可能なフィールドの任意の場所で用語が検索されます。例えば、name フィールドに **table**、meta キーワードに **kitchen** など、異なるフィールド間でも検索されます。

同義語を作成した後、検索動作が変わり、正確な語句 **キッチンテーブル** が検索されます。 これにより、完全に一致する語句を含んだ製品のみが表示されるので、結果の数が減少する可能性があります。

以前と同様に用語を個別に検索する場合は、[&#x200B; サポートチケットを作成 &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide) できます。 需要が十分な場合は、今後のリリース [!DNL Adobe Commerce Optimizer] この機能を製品に追加することを検討します。
