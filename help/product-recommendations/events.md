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
source-git-commit: 88a0b1a238090dec85e0f79082d264b720999fee
workflow-type: tm+mt
source-wordcount: 937
ht-degree: 0%

---

# Collect Data

[[!DNL Product Recommendations]](install-configure.md)をインストールして設定すると、モジュールは行動データ収集をストアフロントにデプロイします。 このメカニズムは、買い物客から匿名化された行動データを収集し、[!DNL Product Recommendations]を強化します。 例えば、`view` イベントは`Viewed this, viewed that`のレコメンデーションタイプの計算に使用され、`place-order` イベントは`Bought this, bought that`のレコメンデーションタイプの計算に使用されます。

[!DNL Product Recommendations] イベントが収集する行動データについて詳しくは、[開発者ドキュメント ](https://developer.adobe.com/commerce/services/shared-services/storefront-events/#product-recommendations)を参照してください。

>[!NOTE]
>
>[!DNL Product Recommendations]の目的でのデータ収集には、個人を特定できる情報（PII）は含まれません。 Cookie IDやIP アドレスなど、あらゆるユーザーIDは厳密に匿名化されます。 [詳細](https://www.adobe.com/privacy/experience-cloud.html)を学習します。

## 医療業界のユーザー事例

ヘルスケアのお客様で、[Data Connection](../data-connection/overview.md)拡張機能に含まれる[Data Services HIPAA拡張機能](../data-connection/hipaa-readiness.md#installation)をインストールしている場合、[!DNL Product Recommendations]はクライアント側で生成されるため、ストアフロントイベントデータの収集を停止します。

ストアフロントイベントデータの収集と送信を再開するには、[!DNL Product Recommendations]のイベント収集を再度有効にします。 詳しくは、[一般設定](https://experienceleague.adobe.com/en/docs/commerce-admin/config/general/general#data-services)を参照してください。

## データの種類とイベント

商品レコメンデーションでは、次の2種類のデータを使用します。

- **行動** – 商品ビュー、カートに追加された商品、購入など、サイトでの買い物客のエンゲージメントに関するデータ。
- **カタログ** – 商品メタデータ（名前、価格、在庫状況など）。

`magento/product-recommendations` モジュールをインストールすると、Adobe AIは行動データとカタログデータを集計し、レコメンデーションタイプごとに商品レコメンデーションを作成します。 商品レコメンデーションサービスは、推奨された商品&#x200B;_個のアイテム_&#x200B;を含むウィジェットの形式で、これらのレコメンデーションをストアフロントにデプロイします。

レコメンデーションタイプの中には、買い物客の行動データを利用してマシンラーニングモデルをトレーニングし、パーソナライズされたレコメンデーションを生成するものもあります。 カタログデータのみに依存している場合もあります。 商品レコメンデーションをすばやく使用するには、次のカタログのみのレコメンデーションタイプから選択します。

- `More like this`
- `Visual similarity`

### コールドスタート

行動データを活用したレコメンデーションタイプを、いつ頃から使うことができますか？ それは企業によって異なります。 この状況は&#x200B;_コールドスタート_&#x200B;問題と呼ばれます。

_Cold Start_&#x200B;の問題は、マシンラーニングモデルが効果的な推奨事項を生成するためにトレーニングに必要な時間です。 商品レコメンデーションの場合、Adobe AIは、レコメンデーションユニットをデプロイする前に、モデルをトレーニングするのに十分なデータを収集する必要があります。 一般的に、データが多いほど、レコメンデーションの正確性と有用性が向上します。 データ収集はライブサイトで行われるので、`magento/product-recommendations` モジュールをインストールして設定することで、このプロセスを早い段階で開始します。

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

ライブサイトでデータを収集し、マシンラーニングモデルをトレーニングしながら、残りのテストと設定のタスクを完了します。 モデルに十分なデータが揃って有益なレコメンデーションが生成されたら、レコメンデーションユニットをストアフロントにデプロイします。

ほとんどの製品SKUに対して十分なトラフィック（ビュー、購入、トレンド）がサイトに流入しない場合、学習プロセスが完了せず、管理画面の準備状況インジケーターが停止しているように見える可能性があります。 準備状況の指標は、マーチャントがストアに最適なレコメンデーションタイプを選択するのに役立ちますが、それはガイドに過ぎず、100%に達することはありません。 準備状況インジケーターについて詳しく見る。 準備状況インジケーターについて[詳細情報](create.md#readiness-indicators)を表示します。

### バックアップの推奨事項 {#backuprecs}

入力データが不十分な場合、レコメンデーションユニットがリクエストされたアイテムをすべて返さないようにすると、Adobe Commerceはバックアップレコメンデーションを入力します。 例えば、ホームページに`Recommended for you`のレコメンデーションタイプをデプロイした後、初めての買い物客は、パーソナライズされたレコメンデーションに十分な行動データを生成できない可能性があります。 この場合、Adobe Commerceは`Most viewed ` レコメンデーションタイプに基づいてアイテムを表示します。

入力データ収集が不十分な場合、次のレコメンデーションタイプは`Most viewed`個のレコメンデーションタイプにフォールバックします。

- `Recommended for you`
- `Viewed this, viewed that`
- `Viewed this, bought that`
- `Bought this, bought that`
- `Trending`
- `Conversion (view to purchase)`
- `Conversion (view to cart)`

#### 注意事項

- 広告ブロッカーとプライバシー設定により、イベントのキャプチャが妨げられ、エンゲージメントと収益[指標](workspace.md#column-descriptions)が過小報告される可能性があります。 さらに、買い物客がページを離れたり、ネットワーク上の問題が原因でイベントが送信されない場合もあります。
- 商品レコメンデーションダッシュボードを強化するには、[ ヘッドレス実装](headless.md)でイベントを実装する必要があります。
- 設定可能な製品の場合、製品レコメンデーションは親製品の画像を使用します。 親製品に画像がない場合、その製品はレコメンデーションユニットに表示されません。

>[!NOTE]
>
>[Cookie制限モード ](https://experienceleague.adobe.com/en/docs/commerce-admin/start/compliance/privacy/compliance-cookie-law)が有効になっている場合、Adobe Commerceは、買い物客がCookieの使用に同意するまで行動データを収集しません。 Cookie制限モードが無効な場合、Adobe Commerceはデフォルトで行動データを収集します。
