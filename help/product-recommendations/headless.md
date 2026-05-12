---
title: ヘッドレス
description: ヘッドレスストアフロントに [!DNL Product Recommendations] を統合する方法について説明します。
exl-id: c40dac31-f87e-402a-ba50-e8aa4c1d66aa
TQID: https://experienceleague.adobe.com/J3qXs-SWuDCz7pQwzGm0VcOOFoU1QM2M4qwsTxxPwE8
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: f42e0a1a-0d79-488d-a83f-f2c30672b137
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: c4147b6e-073b-4d3c-9ab1-d60f2f4434ef
  - id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 33cd0e217447351b690646ec8d230f76060a74da
workflow-type: tm+mt
source-wordcount: 372
ht-degree: 0%

---

# ヘッドレス

[!DNL Product Recommendations]は、[PWA Studio](https://developer.adobe.com/commerce/pwa-studio/)またはReactやVue JSなどのカスタムフロントエンドテクノロジーを使用して、ヘッドレスストアフロントに統合できます。

カスタムインテグレーターおよびヘッドレスインテグレーターは、これらのLumaおよびPWAの手順を推奨される実装として参照する必要があります。 ヘッドレスソリューションに製品レコメンデーションを実装する方法はたくさんあり、このドキュメントではすべてのシナリオを説明しません。 インテグレーターは、実装のイベント、設計、テストをカバーする必要があります。

[!DNL Product Recommendations]を操作するには[行動データとカタログデータ &#x200B;](https://experienceleague.adobe.com/docs/commerce/product-recommendations/developer/development-overview.html?lang=ja)が必要です。 カタログデータの同期プロセスはヘッドレス実装でも変更されませんが、行動データの収集には変更が必要です。

>[!NOTE]
>
>ヘッドレスインスタンスは、商品レコメンデーションダッシュボードを強化するために、イベントを実装する必要があります。

[!DNL Product Recommendations]をヘッドレスストアフロントに統合するには、次の手順を実行する必要があります。

1. 行動データをAdobe AIに送信し、商品レコメンデーションの結果を分析して計算します。 追加データを送信して、商品レコメンデーション [指標レポート &#x200B;](workspace.md)を有効にすることもできます。

1. 商品レコメンデーションの結果を取得し、その結果をページに表示できます。

次のワークフローの説明に従って、使用可能なSDKを使用して、これらのアクションの両方を実行できます。

1. [!DNL Product Recommendations] モジュールを[&#x200B; インストール &#x200B;](install-configure.md)。

1. [Adobe Commerce Storefront Event SDK](https://developer.adobe.com/commerce/services/shared-services/storefront-events/sdk/)をインストールして使用し、[行動イベント &#x200B;](https://developer.adobe.com/commerce/services/shared-services/storefront-events/#product-recommendations)を実行します。

   [!DNL Product Recommendations]件の結果を返すために必要な最小イベント：

   | イベント | カテゴリ |
   |--- | ---|
   | `view` | product |
   | `add-to-cart` | product |
   | `place-order` | チェックアウト |

   [指標レポート &#x200B;](workspace.md)を有効にするには、次の追加イベントが必要です。

   | イベント | カテゴリ |
   |--- | ---|
   | `impression-render` | recommendation-unit |
   | `view` | recommendation-unit |
   | `rec-click` | recommendation-unit |
   | `rec-add-to-cart-click` | recommendation-unit （レコメンデーションテンプレートに「カートに追加」ボタンがある場合） |

1. イベントが発生したら、[Adobe Commerce Storefront Event Collector](https://developer.adobe.com/commerce/services/shared-services/storefront-events/collector/)を使用してイベントを処理し、Adobe AIに送信します。

1. 行動データを収集した後、管理者で[create](create.md) [!DNL Product Recommendations]できます。

1. [Recommendations SDK](https://developer.adobe.com/commerce/services/product-recommendations/)を使用して、ストアフロントのレコメンデーションユニットを取得します。 SDKは、ページ上にレコメンデーションユニットをレンダリングするために必要な商品データを返します。

1. [`recommendations` GraphQL クエリ &#x200B;](https://developer.adobe.com/commerce/webapi/graphql/schema/product-recommendations/queries/recommendations/)を使用して、特定のSKUの商品レコメンデーションブロックに関する情報を返す方法を説明します。
