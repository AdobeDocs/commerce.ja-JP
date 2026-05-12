---
title: 製品レコメンデーション管理者開発
description: 商品レコメンデーションのアーキテクチャと開発機能の概要。
exl-id: 5967259e-c531-4fc7-9abd-cc18433fab33
TQID: https://experienceleague.adobe.com/DtPYY7DaB-A7-VyTeXkjL9Y2My-WOQx-9CD-TgrcTmk
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: bbbea26f-9621-49eb-9ab8-e06fb3bbce8c
  - id: c4147b6e-073b-4d3c-9ab1-d60f2f4434ef
source-git-commit: 33cd0e217447351b690646ec8d230f76060a74da
workflow-type: tm+mt
source-wordcount: 319
ht-degree: 0%

---

# 製品レコメンデーション管理者開発

商品レコメンデーションは、コンバージョンと売上を向上させ、買い物客のエンゲージメントを促進するための優れたマーケティングツールです。 商品レコメンデーションは、「この商品を見たお客様も見た」、「この商品を購入されたお客様も購入した」、「あなたにおすすめ」などの単位で店頭に表示されます。 Adobe Commerceの商品レコメンデーションは、[Adobe AI](https://business.adobe.com/ai.html)によって実現されます。この機能では、AI （人工知能）とマシンラーニング（機械学習）のアルゴリズムを使用して、集約された買い物客データを詳細に分析します。 このデータをCommerceカタログと組み合わせることで、買い物客にとって魅力的で関連性の高い、パーソナライズされた体験を実現できます。

>[!NOTE]
>
>ストアフロントがPWA Studioを使用して実装されている場合は、[PWA ドキュメント &#x200B;](https://developer.adobe.com/commerce/pwa-studio/integrations/product-recommendations/)を参照してください。 ReactやVue JSなどのカスタムフロントエンドテクノロジーを使用する場合は、ユーザーガイドを参照して、[&#x200B; ヘッドレス &#x200B;](headless.md)環境で商品レコメンデーションを統合する方法について説明します。 ヘッドレスインスタンスは、商品レコメンデーションワークスペースを強化するために、イベントを実装する必要があります。

## 建築の概要

Commerceの商品レコメンデーションの多くは、SaaSとして導入されています。 Commerce側には、イベントコレクターとレコメンデーションレイアウトテンプレートを含むストアフロントと、データサービス、SaaS エクスポートモジュール、管理UIを含むバックエンドが含まれます。 Adobe AIのインテリジェンスサービスは、SaaS面で活用されています。

![製品レコメンデーションアーキテクチャ図](assets/arch-diag-sensei.svg)

レコメンデーションモジュールをインストールして設定すると、ストアフロントは行動データの収集を開始します。 Adobe AIでは、この行動データとカタログデータを処理し、recommendations サービスで活用される商品の関連付けを計算します。 この時点で、マーチャントは管理UIから直接、商品レコメンデーションユニットを作成、管理し、ストアフロントにデプロイできます。

## 次のステップ

商品レコメンデーションを使い始めるには、次のトピックを読んでください。

- [商品レコメンデーションの導入方法](implementation-workflow.md)

- [製品レコメンデーションのインストールと設定](install-configure.md)

- [商品レコメンデーションの作成](create.md)
