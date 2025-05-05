---
title: '[!DNL Live Search] イベント'
description: イベントで  [!DNL Live Search] のデータを収集する方法を説明します。
feature: Services, Eventing
exl-id: a9f4f254-d8ff-46f1-8deb-a75b90d70d52
source-git-commit: 94d2a9911ab10d164d75779d1f310e5bdf2aea74
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 0%

---

# [!DNL Live Search] イベント

[!DNL Live Search] はイベントを使用して、「最も多く閲覧された」、「これを閲覧し、それを閲覧した」などの検索アルゴリズムを強化します。 [Commerceのサンプル Luma テーマ ](https://experienceleague.adobe.com/ja/docs/commerce-admin/content-design/design/themes/themes#the-default-theme) が標準でイベントを取得する一方で、ヘッドレスやその他のカスタム実装では、独自のニーズに応じてイベントを実装する必要があります。

次の表に、[!DNL Live Search] が使用するイベントについて説明します [ ランキング戦略 ](rules-add.md#intelligent-ranking)。

| ランキング戦略 | イベント | ページ |
| --- | --- | --- |
| 最も頻繁に閲覧された | `page-view`<br>`product-view` | 製品詳細ページ |
| 最も多く購入された | `page-view`<br>`place-order` | 買い物かご/チェックアウト |
| 買い物かごに追加済み | `page-view`<br>`add-to-cart` | 製品詳細ページ <br> 製品一覧ページ <br> 買い物かご <br> お気に入りリスト |
| がこれを表示し、が表示されました | `page-view`<br>`product-view` | 製品詳細ページ |

>[!NOTE]
>
>[!DNL Live Search] 用のためのデータ収集には、個人を特定できる情報（PII）は含まれません。 Cookie ID や IP アドレスなどのすべてのユーザー識別子は、厳密に匿名化されます。 [ 詳細情報 ](https://www.adobe.com/privacy/experience-cloud.html)。

## 必須のダッシュボードイベント

一部のイベントは、[ ライブ検索ダッシュボード ](performance.md) への入力に必要です

| ダッシュボード領域 | イベント | 結合フィールド |
| ------------------- | ------------- | ---------- |
| ユニーク検索 | `page-view`、`search-request-sent`、`search-response-received` | `searchRequestId` |
| ゼロ結果検索 | `page-view`、`search-request-sent`、`search-response-received` | `searchRequestId` |
| ゼロ結果率 | `page-view`、`search-request-sent`、`search-response-received` | `searchRequestId` |
| 一般的な検索 | `page-view`、`search-request-sent`、`search-response-received` | `searchRequestId` |
| 平均 クリック位置 | `page-view`, `search-request-sent`, `search-response-received`, `search-results-view`, `search-product-click` | `searchRequestId` |
| クリックスルー率 | `page-view`, `search-request-sent`, `search-response-received`, `search-results-view`, `search-product-click` | `searchRequestId`、`sku`、`parentSku` |
| コンバージョン率 | `page-view`, `search-request-sent`, `search-response-received`, `search-results-view`, `search-product-click`, `product-view`, `add-to-cart`, `place-order` | `searchRequestId`、`sku`、`parentSku` |

### 必要なコンテキスト

すべてのイベントには、`Page` および `Storefront` コンテキストが必要です。 これは、個々のイベントを生成する場合ではなく、ページレベル/ストアフロントアプリケーションレイヤーで行う必要があります（例えば、PHP ストアフロントでは、PHP アプリケーションコンテナが実行時に設定を行います）。

## 使用状況

`search-request-sent` イベントの実装例を次に示します。

```javascript
const mse = window.magentoStorefrontEvents;

/* set in application container */
// mse.context.page(pageCtx);
// mse.context.setStorefrontInstance(storefrontCtx);

/* set before firing event */
mse.context.setSearchInput(searchInputCtx);
mse.publish.searchRequestSent("search-bar");
```

## 注意事項

- 広告ブロッカーとプライバシー設定は、イベントがキャプチャされるのを防ぎ、エンゲージメントと売上高 [ 指標 ](performance.md) が過小報告される原因になる可能性があります。 さらに、買い物客のページからの離脱やネットワークの問題が原因で、一部のイベントが送信されない場合があります。
- ヘッドレス実装では、インテリジェントなマーチャンダイジングを強化するためにイベンティングを実装する必要があります。

>[!NOTE]
>
>[Cookie 制限モード ](https://experienceleague.adobe.com/docs/commerce-admin/start/compliance/privacy/compliance-cookie-law.html?lang=ja) が有効になっている場合、買い物客が Cookie の使用を同意するまで、Adobe Commerceは行動データを収集しません。 Cookie 制限モードが無効になっている場合、Adobe Commerceはデフォルトで行動データを収集します。
