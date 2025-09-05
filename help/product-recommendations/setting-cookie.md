---
title: Cookie 制限の処理
description: Cookie 制限およびプライバシーコンプライアンスに関する製品レコメンデーションの処理方法について説明します。
exl-id: 7e7342db-b903-4105-93c0-e4022c81673b
source-git-commit: dbb36b9fa800e128f1aea795a891ffbfb751aa76
workflow-type: tm+mt
source-wordcount: '429'
ht-degree: 0%

---

# Cookie 制限の処理

データがブラウザーの Cookie に保存される前に、Adobe CommerceとMagento Open Sourceの両方が同意を求めます。 詳しくは、「[Cookie 制限モード ](https://experienceleague.adobe.com/docs/commerce-admin/start/compliance/privacy/compliance-cookie-law.html)」を参照してください。

## 製品レコメンデーションによる cookie 制限の処理方法

`magento/product-recommendations` モジュールを実稼動環境にデプロイすると、ストアフロントで買い物客インタラクションイベントの収集が開始されます。 このデータは、ブラウザーの Cookie またはローカルストレージに保存して、レコメンデーションアルゴリズムを強化できます。

>[!IMPORTANT]
>
>Product Recommendations は、Cookie 制限が有効な場合に Cookie やローカルストレージにデータを収集または保存しないことで、Cookie 制限モードを尊重するようになりました。 これには、パーソナライズされたレコメンデーションに使用する行動データが含まれます。

### Cookie 制限の影響を受けるデータ

Cookie 制限モードが有効になっている場合、次の Product Recommendations データは収集されません。

- **行動データ**：製品表示、買い物かごへの追加アクション、購入、その他の買い物客のインタラクション。
- **セッションデータ**：買い物客セッション情報とレコメンデーションユニットのインタラクション。
- **Personalization データ**: 「最近閲覧された」、「最も多く購入された」などのレコメンデーションタイプに使用されるデータ。

### レコメンデーションタイプへの影響

Cookie 制限モードが有効になっていて、買い物客が Cookie を受け入れていない場合、特定のレコメンデーションタイプが表示されないか、結果が限定的になる場合があります。

- **最近表示された製品**:Cookie/ローカルストレージに保存されたセッションデータが必要です。
- **推奨**：パーソナライゼーションのために行動データが必要です。
- **これを購入、それを購入**：購入履歴データが必要です。

>[!NOTE]
>
>「最も多く閲覧」や「視覚的類似性」など、行動データに依存しないレコメンデーションタイプは、cookie 制限が有効になっている場合でも、引き続き正常に機能します。

## サードパーティ cookie 同意ソリューション

Product Recommendations は、サードパーティの cookie 同意ソリューションと自動的に統合されない場合があります。 データ収集が適用されるプライバシー法および規制に準拠していることを確認するのは、マーチャントの責任です。

カスタム cookie 同意ソリューションを使用する場合は、追跡禁止 Cookie メカニズムを実装して、データ収集を制御できます。

### トラッキング対象外 Cookie の実装

`mg_dnt` cookie を使用すると、プログラムによってデータ収集を制御できます。

#### Cookie 名

```javascript
const DNT_COOKIE = "mg_dnt";
```

#### データ収集を無効にする

ユーザーが Cookie を拒否した場合に追跡禁止 Cookie を設定する：

```javascript
$.mage.cookies.set(DNT_COOKIE, true);
```

#### データ収集を有効にする

ユーザーが Cookie を受け入れる際に追跡禁止 Cookie をクリアする：

```javascript
$.mage.cookies.clear(DNT_COOKIE);
```

## cookie 制限モードのテスト

Cookie 制限による製品レコメンデーションの動作をテストするには：

1. Adobe Commerce設定で cookie 制限モードを有効にします。
1. Cookie を受け入れずにストアフロントにアクセスします。
1. レコメンデーションユニットに適切なフォールバックコンテンツが表示されていることを確認します。
1. Cookie を受け入れ、レコメンデーションがデータの収集を開始することを確認します。

## プライバシーコンプライアンス

Product Recommendations のデータ収集には、個人を特定できる情報（PII）は含まれません。 Cookie ID や IP アドレスなどのすべてのユーザー識別子は匿名化されます。 詳しくは、[Adobe プライバシーポリシー ](https://www.adobe.com/privacy/policy.html) を参照してください。

>[!TIP]
>
>データサービス HIPAA 拡張機能を使用している医療関係のお客様の場合は、追加の設定が必要になる場合があります。 詳しくは、[HIPAA 対応 ](../data-connection/hipaa-readiness.md) を参照してください。
