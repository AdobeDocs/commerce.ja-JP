---
title: 行動イベント
description: 各行動イベントがキャプチャするデータを説明します。
role: Admin, Developer
feature: Personalization, Integration, Eventing
exl-id: bcabccc9-8a2e-4045-9306-1d999bb75624
source-git-commit: 631dfacd26a333e70a70f354d191d256d90d946f
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 0%

---

# [!DNL Data Connection] 行動イベント

以下に、[!DNL Data Connection] 拡張機能のインストール時に使用できるCommerceの行動イベントを示します。 これらのイベントで収集されたデータは、Adobe Experience Platformに送信されます。 また、[ カスタムイベント ](custom-events.md) を作成して、初期設定では提供されていない追加のデータを収集することもできます。

次のイベントで収集されるデータに加えて、Adobe Experience Platform web SDKから提供される [ その他のデータ ](https://experienceleague.adobe.com/docs/experience-platform/edge/data-collection/automatic-information.html) も取得します。

行動イベントは、サイトを閲覧する買い物客から匿名化された行動データを収集します。 これらのイベントで収集されたデータを使用して、特定の買い物客のセットをターゲットとしたプロモーションやキャンペーンを作成できます。

>[!NOTE]
>
>すべての行動イベントには、買い物客のメールアドレス（使用可能な場合）や ECID を含む「[`identityMap`](https://experienceleague.adobe.com/docs/experience-platform/xdm/field-groups/profile/identitymap.html)」フィールドが含まれます。

## ストアフロントイベント

ストアフロントイベントは、サイト上での買い物客のインタラクションからデータをキャプチャし、`addToCart`、`pageView`、`createAccount`、`editAccount`、`startCheckout`、`completeCheckout`、`signIn`、`signOut` などのイベントを含みます。 ストアフロントイベントは、シンプルで設定可能な製品にのみ適用されます。

ストアフロントイベントについて詳しくは、[ 開発者向けドキュメント ](https://developer.adobe.com/commerce/services/shared-services/storefront-events/#data-connection) を参照してください。

## 顧客プロファイルイベント

ストアフロントから取得したプロファイルイベントには、`signIn`、`signOut`、`createAccount`、`editAccount` などのアカウント情報が含まれます。 このデータは、新規登録割引オファーの送信、アカウント変更の確認など、セグメントを適切に定義したり、マーケティングキャンペーンを実行したりするために必要な、主な顧客詳細の入力に使用されます。

顧客プロファイルイベントについて詳しくは、[ 開発者向けドキュメント ](https://developer.adobe.com/commerce/services/shared-services/storefront-events/#data-connection) を参照してください。

## イベントを検索

検索イベントは、買い物客の意図に関連するデータを提供します。 買い物客の意図へのInsightは、買い物客が商品をどのように検索しているか、何をクリックしているか、そして最終的に購入または放棄するかをマーチャントが確認するのに役立ちます。 このデータの使用方法の例として、上位の製品を検索しても製品を購入しない既存の買い物客をターゲットにする場合があります。 これらのイベントにアクセスするには、[[!DNL Live Search]](../live-search/install.md) 拡張機能をインストールする必要があります。

`searchRequest.id` イベントと `searchResponse.id` イベントの両方にある `searchRequestSent` フィールドと `searchResponseReceived` フィールドを使用して、検索リクエストを対応する検索応答に相互参照します。

検索イベントについて詳しくは、[ 開発者ドキュメント ](https://developer.adobe.com/commerce/services/shared-services/storefront-events/#data-connection) を参照してください。

## B2B イベント

Adobe Commerceの ![B2B](../assets/b2b.svg) B2B マーチャントの場合、これらのイベントにアクセスするには、[ 拡張機能を ](install.md#install-the-b2b-extension) インストール `experience-platform-connector-b2b` する必要があります。

B2B イベントには、購買依頼リストが作成、追加または削除されたかどうかなど、[ 購買依頼リスト ](https://experienceleague.adobe.com/docs/commerce-admin/b2b/requisition-lists/requisition-lists.html) 情報が含まれます。 購買依頼リストに固有のイベントを追跡することで、顧客が頻繁に購入する製品を確認し、そのデータに基づいてキャンペーンを作成できます。

B2B イベントについて詳しくは、[ 開発者向けドキュメント ](https://developer.adobe.com/commerce/services/shared-services/storefront-events/#data-connection) を参照してください。
