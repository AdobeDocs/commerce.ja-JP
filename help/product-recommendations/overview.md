---
title: 概要  [!DNL Product Recommendations]
description: '[!DNL Product Recommendations] は、コンバージョンを増やし、売上高を増やし、買い物客のエンゲージメントを促進するために使用できる、強力なマーケティングツールです。'
recommendations: noCatalog
badgePaas: label="PaaS のみ" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce on Cloud プロジェクト（Adobeが管理する PaaS インフラストラクチャ）およびオンプレミスプロジェクトにのみ適用されます。"
exl-id: 72850cfd-555c-4e0e-ac3e-097e6dac2030
source-git-commit: ae672ed3f2693e2f14e8c7f379e59ef117a34fc3
workflow-type: tm+mt
source-wordcount: '490'
ht-degree: 0%

---

# [!DNL Product Recommendations] の概要

製品レコメンデーションは、コンバージョンを増やし、売上高を増やし、買い物客のエンゲージメントを促進するために使用できる強力なマーケティングツールです。 Adobe Commerceの製品レコメンデーションは、人工知能と機械学習アルゴリズムを使用して集計された訪問者データの詳細な分析を実行する [0}Adobe Sensei} を活用しています。 ](https://www.adobe.com/sensei.html)このデータをAdobe Commerce カタログと組み合わせると、非常に魅力的で関連性が高く、パーソナライズされたエクスペリエンスが実現します。

レコメンデーション商品は、「この商品を閲覧したお客様も閲覧しました」などのラベル付きユニットとしてストアフロントに表示されます。 Adobe Commerce管理者から直接、ストアビュー全体でレコメンデーションを作成、管理およびデプロイできます。

ストアフロントがPWA Studioを使用して実装されている場合は、[PWA ドキュメント ](https://developer.adobe.com/commerce/pwa-studio/integrations/product-recommendations/) を参照してください。 React や Vue JS などのカスタムフロントエンドテクノロジーを使用している場合は、ヘッドレスストアフロントに [ を ](headless.md) 統合 [!DNL Product Recommendations] する方法を説明します。

>[!NOTE]
>
>ヘッドレス実装またはカスタム実装を開発する方法は多数あります。 このガイドでは、PWA Studioを使用した方法の 1 つを説明します。 すべてのシナリオやイベントには対応していません。

## プライバシー

[!DNL Product Recommendations] の目的でのデータ収集には、個人を特定できる情報（PII）は含まれません。 また、Cookie ID や IP アドレスなどのすべてのユーザー識別子は、厳密に匿名化されます。 詳しくは、[Adobeのプライバシーポリシー ](https://www.adobe.com/privacy/policy.html) を参照してください。

デ [!DNL Product Recommendations] タ同期について詳しくは、[ データ管理ダッシュボード ](https://experienceleague.adobe.com/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard.html) を参照してください。

## 製品レコメンデーションと製品の関係

オンラインショッピングの複雑さが絶えず変化していることを考えると、ストアフロントに最適なものは、多くの場合、複数の主要なテクノロジーの組み合わせです。 [!DNL Product Recommendations] と [ 製品の関係 ](https://experienceleague.adobe.com/docs/commerce-admin/marketing/promotions/product-relationships/product-relationships.html) の両方を使用すると、製品のプロモーションをより柔軟に行うことができます。 Adobe Senseiを活用した [!DNL Product Recommendations] を活用して、レコメンデーションを大規模にインテリジェントに自動化できます。 その後、手動で介入して、ターゲットの買い物客セグメントに対して特定のレコメンデーションが行われていることを確認する必要がある場合や、特定のビジネス目標を満たす必要がある場合は、[ 関連製品ルール ](https://experienceleague.adobe.com/docs/commerce-admin/marketing/promotions/product-relationships/product-related-rules.html) を活用できます。

製品レコメンデーションを使用すると、次のことが可能です。

- 買い物客ベース、項目ベース、人気度ベース、トレンド、類似性ベースの領域に基づいて、9 つの異なるインテリジェントレコメンデーションタイプから選択します。
- 行動データを使用して、買い物客のストアフロントジャーニー全体を通してレコメンデーションをパーソナライズします
- 各レコメンデーションに関連する主要指標を測定し、レコメンデーションの影響を理解するのに役立てる

## [!DNL Product Recommendations] デモ

[!DNL Product Recommendations] について詳しくは、このビデオをご覧ください。

>[!VIDEO](https://video.tv.adobe.com/v/343991?quality=12)

## カタログデータ保持ポリシー

テスト環境でカタログデータのクエリを 90 日間連続で送信しない場合、カタログデータは休止モードに設定され、クエリに対してデータが返されません。 実稼動環境のカタログデータは、このポリシーの影響を受けません。

テスト環境でカタログデータを再アクティブ化するには、「[ を再アクティブ化 ](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#experience-league-start-page) というタイトルで [!DNL Product Recommendations] サポートリクエストを送信」し、環境 ID を含めます。 テスト環境のカタログデータは、数時間以内に復元する必要があります。
