---
title: 統合の制限と境界
description: サードパーティカタログの範囲の制限、自動修正の範囲、クロールの前提条件、エンタープライズ規模に関する考慮事項、LLM OptimizerとCommerceの制限付きベータアクセスの制約について説明します。
role: Admin, User, Leader
recommendations: noCatalog
badgePaas: label="PaaSのみ" type="Informative" url="https://experienceleague.adobe.com/ja/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce on Cloud プロジェクト（Adobeで管理されるPaaS インフラストラクチャ）とオンプレミス プロジェクトにのみ適用されます。"
source-git-commit: 47348a44ff7c5f890c10594f44cae6e771be046f
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 0%

---

# 統合の制限と境界

>[!IMPORTANT]
>
>この統合へのアクセスは制限されています。 詳しくは、テクニカルアカウントマネージャーにお問い合わせください。

このトピックでは、[!DNL Adobe Commerce]と[!DNL Adobe LLM Optimizer]の統合で自動化できる機能、責任を維持する場所、まだ進化している制約について、期待値を設定します。

## サードパーティカタログの制限 {#third-party-catalog}

カタログ **が[!DNL Adobe Commerce]に存在しない**&#x200B;場合：

- LLM Optimizerでは、設定に応じて、ミラーまたはインポートされたカタログデータを使用して問題を特定し、改善を提案することができます。
- 加盟店のコマースプラットフォームに&#x200B;**直接自動修正**&#x200B;を追加することと、加盟店のソースカタログに書き込むことは同じではありません。 変更を適用するには、ミラーカタログ、書き出し/読み込み、またはパートナーの自動化が必要になる場合があります。

Commerceでホストされているカタログの場合、承認済みの名前と説明の更新は、Commerce記録システムに送信されます。 [Adobe CommerceでLLM Optimizerを使用する](get-started/use-llmo-with-commerce.md)を参照してください。

## 拡大と技術的な限界 {#scale-limits}

カタログが大きくURL数が多い場合、クロール、分析、エッジ展開のパターンに負担がかかる可能性があります。

## クロールとボットの読みやすさ {#crawling}

有意義なカタログとPDPのインサイトは、LLM関連の&#x200B;**ボットが重要なURLに** アクセスでき、ページが構造化されているため、自動分析の信頼性が高いと仮定します。 ロボットルール、認証、ジオブロッキング、高度なパーソナライゼーションにより、カバー範囲を縮小することができます。

## 関連トピック

- [統合の概要](overview.md)
- [Adobe CommerceとLLM Optimizerの連携](get-started/connect-to-llmo.md)
- [Adobe CommerceでのLLM Optimizerの使用](get-started/use-llmo-with-commerce.md)
