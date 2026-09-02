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
source-git-commit: 127067a1ef47c7d9e51c5792e03b568dd818fe8e
workflow-type: tm+mt
source-wordcount: 300
ht-degree: 0%

---

# 製品レコメンデーション管理者開発

商品レコメンデーションは、コンバージョンと売上を向上させ、買い物客のエンゲージメントを促進するための優れたマーケティングツールです。 「この商品を見たお客様も見た」 「この商品を買ったお客様も買った」 「あなたにおすすめ」といったユニット形式で、店頭に商品レコメンデーションを表示しています。 [Adobe AI](https://business.adobe.com/ai.html)は、Adobe Commerceの商品レコメンデーション機能を強化しています。この機能では、AI （人工知能）とマシンラーニング（機械学習）のアルゴリズムを使用して、集約された顧客データを詳細に分析します。 このデータをCommerceカタログと組み合わせることで、買い物客にとって魅力的で関連性の高い、パーソナライズされた体験を実現できます。

>[!NOTE]
>
>ストアフロントがPWA Studioを使用して実装されている場合は、[PWA ドキュメント &#x200B;](https://developer.adobe.com/commerce/pwa-studio/integrations/product-recommendations/)を参照してください。 ReactやVue JSなどのカスタムフロントエンドテクノロジーを使用している場合に、[&#x200B; ヘッドレス &#x200B;](headless.md)環境で商品レコメンデーションを統合する方法について説明します。 ヘッドレスインスタンスは、商品レコメンデーションワークスペースを強化するために、イベントを実装する必要があります。

## 建築の概要

Commerceの商品レコメンデーションの多くは、SaaSとして導入されています。 Commerce側には、イベントコレクターとレコメンデーションレイアウトテンプレートを含むストアフロントと、データサービス、SaaS エクスポートモジュール、管理UIを含むバックエンドが含まれます。 Adobe AIのインテリジェンスサービスは、SaaS面で活用されています。

![製品レコメンデーションアーキテクチャ図](assets/arch-diag-sensei.svg)

インストールと設定が完了すると、レコメンデーションモジュールにより、ストアフロントで行動データを収集できるようになります。 Adobe AIは、このデータをカタログデータと組み合わせて、Recommendations サービスで使用される商品の関連付けを計算します。 その後、管理者UIから直接製品レコメンデーションユニットを作成、管理、デプロイできます。

## 次のステップ

商品レコメンデーションを使い始めるには、次のトピックを読んでください。

- [商品レコメンデーションの導入方法](implementation-workflow.md)

- [製品レコメンデーションのインストールと設定](install-configure.md)

- [商品レコメンデーションの作成](create.md)
