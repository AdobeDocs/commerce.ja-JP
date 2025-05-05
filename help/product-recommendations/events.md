---
title: データを収集
description: イベントで  [!DNL Product Recommendations] のデータを収集する方法を説明します。
feature: Services, Recommendations, Eventing
exl-id: 0d5317e3-c049-4fcd-a8e4-228668d89386
source-git-commit: 94d2a9911ab10d164d75779d1f310e5bdf2aea74
workflow-type: tm+mt
source-wordcount: '1360'
ht-degree: 0%

---

# データを収集

[[!DNL Product Recommendations]](install-configure.md) や [[!DNL Live Search]](../live-search/install.md) などの SaaS ベースのAdobe Commerce機能をインストールして設定する場合、行動データ収集がストアフロントにデプロイされます。 このメカニズムは、匿名化された行動データを買い物客から収集し、[!DNL Product Recommendations] の権限を与えます。 例えば、`view` イベントは `Viewed this, viewed that` レコメンデーションタイプの計算に使用され、`place-order` イベントは `Bought this, bought that` レコメンデーションタイプの計算に使用されます。

>[!NOTE]
>
>[!DNL Product Recommendations] 用のためのデータ収集には、個人を特定できる情報（PII）は含まれません。 Cookie ID や IP アドレスなどのすべてのユーザー識別子は、厳密に匿名化されます。 詳細情報 [ 詳細情報 ](https://www.adobe.com/privacy/experience-cloud.html)。

## ヘルスケア関連のお客様

医療関係のお客様が [ データ接続 ](../data-connection/hipaa-readiness.md#installation) 拡張機能の一部である [ データサービス HIPAA 拡張機能 ](../data-connection/overview.md) をインストールした場合、[!DNL Product Recommendations] で使用されるストアフロントイベントデータは取得されなくなります。 これは、ストアフロントのイベントデータがクライアントサイドで生成されるからです。 引き続きストアフロントのイベントデータのキャプチャと送信を行うには、[!DNL Product Recommendations] のイベント収集を再度有効にします。 詳しくは、[ 一般設定 ](https://experienceleague.adobe.com/en/docs/commerce-admin/config/general/general.html#data-services) を参照してください。

## データタイプとイベント

Product Recommendations で使用されるデータには、次の 2 種類があります。

- **行動** – 製品表示、買い物かごに追加された項目、購入など、サイトに対する買い物客のエンゲージメントからのデータ。
- **カタログ** – 製品メタデータ（名前、価格、在庫状況など）。

`magento/product-recommendations` モジュールをインストールすると、Adobe Senseiは行動データとカタログデータを集計し、レコメンデーションタイプごとに商品レコメンデーションを作成します。 次に、Product Recommendations サービスは、推奨される製品 _項目_ を含むウィジェットの形式で、レコメンデーションをストアフロントにデプロイします。

一部のレコメンデーションタイプでは、買い物客の行動データを使用して機械学習モデルをトレーニングし、パーソナライズされたレコメンデーションを作成します。 その他のレコメンデーションタイプでは、カタログデータのみを使用し、行動データは使用しません。 サイトでの製品レコメンデーションの使用をすぐに開始する場合は、次のカタログのみのレコメンデーションタイプを使用できます。

- `More like this`
- `Visual similarity`

### コールドスタート

行動データを使用するレコメンデーションタイプの使用を開始できるのはいつですか？ 場合によります。 これは、「コールドスタート _問題と呼ば_ ます。

_コールドスタート_ の問題は、モデルがトレーニングを受けて実効を発揮するまでにかかる時間を表します。 商品レコメンデーションの場合、レコメンデーションユニットをサイトにデプロイする前に、Adobe Senseiが機械学習モデルをトレーニングするのに十分なデータを収集するのを待つことになります。 モデルのデータが多いほど、レコメンデーションはより正確で有用になります。 データ収集はライブサイトで行われるので、`magento/production-recommendations` モジュールをインストールして設定し、このプロセスを早期に開始することをお勧めします。

次の表に、各レコメンデーションタイプで十分なデータの収集に要する時間に関する一般的なガイダンスを示します。

| レコメンデーションタイプ | トレーニング時間 | 備考 |
|---|---|---|
| 人気度ベース（`Most viewed`、`Most purchased`、`Most added to cart`） | 可変 | イベントの量に依存 – 表示は最も一般的なので、より迅速に学習されます。その後、買い物かごに追加され、購入されます |
| `Viewed this, viewed that` | さらにトレーニングが必要 | 製品表示の量が急激に多い |
| `Viewed this, bought that`, `Bought this, bought that` | 最も多くのトレーニングが必要 | 購入イベントは、特に製品表示と比較して、コマースサイトで最もまれなイベントです |
| `Trending` | 人気度のベースラインを確立するために 3 日間のデータが必要です | トレンド分析は、製品の人気ベースラインと比較した、製品の人気の最近の勢いの指標です。 製品のトレンドスコアは、フォアグラウンドセット（24 時間にわたる最近の人気度）とバックグラウンドセット（72 時間にわたる人気度のベースライン）を使用して計算されます。 24 時間以内にアイテムの人気度がベースラインの人気度と比較して大幅に上昇した場合、高いトレンドスコアが得られます。 すべての製品にこのスコアがあり、スコアが最も高い項目はいつでも、上位のトレンド製品のセットで構成されます。 |

トレーニングに要する時間に影響を与える可能性があるその他の変数を次に示します。

- トラフィック量が多いほど、学習が速くなります
- 一部のレコメンデーションタイプは、他のタイプよりも高速にトレーニングされます
- Adobe Commerceは 4 時間ごとに行動データを再計算します。 レコメンデーションは、サイトで使用されるほど正確になります。

各推奨タイプのトレーニングの進行状況を視覚化できるように、「[ 推奨を作成 ](create.md#readiness-indicators)」ページに準備状況インジケーターが表示されます。

ライブサイトでデータが収集され、機械学習モデルがトレーニングされている間に、レコメンデーションを設定するために必要な他のテストおよび設定タスクを完了できます。 この作業が完了するまでに、モデルには便利なレコメンデーションを作成するのに十分なデータが含まれており、ストアフロントにモデルをデプロイできます。

ほとんどの製品 SKU でサイトに十分なトラフィック（表示、購入、トレンド）が届かない場合は、学習プロセスを完了するのに十分なデータがない可能性があります。 これにより、管理者の準備インジケーターが動かなくなったように見える場合があります。 準備状況の指標は、店舗にとって優れたレコメンデーションタイプを選択する際に、マーチャントに別のデータポイントを提供することを目的としています。 数値は目安であり、100% に達することはありません。 準備状況インジケーターについて &rbrack;(create.md#readiness-indicators) 詳しくは、[ こちら ] を参照してください。

### バックアップの推奨事項 {#backuprecs}

入力データが不十分で、リクエストされたすべてのレコメンデーションアイテムをユニットで提供できない場合、Adobe Commerceは、レコメンデーションユニットを設定するためのバックアップレコメンデーションを提供します。 例えば、ホームページに `Recommended for you` のレコメンデーションのタイプをデプロイした場合、サイト上で初めて買い物をする人は、パーソナライズされた製品を正確に推奨するのに十分な行動データを生成していません。 この場合、Adobe Commerceは、この買い物客に `Most viewed` のレコメンデーションタイプに基づいて項目を表示します。

入力データの収集が不十分な場合、次のレコメンデーションタイプが `Most viewed` のレコメンデーションタイプにフォールバックします。

- `Recommended for you`
- `Viewed this, viewed that`
- `Viewed this, bought that`
- `Bought this, bought that`
- `Trending`
- `Conversion (view to purchase)`
- `Conversion (view to cart)`

### イベント

[Adobe Commerce ストアフロントイベントコレクター ](https://developer.adobe.com/commerce/services/shared-services/storefront-events/collector/#quick-start) には、ストアフロントにデプロイされたすべてのイベントが一覧表示されます。 このリストには、[!DNL Product Recommendations] に固有のイベントのサブセットがあります。 これらのイベントは、買い物客がストアフロントでレコメンデーションユニットとやり取りする際にデータを収集し、レコメンデーションのパフォーマンスを分析するために指標を強化します。

| イベント | 説明 |
| --- | --- |
| `impression-render` | レコメンデーションユニットがページでレンダリングされる際に送信されます。 ページに 2 つのレコメンデーションユニット（購入済み、表示ビュー）がある場合、2 つの `impression-render` イベントが送信されます。 このイベントは、インプレッション数の指標を追跡するために使用されます。 |
| `rec-add-to-cart-click` | 買い物客は、レコメンデーションユニット内の項目の **買い物かごに追加** ボタンをクリックします。 |
| `rec-click` | 買い物客は、レコメンデーションユニット内の製品をクリックします。 |
| `view` | ページを下にスクロールするなど、レコメンデーションユニットが 50% 以上の表示できるようになると送信されます。 例えば、レコメンデーションユニットに 2 行がある場合、1 行に 2 行目の 1 ピクセルを加えた `view` イプイベントが買い物客に表示されると送信されます。 買い物客がページを上下に複数回スクロールした場合、買い物客がレコメンデーションユニット全体をページ上で再度表示すると、`view` のイベントが何度も送信されます。 |

>[!NOTE]
>
>製品レコメンデーション指標は、Luma ストアフロント用に最適化されています。 ストアフロントがPWA Studioと共に実装されている場合は、[PWAのドキュメント ](https://developer.adobe.com/commerce/pwa-studio/integrations/product-recommendations/) を参照してください。 React や Vue JS などのカスタムフロントエンドテクノロジーを使用する場合は、[Product Recommendations をヘッドレス ](headless.md) 環境に統合する方法を参照してください。

#### 必須のダッシュボードイベント

[[!DNL Product Recommendations] dashboard](workspace.md) に値を入力するには、次のイベントが必要です。

| ダッシュボード列 | イベント | 結合フィールド |
| ---------------- | --------- | ----------- |
| インプレッション | `page-view`, `recs-request-sent`, `recs-response-received`, `recs-unit-render` | `unitId` |
| ビュー | `page-view`, `recs-request-sent`, `recs-response-received`, `recs-unit-render`, `recs-unit-view` | `unitId` |
| クリック数 | `page-view`, `recs-request-sent`, `recs-response-received`, `recs-item-click`, `recs-add-to-cart-click` | `unitId` |
| 収益 | `page-view`, `recs-request-sent`, `recs-response-received`, `recs-item-click`, `recs-add-to-cart-click`, `place-order` | `unitId`、`sku`、`parentSku` |
| 長期収益 | `page-view`, `recs-request-sent`, `recs-response-received`, `recs-item-click`, `recs-add-to-cart-click`, `place-order` | `unitId`、`sku`、`parentSku` |
| CTR | `page-view`, `recs-request-sent`, `recs-response-received`, `recs-unit-render`, `recs-item-click`, `recs-add-to-cart-click` | `unitId`、`sku`、`parentSku` |
| vCTR | `page-view`, `recs-request-sent`, `recs-response-received`, `recs-unit-render`, `recs-unit-view`, `recs-item-click`, `recs-add-to-cart-click` | `unitId`、`sku`、`parentSku` |

次のイベントは、Product Recommendations に固有ではありませんが、Adobe Senseiが買い物客データを正しく解釈するために必要です。

- `view`
- `add-to-cart`
- `place-order`

#### レコメンデーションタイプ

次の表に、各レコメンデーションタイプで使用されるイベントを示します。

| レコメンデーションタイプ | イベント | ページ |
| --- | --- | --- |
| 最も頻繁に閲覧された | `page-view`<br>`product-view` | 製品詳細ページ |
| 最も多く購入された | `page-view`<br>`place-order` | 買い物かご/チェックアウト |
| 買い物かごに追加済み | `page-view`<br>`add-to-cart` | 製品詳細ページ <br> 製品一覧ページ <br> 買い物かご <br> お気に入りリスト |
| がこれを表示し、が表示されました | `page-view`<br>`product-view` | 製品詳細ページ |
| これを閲覧し、次を購入 | 製品のレシピ | `page-view`<br>`product-view` | 製品詳細ページ <br> 買い物かご/チェックアウト |
| これを購入し、それを購入しました | 製品のレシピ | `page-view`<br>`product-view` | 製品詳細ページ |
| トレンド | `page-view`<br>`product-view` | 製品詳細ページ |
| コンバージョン：表示から購入 | 製品のレシピ | `page-view`<br>`product-view` | 製品詳細ページ |
| コンバージョン：表示から購入 | 製品のレシピ | `page-view`<br>`place-order` | 買い物かご/チェックアウト |
| コンバージョン：買い物かごに表示 | 製品のレシピ | `page-view`<br>`product-view` | 製品詳細ページ |
| コンバージョン：買い物かごに表示 | 製品のレシピ | `page-view`<br>`add-to-cart` | 製品詳細ページ <br> 製品リストページ <br> 買い物かご <br> ウィッシュリスト |

#### 注意事項

- 広告ブロッカーとプライバシー設定は、イベントがキャプチャされるのを防ぎ、エンゲージメントと売上高 [ 指標 ](workspace.md#column-descriptions) が過小報告される原因になる可能性があります。 さらに、買い物客のページからの離脱やネットワークの問題が原因で、一部のイベントが送信されない場合があります。
- [ ヘッドレス実装 ](headless.md) 製品レコメンデーションダッシュボードを強化するには、イベンティングを実装する必要があります。
- 設定可能な製品の場合、Product Recommendations では、レコメンデーションユニット内の親製品の画像を使用します。 設定可能な製品に画像が指定されていない場合、その特定の製品のレコメンデーションユニットは空になります。

>[!NOTE]
>
>[Cookie 制限モード ](https://experienceleague.adobe.com/docs/commerce-admin/start/compliance/privacy/compliance-cookie-law.html?lang=ja) が有効になっている場合、買い物客が Cookie の使用を同意するまで、Adobe Commerceは行動データを収集しません。 Cookie 制限モードが無効になっている場合、Adobe Commerceはデフォルトで行動データを収集します。
