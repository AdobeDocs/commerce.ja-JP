---
title: Cookie制限への対応
description: 商品レコメンデーションがCookie制限とプライバシーコンプライアンスをどのように処理するかをご確認ください。
exl-id: 7e7342db-b903-4105-93c0-e4022c81673b
TQID: https://experienceleague.adobe.com/qqgwO4KI4koSBcYu9mdrjb6AQFW4guxk6dfLDBEwVb8
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2:
  - id: c4147b6e-073b-4d3c-9ab1-d60f2f4434ef
  - id: d3cdead0-685a-4489-9250-4bb709942f66
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
  - id: f4e6943a-c91a-4134-a2c7-f4f20cfff2f0
source-git-commit: 33cd0e217447351b690646ec8d230f76060a74da
workflow-type: tm+mt
source-wordcount: 454
ht-degree: 0%

---

# Cookie制限への対応

Adobe CommerceとMagento Open Sourceは、データがブラウザーCookieに保存される前に、同意を求めます。 詳しくは、[Cookie制限モード &#x200B;](https://experienceleague.adobe.com/docs/commerce-admin/start/compliance/privacy/compliance-cookie-law.html?lang=ja)を参照してください。

## 商品レコメンデーションでのCookie制限の処理方法

`magento/product-recommendations` モジュールを実稼動環境にデプロイすると、ストアフロントで買い物客インタラクションイベントの収集が開始されます。 このデータはブラウザーのCookieまたはローカルストレージに保存して、レコメンデーションアルゴリズムに利用できます。

>[!IMPORTANT]
>
>製品レコメンデーションは、Cookie制限が有効になっている場合に、Cookieまたはローカルストレージにデータを収集または保存しないことにより、Cookie制限モードを尊重するようになりました。 これには、パーソナライズされたレコメンデーションに使用された行動データが含まれます。

### Cookie制限の影響を受けるデータ

Cookie制限モードが有効になっている場合、次の製品レコメンデーションデータは収集されません。

- **行動データ**：商品ビュー、カートへの追加アクション、購入、その他の買い物客とのやり取り。
- **セッションデータ**：買い物客のセッション情報とレコメンデーションユニットのインタラクション。
- **Personalization data**: 「最近閲覧した」や「購入済み」などのレコメンデーションタイプに使用されるデータ。

### レコメンデーションの種類への影響

Cookie制限モードが有効になっていて、買い物客がCookieを受け入れていない場合、特定のレコメンデーションタイプが表示されないか、結果が制限される場合があります。

- **最近閲覧した商品**: Cookie/ローカルストレージに保存されているセッションデータが必要です。
- **おすすめ**: パーソナライゼーションには行動データが必要です。
- **これを購入しました。購入履歴データが必要です。**

>[!NOTE]
>
>「最も閲覧された」や「視覚的な類似性」など、行動データに依存しないレコメンデーションタイプは、Cookie制限が有効になっている場合でも、引き続き正常に動作します。

## サードパーティ Cookie同意ソリューション

商品レコメンデーションは、サードパーティのCookie同意ソリューションと自動的に統合されない場合があります。 データ収集が適用されるプライバシー法や規制を確実に遵守することは、販売者の責任です。

カスタム Cookie同意ソリューションを使用する場合は、データ収集を制御するトラッキング不可Cookie メカニズムを実装できます。

### Do-not-track Cookieの実装

`mg_dnt` Cookieを使用して、プログラムでデータ収集を制御できます。

#### Cookie名

```javascript
const DNT_COOKIE = "mg_dnt";
```

#### データ収集の無効化

ユーザーがCookieを拒否する場合のトラッキング不可Cookieを設定します。

```javascript
$.mage.cookies.set(DNT_COOKIE, true);
```

#### データ収集の有効化

ユーザーがCookieを受け入れたときにトラッキング不可Cookieを消去します。

```javascript
$.mage.cookies.clear(DNT_COOKIE);
```

## Cookie制限モードのテスト

商品レコメンデーションがCookie制限でどのように動作するかをテストするには：

1. Adobe Commerce設定でCookie制限モードを有効にします。
1. Cookieを受け入れずにストアフロントにアクセス。
1. レコメンデーションユニットに適切なフォールバックコンテンツが表示されていることを確認します。
1. Cookieを受け入れ、レコメンデーションがデータの収集を開始することを確認します。

## プライバシーコンプライアンス

商品レコメンデーション データ収集には、個人を特定できる情報（PII）は含まれません。 Cookie IDやIP アドレスなど、あらゆるユーザーIDは匿名化されます。 詳しくは、[Adobe プライバシーポリシー](https://www.adobe.com/privacy/policy.html)を参照してください。

>[!TIP]
>
>Data Services HIPAA拡張機能を使用するヘルスケアのお客様の場合、追加の設定が必要になる場合があります。 詳しくは、[HIPAA対応](../data-connection/hipaa-readiness.md)を参照してください。
