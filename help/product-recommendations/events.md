---
title: Collect Data
description: イベントが [!DNL Product Recommendations]のデータを収集する方法を説明します。
feature: Services, Recommendations, Eventing
exl-id: 0d5317e3-c049-4fcd-a8e4-228668d89386
TQID: https://experienceleague.adobe.com/efHRMj3u3w-xvUgMnEYDpX0D-BDCUyjhhrkMaa3n-xg
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: d1e21356-0064-4f48-9089-16e3f0dbd2a6id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: c4147b6e-073b-4d3c-9ab1-d60f2f4434efid: d3cdead0-685a-4489-9250-4bb709942f66id: eb30f47f-d87a-400f-8f78-63ce7979ff56id: f4e6943a-c91a-4134-a2c7-f4f20cfff2f0
source-git-commit: 33cd0e217447351b690646ec8d230f76060a74da
workflow-type: tm+mt
source-wordcount: 1019
ht-degree: 0%

---

# Collect Data

[[!DNL Product Recommendations]](install-configure.md)をインストールして設定すると、モジュールは行動データ収集をストアフロントにデプロイします。 このメカニズムは、買い物客から匿名化された行動データを収集し、[!DNL Product Recommendations]を強化します。 例えば、`view` イベントは`Viewed this, viewed that`のレコメンデーションタイプの計算に使用され、`place-order` イベントは`Bought this, bought that`のレコメンデーションタイプの計算に使用されます。

[!DNL Product Recommendations] イベントが収集する行動データについて詳しくは、[開発者ドキュメント ](https://developer.adobe.com/commerce/services/shared-services/storefront-events/#product-recommendations)を参照してください。

>[!NOTE]
>
>[!DNL Product Recommendations]の目的でのデータ収集には、個人を特定できる情報（PII）は含まれません。 Cookie IDやIP アドレスなど、あらゆるユーザーIDは厳密に匿名化されます。 [詳細](https://www.adobe.com/privacy/experience-cloud.html)を学習します。

## 医療業界のユーザー事例

ヘルスケアのお客様で、[Data Connection](../data-connection/overview.md)拡張機能の一部である[Data Services HIPAA拡張機能](../data-connection/hipaa-readiness.md#installation)をインストールした場合、[!DNL Product Recommendations]によって使用されるストアフロントイベントデータはキャプチャされなくなります。 これは、ストアフロントのイベントデータがクライアントサイドで生成されるためです。 ストアフロントイベントデータの取得と送信を続行するには、[!DNL Product Recommendations]のイベント収集を再度有効にします。 詳しくは、[一般設定](https://experienceleague.adobe.com/en/docs/commerce-admin/config/general/general#data-services)を参照してください。

## データの種類とイベント

商品レコメンデーションでは、次の2種類のデータを使用します。

- **行動** – 商品ビュー、カートに追加された商品、購入など、サイトでの買い物客のエンゲージメントに関するデータ。
- **カタログ** – 商品メタデータ（名前、価格、在庫状況など）。

`magento/product-recommendations` モジュールをインストールすると、Adobe AIは行動データとカタログデータを集計し、レコメンデーションタイプごとに商品レコメンデーションを作成します。 商品レコメンデーションサービスは、推奨された商品&#x200B;_個のアイテム_&#x200B;を含むウィジェットの形式で、これらのレコメンデーションをストアフロントにデプロイします。

レコメンデーションタイプによっては、買い物客の行動データを活用してマシンラーニングモデルをトレーニングし、パーソナライズされたレコメンデーションを作成するものもあります。 その他のレコメンデーションタイプでは、カタログデータのみを使用し、行動データは使用しません。 サイトで商品レコメンデーションをすばやく使用する場合は、次のカタログのみのレコメンデーションタイプを使用できます。

- `More like this`
- `Visual similarity`

### コールドスタート

行動データを活用したレコメンデーションタイプを、いつ頃から使うことができますか？ それは企業によって異なります。 これは&#x200B;_コールドスタート_&#x200B;問題と呼ばれます。

_Cold Start_&#x200B;の問題は、モデルのトレーニングと効果の実現にかかる時間を指します。 商品レコメンデーションの場合、Adobe AIがマシンラーニングモデルのトレーニングに十分なデータを収集するのを待ってから、レコメンデーションユニットをサイトに展開します。 モデルに含まれるデータが多ければ多いほど、レコメンデーションはより正確で有用になります。 データ収集はライブサイトで行われるので、`magento/production-recommendations` モジュールをインストールして設定することで、早い段階でこのプロセスを開始することをお勧めします。

次の表に、各レコメンデーションタイプに十分なデータを収集するのにかかる時間に関する一般的なガイダンスを示します。

| レコメンデーションタイプ | トレーニング時間 | メモ |
|---|---|---|
| 人気ベース （`Most viewed`、`Most purchased`、`Most added to cart`） | Varies | イベントの量に依存します – ビューは最も一般的であり、したがって迅速に学習します。次にカートに追加してから購入します |
| `Viewed this, viewed that` | より多くのトレーニングが必要 | 製品ビューは適度に多くなっています |
| `Viewed this, bought that`, `Bought this, bought that` | 最もトレーニングが必要 | 購入イベントは、コマースサイトで最もまれなイベントです。特に、商品ビューと比較すると重要です |
| `Trending` | 人気のベースラインを確立するには3日間のデータが必要です | トレンドとは、製品の人気が、自社の人気ベースラインと比較した際の最近の勢いを示す指標です。 製品のトレンドスコアは、前景セット（最近の人気度が24時間を超える）と背景セット（人気度のベースラインが72時間を超える）を使用して計算されます。 ベースラインの人気度と比較して、24時間以内に商品の人気度が大幅に増加すると、高いトレンドスコアが得られます。 あらゆる商品にこのスコアがあり、いつでも最もスコアの高い商品は、最もトレンドの商品のセットで構成されています。 |

トレーニングに必要な時間に影響を与える可能性があるその他の変数：

- トラフィック量の増加が学習の高速化に貢献
- レコメンデーションタイプによっては、他のタイプよりも学習が速いものもあります
- Adobe Commerceは、行動データを4時間ごとに再計算します。 レコメンデーションは、サイトで長く使用するにつれて精度が向上します。

各レコメンデーションタイプのトレーニングの進捗状況を視覚化するために、[ レコメンデーションの作成](create.md#readiness-indicators) ページには準備状況インジケーターが表示されます。

ライブサイトでデータを収集し、マシンラーニングモデルをトレーニングしている間に、レコメンデーションの設定に必要なその他のテストや設定タスクを完了できます。 この作業が完了する頃には、モデルには有用なレコメンデーションを作成するのに十分なデータが揃っており、ストアフロントに展開することができます。

多くの商品SKUで十分なトラフィック（閲覧数、購入数、トレンド）をサイトで獲得できなければ、学習プロセスを完了するのに十分なデータがない可能性があります。 これにより、管理者の準備状況インジケーターが停止しているように見える場合があります。 準備状況インジケーターは、店舗に適したレコメンデーションタイプを選択するためのデータポイントを加盟店に提供することを目的としています。 数字はガイドであり、100%に達することはありません。 準備状況インジケーターについて[詳細情報](create.md#readiness-indicators)を表示します。

### バックアップの推奨事項 {#backuprecs}

入力データがユニット内のすべてのリクエスト済みレコメンデーション項目を提供するのに不十分な場合、Adobe Commerceはレコメンデーション単位を設定するためのバックアップ レコメンデーションを提供します。 例えば、`Recommended for you`のレコメンデーションタイプをホームページにデプロイした場合、サイトで初めて購入する顧客は、パーソナライズされた商品を正確にレコメンデーションするのに十分な行動データを生成できていません。 この場合、Adobe Commerceは、この買い物客に`Most viewed`のレコメンデーションタイプに基づいて商品を表示します。

入力データ収集が不十分な場合、次のレコメンデーションタイプは`Most viewed`個のレコメンデーションタイプにフォールバックします。

- `Recommended for you`
- `Viewed this, viewed that`
- `Viewed this, bought that`
- `Bought this, bought that`
- `Trending`
- `Conversion (view to purchase)`
- `Conversion (view to cart)`

#### 注意事項

- 広告ブロッカーとプライバシー設定により、イベントのキャプチャが妨げられ、エンゲージメントと収益[指標](workspace.md#column-descriptions)が過小報告される可能性があります。 さらに、買い物客がページを離れたり、ネットワーク上の問題が原因で、イベントが送信されない場合もあります。
- 商品レコメンデーションダッシュボードを強化するには、[ ヘッドレス実装](headless.md)でイベントを実装する必要があります。
- 設定可能な製品の場合、製品レコメンデーションでは、レコメンデーションユニット内の親製品の画像を使用します。 設定可能な製品に画像が指定されていない場合、その製品のレコメンデーションユニットは空になります。

>[!NOTE]
>
>[Cookie制限モード ](https://experienceleague.adobe.com/docs/commerce-admin/start/compliance/privacy/compliance-cookie-law.html)が有効になっている場合、Adobe Commerceは、買い物客がCookieの使用に同意するまで行動データを収集しません。 Cookie制限モードが無効な場合、Adobe Commerceはデフォルトで行動データを収集します。
