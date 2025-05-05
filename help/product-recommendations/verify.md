---
title: イベント収集の検証
description: 行動データがAdobe Commerceに送信されていることを確認する方法を説明します。
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '420'
ht-degree: 0%

---

# イベント収集の検証

`magento/product-recommendations` モジュールを [ インストールおよび設定 ](install-configure.md) した後、行動データがAdobe Commerceに送信されていることを確認できます。 Chromeで利用可能な開発者ツールを使用するか、Snowplow Chrome拡張機能をインストールできます。 追加のヘルプが必要な場合は、サポートナレッジベースの [ トラブルシューティング  [!DNL Product Recommendations]  モジュール ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/troubleshoot-product-recommendations-module-in-magento-commerce.html?lang=ja) を参照してください。

## Chromeのデベロッパーツールを使用した検証

イベントコレクター JS ファイルがすべてのサイトページに読み込まれていることを確認するには：

1. Chromeで、「**Google Chromeをカスタマイズして制御する**」を選択し、**その他のツール**/**開発者ツール** を選択します。
1. 「**ネットワーク**」タブを選択し、**JS** タイプを選択します。
1. `ds.` のフィルター
1. ページをリロードします。
1. **Name** 列に `ds.js` または `ds.min.js` が表示されます。

![ イベントコレクター JS](assets/filter-ds.png)
_イベント コレクター JS_

サイト全体（ホーム、製品、チェックアウトなど）でイベントが発生していることを確認するには：

1. ブラウザーで広告ブロッカーを無効にし、サイトの Cookie を受け入れてください。
1. Chromeで、「**Google Chromeのカスタマイズと制御**」（ブラウザーの右上隅にある 3 つの縦並びのドット）を選択し、**その他のツール**/**開発者ツール** を選択します。
1. 「**ネットワーク**」タブを選択し、`tp2` のフィルターを適用します。
1. ページをリロードします。
1. **Name** 列の `tp2` の下に呼び出しが表示されます。

![ イベントの実行 ](assets/filter-tp2.png)
_イベントが発生していることを確認_

## Snowplow Chrome拡張機能を使用した検証

[Chrome用 Snowplow Analytics デバッガー拡張機能 ](https://chrome.google.com/webstore/detail/snowplow-analytics-debugg/jbnlcgeengmijcghameodeaenefieedm) をインストールします。 この拡張機能は、収集されてAdobe Commerceに送信されるイベントを表示します。

1. ブラウザーで広告ブロッカーを無効にし、サイトの Cookie を受け入れてください。

1. Chromeで、「**Google Chromeのカスタマイズと制御**」（ブラウザーの右上隅にある 3 つの縦並びのドット）を選択し、**その他のツール**/**開発者ツール** を選択します。

1. 「**Snowplow Analytics デバッガー**」タブを選択します。

1. **イベント** 列の下で、「**構造化イベント**」を選択します。

1. **コンテキストデータ _n_**&#x200B;が表示されるまで下にスクロールします。**スキーマ**&#x200B;でストアフロントインスタンスを探します。

1. [SaaS Data Space ID](https://experienceleague.adobe.com/docs/commerce-admin/config/services/saas.html?lang=ja) が正しく設定されていることを確認します。

![ 除雪機フィルタ ](assets/snowplow-filter.png)
_除雪機フィルタ_

>[!NOTE]
>
> デバッガーの値 `Data validity : NOT FOUND` は内部スキーマを示します。 Snowplow Chrome プラグインは、内部スキーマでイベントを検証できません。 実際の機能には影響はありません。

## イベントが正しく実行されていることを確認

指標に使用されるイベントが正しく実行されていることを確認するには、Snowplow Analytics デバッガーで `impression-render`、`view`、`rec-click` の各イベントを探します。 [ イベントの完全なリスト ](https://experienceleague.adobe.com/docs/commerce/product-recommendations/developer/events.html?lang=ja) を参照してください。

>[!NOTE]
>
> [Cookie 制限モード ](https://experienceleague.adobe.com/docs/commerce-admin/start/compliance/privacy/compliance-cookie-law.html?lang=ja) が有効になっている場合、Adobe Commerceは、買い物客が同意するまで行動データを収集しません。 Cookie 制限モードが無効になっている場合、行動データがデフォルトで収集されます。
