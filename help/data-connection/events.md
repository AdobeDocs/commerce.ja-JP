---
title: 行動イベント
description: 各行動イベントがどのようなデータを取得するかをご確認ください。
role: Admin, Developer
feature: Personalization, Integration, Eventing
exl-id: bcabccc9-8a2e-4045-9306-1d999bb75624
TQID: https://experienceleague.adobe.com/YS3jKQ3jmy76aeaqAp1PR8cGpD0euagdhoqL6CoMAnQ
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: c4147b6e-073b-4d3c-9ab1-d60f2f4434ef
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 33cd0e217447351b690646ec8d230f76060a74da
workflow-type: tm+mt
source-wordcount: 467
ht-degree: 0%

---

# [!DNL Data Connection]行動イベント

次に、[!DNL Data Connection]拡張機能のインストール時に使用できるCommerce行動イベントを示します。 これらのイベントで収集されたデータは、Adobe Experience Platformに送信されます。 [&#x200B; カスタムイベント &#x200B;](custom-events.md)を作成して、標準提供されていない追加データを収集することもできます。

次のイベントが収集するデータに加えて、Adobe Experience Platform Web SDKが提供する[その他のデータ &#x200B;](https://experienceleague.adobe.com/docs/experience-platform/edge/data-collection/automatic-information.html)も取得できます。

行動イベントは、サイトを閲覧する顧客から、匿名化された行動データを収集します。 イベントで収集したデータを活用して、特定の買い物客をターゲットにしたプロモーションや施策を構築できます。

>[!NOTE]
>
>すべての行動イベントには、買い物客の電子メールアドレス（使用可能な場合）、およびECIDを含む[`identityMap`](https://experienceleague.adobe.com/docs/experience-platform/xdm/field-groups/profile/identitymap.html) フィールドが含まれます。

## ストアフロントイベント

ストアフロントイベントは、サイトでの買い物客のインタラクションからデータを取得し、`addToCart`、`pageView`、`createAccount`、`editAccount`、`startCheckout`、`completeCheckout`、`signIn`、`signOut`などのイベントを含めます。 ストアフロントイベントは、シンプルで設定可能な製品にのみ適用されます。

ストアフロントイベントについて詳しくは、[開発者ドキュメント &#x200B;](https://developer.adobe.com/commerce/services/shared-services/storefront-events/#data-connection)を参照してください。

## 顧客プロファイルイベント

ストアフロントから取り込まれたプロファイルイベントには、`signIn`、`signOut`、`createAccount`、`editAccount`などのアカウント情報が含まれます。 これらのデータは、セグメントの定義やマーケティング施策の実行に必要な顧客の詳細情報（サインアップ割引オファーの送信やアカウント変更確認の送信など）を提供するのに役立ちます。

顧客プロファイルイベントについて詳しくは、[開発者ドキュメント &#x200B;](https://developer.adobe.com/commerce/services/shared-services/storefront-events/#data-connection)を参照してください。

## イベントを検索

検索イベントは、買い物客の意図に関連するデータを提供します。 Insightを通じて顧客の意図を把握することで、顧客が商品をどのように検索し、何をクリックして、最終的に購入または放棄するのかを把握できます。 このデータを活用する例として、一番上の商品を検索したものの、その商品を購入しなかった既存顧客をターゲティングする場合があります。 これらのイベントにアクセスするには、[[!DNL Live Search]](../live-search/install.md)拡張機能をインストールする必要があります。

`searchRequestSent`および`searchResponseReceived` イベントの両方にある`searchRequest.id`および`searchResponse.id` フィールドを使用して、検索リクエストを対応する検索応答に相互参照します。

検索イベントについて詳しくは、[開発者ドキュメント &#x200B;](https://developer.adobe.com/commerce/services/shared-services/storefront-events/#data-connection)を参照してください。

## B2B イベント

Adobe Commerceの![B2B](../assets/b2b.svg) B2B マーチャントの場合、これらのイベントにアクセスするには、`experience-platform-connector-b2b`拡張機能を[&#x200B; インストール &#x200B;](install.md#install-the-b2b-extension)する必要があります。

B2B イベントには、購買リストが作成されたか、に追加されたか、または購買リストから削除されたかなどの[購買リスト &#x200B;](https://experienceleague.adobe.com/docs/commerce-admin/b2b/requisition-lists/requisition-lists.html)情報が含まれています。 購買リストに特化したイベントを追跡することで、顧客が頻繁に購入する商品を把握し、そのデータにもとづいた施策を構築できます。

B2B イベントについて詳しくは、[開発者ドキュメント &#x200B;](https://developer.adobe.com/commerce/services/shared-services/storefront-events/#data-connection)を参照してください。
