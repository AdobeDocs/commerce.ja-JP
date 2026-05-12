---
title: 同義語のベストプラクティス
description: ストアに類義語を実装するためのベストプラクティスについて説明します。
role: Admin, Developer
badgeSaas: label="SaaSのみ" type="Positive" url="https://experienceleague.adobe.com/ja/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud Serviceおよび [!DNL Adobe Commerce Optimizer]  プロジェクトにのみ適用されます（Adobeで管理されるSaaS インフラストラクチャ）。"
exl-id: 026bb17b-14e3-4493-ae10-376837b69de6
TQID: https://experienceleague.adobe.com/2ktYgzsiM-BvHEJNeu0-XkxhgDThHVuXMnDux3Fb9WA
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 33cd0e217447351b690646ec8d230f76060a74da
workflow-type: tm+mt
source-wordcount: 433
ht-degree: 0%

---

# 同義語のベストプラクティス

次に、類義語を作成する際のベストプラクティスのリストを示します。

- [!DNL Adobe Commerce Optimizer]はスペルの間違いを既定で管理します。 カタログで指定した単語とは異なる、買い物客が使用する可能性のある単語を含めるように類義語を設定できます。 誰かが「ソファ」を探している間に、製品が「ソファ」としてリストされているので、販売を失いたくありません。 顧客が自社商品を探す際に使用する可能性のあるあらゆる単語を入力することで、幅広い検索語を取得できます。 [類義語を1つの方法または2つの方法](add.md#step-2-define-the-synonym-by-type)として設定して、結果を改善できます。

- ブランド名と略語をフルネームにマッピングします（例：「HP」、「Hewlett-Packard」、「iPhone」、「Apple iPhone」など）。

- 「スニーカー」や「ランニングシューズ」など、業界固有の用語や、買い物客が区別せずに使用する可能性のある用語を含めます。

- 新しい検索トレンド、商品の追加、買い物客の行動にもとづいて、類義語リストを定期的に更新します。

- 検索結果と買い物客のフィードバックを分析することで、類義語マッピングの効果をテストできます。 マッピングを調整して、精度と関連性を向上させます。

- ストップワードは、類義語をより意味のあるものにするのではなく、処理する必要があるデータの量を増やします。 [!DNL Adobe Commerce Optimizer]は、類義語から一般的な英語の「ストップ ワード」を除外します。例えば、次のようになります。

  a, an, and, are, at, be, but, by, for, for, in, is, it, no, not, of, on, or, such, that, the, their, then, then, there, these, they, this, to, was, with, with

- 単語の単一形と複数形の両方を同義語として定義する必要はありません。 カタログに単一語と複数語が混在している場合、検索で正しい商品セットが見つかります。 例えば、商品名に「pant」という単語を使用し、買い物客が「pants」と検索した場合、正しい商品セットが返され、「pant」という単語が候補として提示されます。 単数形の「パンツ」は、ファッション業界や小売業界でよく使用されますが、複数形の「パンツ」は一部の地域でより一般的に使用されています。 （パンツという言葉は技術的には、片足を覆う衣服の部分を指します。そのため、両足を覆うために「パンツのペア」が必要です。

- カタログ内で使用する用語と一貫性を持たせます。 使用には地域ごとの違いがあり、業界内でも時には違いがあることに留意してください。
