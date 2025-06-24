---
title: 同義語のベストプラクティス
description: ストアで同義語を実装するためのベストプラクティスを説明します。
role: Admin, Developer
badgeSaas: label="SaaS のみ" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud ServiceおよびAdobe Commerce Optimizer プロジェクトにのみ適用されます（Adobeで管理される SaaS インフラストラクチャ）。"
source-git-commit: 54b300ed89f830c2fe5258ec889302a59decd59f
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 0%

---

# 同義語のベストプラクティス

同義語を作成する際のベストプラクティスのリストを次に示します。

- [!DNL Adobe Commerce Optimizer] は、デフォルトでスペルミスを管理します。 同義語を設定すると、買い物客がカタログで指定した単語とは異なる単語を使用する可能性があります。 あなたの製品が「ソファ」としてリストされている間、誰かが「ソファ」を探しているので、あなたは販売を失いたくありません。 顧客が商品の検索に使用する可能性のあるすべての単語を入力することで、様々な検索語句を取り込むことができます。 結果を向上させるには [ 同義語を一方向または双方向として設定 ](add.md#step-2-define-the-synonym-by-type) できます。

- ブランド名および略称をフルネームにマッピングします（「HP」から「Hewlett-Packard」など）。一般的な商品のニックネーム（「iPhone」から「Apple iPhone」など）。

- 業界特有の専門用語や、買い物客が同じ意味で使用する用語（例えば、「スニーカー」や「ランニングシューズ」）を含めます。

- 新しい検索トレンド、製品の追加、買い物客の行動に基づいて、同義語リストを定期的に更新します。

- 検索結果と買い物客のフィードバックを分析して、シノニムマッピングの有効性をテストします。 マッピングを調整して、精度と関連性を向上させます。

- ストップワードは、同義語をより意味のあるものにするのではなく、処理する必要があるデータの量を増やすので、使用しないでください。 [!DNL Adobe Commerce Optimizer] は、次のような一般的な英語の「ストップワード」を同義語から除外します。

  a、an、and、are、as、at、be、but、by、for、if、in、into、is、it、no、not、of、on、or、such、that、the、their、then、there、these、they、this、to、was、will、with

- 単語の単数形と複数形の両方を同義語として定義する必要はありません。 カタログ内の用語が単数と複数の場合、正しい商品セットが検索されます。 例えば、製品名に「pant」という単語を使用し、買い物客が「pants」を検索すると、正しい商品セットが返され、提案として「pant」という単数形の単語が提供されます。 ファッション業界や小売業では単数形の「パンツ」が使われることが多いが、一部の地域では複数形の「パンツ」が一般的に使われている。 （パンツとは厳密には片方の足を覆う衣服の一部を指し、そのため両足を覆う「パンツ」が必要になります。

- カタログ内での用語の使用方法に一貫性を持たせます。 使用には地域による違いがあり、場合によっては業界内でも違いがあることに注意してください。
