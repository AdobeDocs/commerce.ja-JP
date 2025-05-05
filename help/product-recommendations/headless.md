---
title: ヘッドレス
description: ヘッドレスストアフロント  [!DNL Product Recommendations]  統合する方法について説明します。
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 0%

---

# ヘッドレス

[PWA Studio](https://developer.adobe.com/commerce/pwa-studio/) または React や Vue JS などのカスタムフロントエンドテクノロジーを使用して、[!DNL Product Recommendations] をヘッドレスストアフロントに統合できます。

カスタムおよびヘッドレスインテグレーターは、これらの Luma とPWAの手順を実装の推奨事項として参照する必要があります。 ヘッドレスソリューションに Product Recommendations を実装する方法は多数ありますが、このドキュメントでは、すべてのシナリオについて説明しているわけではありません。 インテグレーターは、実装のイベント、設計、テストをカバーする必要があります。

操作 [!DNL Product Recommendations] には [ 行動データとカタログデータ ](https://experienceleague.adobe.com/docs/commerce/product-recommendations/developer/development-overview.html) が必要です。 カタログデータの同期プロセスはヘッドレス実装でも変更されませんが、行動データの収集には変更が必要です。

>[!NOTE]
>
>ヘッドレスインスタンスでは、Product Recommendations ダッシュボードを強化するためにイベントを実装する必要があります。

[!DNL Product Recommendations] をヘッドレスストアフロントに統合するには、次の操作を行う必要があります。

1. 行動データをAdobe Senseiに送信し、製品のレコメンデーション結果を分析および計算します。 また、追加データを送信して、製品レコメンデーション [ 指標レポート ](workspace.md) を有効にすることもできます。

1. 製品の推奨結果を取得し、その結果をページにレンダリングします。

次のワークフローに説明するように、使用可能な SDK を使用して、これらのアクションの両方を実行できます。

1. [!DNL Product Recommendations] モジュール [&#128279;](install-configure.md) インストールします。

1. [Adobe Commerce Storefront Event SDK](https://developer.adobe.com/commerce/services/shared-services/storefront-events/sdk/) をインストールして使用し、[ 行動イベント ](https://experienceleague.adobe.com/docs/commerce/product-recommendations/developer/events.html) を発生させます。

   結果を返すために必要な最小イベント数 [!DNL Product Recommendations] 次のとおりです。

   | イベント | カテゴリ |
   |--- | ---|
   | `view` | 製品 |
   | `add-to-cart` | 製品 |
   | `place-order` | チェックアウト |

   [ 指標レポート ](workspace.md) を有効にするには、次の追加イベントが必要です。

   | イベント | カテゴリ |
   |--- | ---|
   | `impression-render` | recommendation-unit |
   | `view` | recommendation-unit |
   | `rec-click` | recommendation-unit |
   | `rec-add-to-cart-click` | recommendation-unit （レコメンデーションテンプレートに「買い物かごに追加」ボタンが存在する場合） |

1. イベントが発生したら、[Adobe Commerce Storefront Event Collector](https://developer.adobe.com/commerce/services/shared-services/storefront-events/collector/) を使用してイベントを処理し、Adobe Senseiに送信します。

1. 行動データが収集されたら、管理者で [ 作成 ](create.md) [!DNL Product Recommendations] できます。

1. [Recommendations SDK](https://developer.adobe.com/commerce/services/product-recommendations/) を使用して、ストアフロントのレコメンデーションユニットを取得します。 SDKは、レコメンデーションユニットをページにレンダリングするために必要な商品データを返します。
