---
title: ' [!DNL Product Recommendations]の概要'
description: '[!DNL Product Recommendations]は、コンバージョンの増加、売上の増加、買い物客のエンゲージメントの促進に使用できる強力なマーケティングツールです。'
recommendations: noCatalog
badgePaas: label="PaaSのみ" type="Informative" url="https://experienceleague.adobe.com/ja/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce on Cloud プロジェクト（Adobeで管理されるPaaS インフラストラクチャ）とオンプレミス プロジェクトにのみ適用されます。"
exl-id: 72850cfd-555c-4e0e-ac3e-097e6dac2030
source-git-commit: 1ae6b0f6786375ca4e7bb7620e164008a08f8965
workflow-type: tm+mt
source-wordcount: '641'
ht-degree: 0%

---

# [!DNL Product Recommendations]の概要

商品レコメンデーションは、コンバージョンと売上を向上させ、買い物客のエンゲージメントを促進するための優れたマーケティングツールです。 Adobe Commerceの商品レコメンデーションは、[Adobe AI](https://business.adobe.com/jp/ai.html)によって提供されます。この機能は、人工知能とマシンラーニング（機械学習）のアルゴリズムを使用して、集約された訪問者データを詳細に分析します。 このデータをAdobe Commerceカタログと組み合わせることで、非常に魅力的で関連性の高い、パーソナライズされた体験を生み出すことができます。

>[!IMPORTANT]
>
>**製品レコメンデーションはHIPAA対応サービスではありません。** HIPAA対応の製品を使用するか、保護された健康情報（PHI）を処理するAdobe Commerceの実装では、製品レコメンデーションを有効にしたり、使用したりしないでください。 商品レコメンデーションは、現在HIPAA非対応として分類されているCommerce SaaS サービスの一部です。
>
>どのAdobe Commerce機能がHIPAAに対応しているか、どのサービスをPHIで使用してはならないかについて詳しくは、[Adobe CommerceでのHIPAA対応](https://experienceleague.adobe.com/ja/docs/commerce-admin/start/compliance/hipaa-ready-service/overview)および[操作](https://experienceleague.adobe.com/ja/docs/commerce-admin/start/compliance/hipaa-ready-service/operations#adobe-commerce-services)を参照してください。

商品レコメンデーションは、「この商品を閲覧したお客様も閲覧した」などのラベル付きのユニットとしてストアフロントに表示されます。 Adobe Commerce管理者から直接、ストアビュー全体でレコメンデーションを作成、管理、デプロイできます。

ストアフロントがPWA Studioを使用して実装されている場合は、[PWA ドキュメント &#x200B;](https://developer.adobe.com/commerce/pwa-studio/integrations/product-recommendations/)を参照してください。 ReactやVue JSなどのカスタムフロントエンドテクノロジーを使用する場合は、[&#x200B; ヘッドレスストアフロントに](headless.md) [!DNL Product Recommendations]を統合する方法を説明します。

>[!NOTE]
>
>ヘッドレス実装やカスタム実装を開発する方法はたくさんあります。 このガイドでは、PWA Studioを使用した方法について説明します。 すべてのシナリオや不測の事態を網羅しているわけではありません。

## プライバシー

[!DNL Product Recommendations]の目的でのデータ収集には、個人を特定できる情報（PII）は含まれません。 また、Cookie IDやIP アドレスなどのユーザーIDはすべて厳密に匿名化されています。 詳しくは、[Adobe プライバシーポリシー](https://www.adobe.com/privacy/policy.html)を参照してください。

[!DNL Product Recommendations]人のユーザーは、[&#x200B; データ管理ダッシュボード &#x200B;](https://experienceleague.adobe.com/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard.html?lang=ja)で、データの同期に関する詳細なデータを参照できます。

## 商品レコメンデーションと商品関係

オンラインショッピングの複雑さが絶えず変化していることを考えると、ストアフロントで最も効果的なものは、複数の主要なテクノロジーの組み合わせであることが多いです。 [!DNL Product Recommendations]と[製品関係](https://experienceleague.adobe.com/docs/commerce-admin/marketing/promotions/product-relationships/product-relationships.html?lang=ja)の両方を使用すると、製品のプロモーションをより柔軟に行うことができます。 Adobe AIが提供する[!DNL Product Recommendations]を活用して、大規模なレコメンデーションをインテリジェントに自動化できます。 次に、手動で介入して、ターゲットの買い物客セグメントに対して特定のレコメンデーションが行われていることを確認する必要がある場合、または特定のビジネス目標を達成する必要がある場合は、[関連製品ルール &#x200B;](https://experienceleague.adobe.com/docs/commerce-admin/marketing/promotions/product-relationships/product-related-rules.html?lang=ja)を活用できます。

商品レコメンデーションを活用すると、以下のことが可能になります。

- 買い物客ベース、アイテムベース、人気ベース、トレンド、類似性ベースのエリアに基づいて、9つのインテリジェントなレコメンデーションタイプから選択できます
- 行動データを利用して、ストアフロントジャーニー全体にわたってレコメンデーションをパーソナライズします
- 各レコメンデーションに関連する主要な指標を測定して、レコメンデーションのインパクトを把握できます

## [!DNL Product Recommendations] デモ

[!DNL Product Recommendations]について詳しくは、このビデオをご覧ください。

>[!VIDEO](https://video.tv.adobe.com/v/343991?quality=12)

## カタログデータ保持ポリシー

テスト環境でカタログデータのクエリを90日間連続して送信しない場合、カタログデータは休止モードに設定され、クエリに対してデータは返されません。 実稼動環境内のカタログデータは、このポリシーの影響を受けません。

### 非アクティブなテスト環境

テスト環境でカタログデータを再アクティブ化するには、[&#x200B; サポートリクエスト &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#experience-league-start-page)を「再アクティブ化[!DNL Product Recommendations]」というタイトルで送信し、環境IDを含めます。 テスト環境のカタログデータは、数時間以内に復元する必要があります。

### 空のカタログ

環境に空のカタログが作成されてから45日後に存在する場合、カタログデータは休止モードに設定され、クエリに対してデータは返されません。 これには、実稼動環境とテスト環境の両方が含まれます。

環境でカタログデータを再アクティブ化するには、[&#x200B; サポートリクエスト &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#experience-league-start-page)を「再アクティブ化[!DNL Product Recommendations]」というタイトルで送信し、環境IDを含めます。 環境内のカタログデータは、数時間以内に復元する必要があります。
