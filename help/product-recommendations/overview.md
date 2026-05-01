---
title: 商品レコメンデーションとは？
description: Adobe Commerceの商品レコメンデーションの詳細。 AIを活用したストアフロント単位、プライバシー、管理者とストアフロントのパス、主要なデータ保持をご確認ください。
recommendations: noCatalog
exl-id: 72850cfd-555c-4e0e-ac3e-097e6dac2030
source-git-commit: 6bfc2c0ed53b44fb30a142dc87f87dca8a601a33
workflow-type: tm+mt
source-wordcount: '738'
ht-degree: 0%

---

# [!DNL Product Recommendations]とは

[!DNL Product Recommendations]は、[Adobe AI](https://business.adobe.com/jp/ai.html)とマシンラーニングを使用して、Adobe Commerce ストアフロントでパーソナライズされた商品レコメンデーションを表示する際に、集約された買い物客の行動とカタログに関して役立ちます。 この概要では、サービスの制約（HIPAAを含む）、データおよびプライバシー、レコメンデーション単位の表示場所、ストアフロントの実装パス、レコメンデーションが製品関係をどのように補完するか、カタログデータの保持について説明します。

>[!IMPORTANT]
>
>**[!DNL Product Recommendations]はHIPAA対応サービスではありません。** HIPAA対応のオファーを使用するか、保護されたヘルス情報（PHI）を処理するAdobe Commerceの実装では、[!DNL Product Recommendations]を有効にしたり、使用したりしないでください。 [!DNL Product Recommendations]は、現在、非HIPAA対応として分類されているCommerce SaaS サービスの一部です。
>
>どのAdobe Commerce機能がHIPAAに対応しているか、どのサービスをPHIで使用してはならないかについて詳しくは、[Adobe CommerceでのHIPAA対応](https://experienceleague.adobe.com/ja/docs/commerce-admin/start/compliance/hipaa-ready-service/overview)および[操作](https://experienceleague.adobe.com/ja/docs/commerce-admin/start/compliance/hipaa-ready-service/operations#adobe-commerce-services)を参照してください。

## データの取り扱いとプライバシー

[!DNL Product Recommendations]のデータ収集には、個人を特定できる情報（PII）が含まれていません。 Cookie IDやIP アドレスなどのユーザーIDはすべて厳密に匿名化されます。 詳しくは、[Adobe プライバシーポリシー](https://www.adobe.com/privacy/policy.html)を参照してください。

データの同期について詳しくは、[&#x200B; データ管理ダッシュボード &#x200B;](https://experienceleague.adobe.com/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard.html?lang=ja)を参照してください。

## レコメンデーションの表示場所

「この商品を閲覧したお客様も閲覧した」などのラベルが付いたユニットとして、ストアフロントにレコメンデーションが表示されます。 Adobe Commerce管理者から、ストアビュー全体でレコメンデーションを作成、管理、デプロイできます。 Commerce プロジェクトで[Adobe Commerce Optimizer コネクタ &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce/aco-optimizer-connector/overview)を使用している場合、[Adobe Commerce Optimizer](../optimizer/overview.md)を通じてレコメンデーションを作成、管理、デプロイします。

## ストアフロントの導入

ストアフロントに一致するドキュメントを選択します。

- **PWA Studio** — [PWA ドキュメント &#x200B;](https://developer.adobe.com/commerce/pwa-studio/integrations/product-recommendations/)
- **カスタムフロントエンド（ReactまたはVue.jsなど）** — [&#x200B; ヘッドレスストアフロントに [!DNL Product Recommendations]](headless.md)統合
- **Commerce Edge Delivery Services （EDS）** — EDS[&#128279;](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/?lang=ja)のAdobe Commerce Storefront ドキュメント

>[!NOTE]
>
>ヘッドレスおよびカスタムの設定は、スタックによって異なります。 この製品領域では、PWA Studioのパスと一般的なヘッドレス統合パターンを文書化します。すべてのサードパーティやカスタムのシナリオをカバーしているわけではありません。

## 商品レコメンデーションと商品関係

オンラインショッピングの複雑さが絶えず変化していることを考えると、ストアフロントで最も効果的なものは、複数の主要なテクノロジーの組み合わせであることが多いです。 [!DNL Product Recommendations]と[製品関係](https://experienceleague.adobe.com/docs/commerce-admin/marketing/promotions/product-relationships/product-relationships.html?lang=ja)の両方を使用すると、製品のプロモーションをより柔軟に行うことができます。 Adobe AIが提供する[!DNL Product Recommendations]を活用して、大規模なレコメンデーションをインテリジェントに自動化できます。 次に、手動で介入して、ターゲットの買い物客セグメントに対して特定のレコメンデーションが行われていることを確認する必要がある場合、または特定のビジネス目標を達成する必要がある場合は、[関連製品ルール &#x200B;](https://experienceleague.adobe.com/docs/commerce-admin/marketing/promotions/product-relationships/product-related-rules.html?lang=ja)を活用できます。

商品レコメンデーションを活用すると、以下のことが可能になります。

- 買い物客ベース、アイテムベース、人気ベース、トレンド、類似性ベースのエリアに基づいて、9つのインテリジェントなレコメンデーションタイプから選択できます
- 行動データを利用して、ストアフロントジャーニー全体にわたってレコメンデーションをパーソナライズします
- 各レコメンデーションに関連する主要な指標を測定して、レコメンデーションのインパクトを把握できます

## 商品レコメンデーション

[!DNL Product Recommendations]について詳しくは、このビデオをご覧ください。

>[!VIDEO](https://video.tv.adobe.com/v/3449926?captions=jpn&quality=12)

## カタログデータ保持ポリシー

[!DNL Product Recommendations] サービスは、お使いのAdobe Commerce環境と常に同期しているカタログデータに依存します。 非アクティブなカタログまたはデータのクエリを停止する環境では、休止状態に入る可能性があります。これは、再アクティブ化するまでサービスが返す内容に影響します。

**testing**&#x200B;環境のカタログデータに対して90日間連続でクエリを送信しない場合、カタログデータは休止状態モードに設定され、どのクエリにもデータは返されません。 **実稼動**&#x200B;環境内のカタログデータは、90日ルールの影響を受けません。

環境の作成後45日後に&#x200B;**空のカタログ**&#x200B;がある場合、カタログデータは休止状態モードに設定され、クエリに対してデータは返されません。 これは実稼動環境とテスト環境の両方に適用されます。

### カタログデータの再アクティブ化

休止後にカタログデータを復元するには、[&#x200B; サポートリクエスト &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#experience-league-start-page)を「再アクティブ化[!DNL Product Recommendations]」というタイトルで送信し、環境IDを含めます。 カタログデータは数時間以内に復元する必要があります。
