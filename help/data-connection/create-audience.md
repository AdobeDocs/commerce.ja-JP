---
title: ' [!DNL Commerce]  イベントデータを使用してReal-Time CDPでオーディエンスを作成する'
description: Real-Time CDPで [!DNL Commerce]  イベントデータを使用してオーディエンスを作成する方法を説明します
role: Admin, Developer
feature: Personalization, Integration
exl-id: 0e9d286b-c459-44db-bbf8-2cb46e21739d
TQID: https://experienceleague.adobe.com/f8XYzoWJCecwuEaNBA17-bf6gtGBLxpDQPJBqDk07-0
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
  - id: fd2e3797-f2ea-4b36-a9af-52acf5e90513
source-git-commit: 2362159cd352d812f60838b42ade1e98bab5a0d3
workflow-type: tm+mt
source-wordcount: 1107
ht-degree: 0%

---

# [!DNL Commerce] イベントデータを使用してReal-Time CDPでオーディエンスを作成

[!DNL Commerce] ストアから取得したイベントデータを使用して、Real-Time CDPでオーディエンスを作成します。 取り込まれるデータは、閲覧行動、過去の購入履歴、プロファイル属性、コンバージョンや解約の傾向、ロイヤルティステータス、顧客価値の高い製品や低い製品など、様々な情報にもとづいています。

## どのようなデータの利用を検討すればよいか？

ストアフロント、バックオフィス、プロファイルイベントからのデータを利用して、Real-Time CDPでオーディエンスを構築できます。

| データタイプ | ストアフロントデータ（行動イベント） | バックオフィスデータ（サーバーサイドイベント） | 顧客プロファイルデータとセグメントデータ |
|---|---|---|---|
| **定義** | 顧客がサイトで実行するクリック数やアクション数。 | 各注文のライフサイクルと詳細に関する情報（過去と現在）。 | 顧客が誰であり、その適格性を判断するセグメントは何か。 |
| **Adobe Commerceによってキャプチャされたイベント** | `productPageView`<br>`addToCart` | `placeOrder`<br>`orderplaced`<br>`orderLineItemRefunded`<br>`order Canceled`<br>`order history` | `createAccount`<br>`editAccount`<br>`Profile Record` |

## 他の顧客は何を達成しましたか？

Adobe [!DNL Commerce]のお客様は、Real-Time CDPで構築されたオーディエンスをアクティブ化し、[!DNL Commerce] インスタンスにデプロイすることで、大きなビジネス効果を得ました。 関連するCommerce イベントデータの結果については、[Adobe Journey Optimizerを使用してカート放棄メールを送信する](using-ajo.md#what-have-other-customers-achieved)を参照してください。

## では始めましょう

この記事では、次の方法について説明します。

- イベントが収集した[!DNL Commerce] データに基づいて、Real-Time CDPでオーディエンスを作成します
- [!DNL Commerce] ストアのオーディエンスをアクティブ化
- [!DNL Commerce]のオーディエンスを使用して、買い物かごの価格ルールを通知する

>[!IMPORTANT]
>
>[!DNL Commerce] サンドボックス環境を使用して、この記事で説明したタスクを完了します。 これにより、Experience Platformに送信するストアフロントおよびバックオフィスのイベントデータが、本番イベントデータを希薄化しないようにします。

### 前提条件

始める前に、次の点を確認してください。

- Real-Time CDPを使用するようにプロビジョニングされています。 不明な場合は、システムインテグレーターまたはプロジェクトや環境を管理する開発チームに確認してください。
- [さんが[!DNL Commerce]の[!DNL Data Connection]拡張機能を](install.md) インストールし、[さんが](connect-data.md)設定しました。
- [!DNL Commerce] イベントデータがExperience Platform エッジに到達していることを[確認しました](connect-data.md#confirm-that-event-data-is-collected)。

### &#x200B;1. オーディエンスの作成

オーディエンスとは、類似の行動や特徴を共有する顧客のセットのことです。 この演習では、ストアの特定の製品に関心を持つユーザーを対象とするオーディエンスを作成します。

この演習を簡素化するには、`productPageView` イベントのイベントデータを使用します。 このイベントは、製品名、SKU、価格など、閲覧された製品に関する詳細をキャプチャします。

このイベントデータを使用して、SKU （製品識別子）がサイト上の特定の製品に等しく、イベントが最終日に発生する「製品ビュー」イベントを少なくとも1つ持つ個人をオーディエンスに含めるように指定します。 &#x200B;

1. Experience Platformを開き、左側のナビゲーションメニューから「**[!UICONTROL Audiences]**」を選択します。

   ![&#x200B; オーディエンスダッシュボード &#x200B;](assets/audience-left-rail.png)

1. **[!UICONTROL Create Audience]**&#x200B;をクリックします。

   ![&#x200B; オーディエンスの作成](assets/browse-create-audience.png)

   **セグメントビルダー** ワークスペースが表示されます。

1. **セグメントビルダー** ワークスペースで、**ビルドルール**&#x200B;の作成方法を選択します。

   ![&#x200B; ルールの作成](assets/build-rule.png)

   **セグメントビルダー** ワークスペースでは、オーディエンスのルールと条件を定義します。これらのルールと条件はCommerce ストアのイベントデータとプロファイルデータに基づいており、オーディエンスに適格かどうかを判断する条件を定義します。 たとえば、特定の商品を閲覧した利用者や、特定の期間内に購入した利用者を含むルールを作成することができます。 [&#x200B; セグメントビルダー](https://experienceleague.adobe.com/ja/docs/experience-platform/segmentation/ui/segment-builder)とルールと条件について詳しく説明します。

1. 「[&#x200B; イベント &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-platform/segmentation/ui/segment-builder#events)」タブを選択します。

   ![&#x200B; イベント タブ &#x200B;](assets/audience-events-tab.png)

1. 「製品ビュー」イベントタイプを検索します。 次に、**セグメントビルダー** ワークスペースにドラッグ&amp;ドロップします。

1. 「**イベント**」タブに戻り、「`productListItems`」フィールドの下のデータフィールドである「SKU」を検索します。 **製品ビュー** イベントの上にある&#x200B;**セグメントビルダー** ワークスペースにドラッグ&amp;ドロップします。

   **イベントルール** セクションには、オーディエンスを構築する特定の製品を指定できる場所が表示されます。

   ![SKUを選択](assets/audience-addsku.png)

1. **Any Time**&#x200B;をクリックし、値&#x200B;*1*&#x200B;で&#x200B;*In last*&#x200B;を選択して、時間間隔を1日に設定します。

   オーディエンスを構築する際には、最近のアクティビティを取得するための時間間隔を指定できます。 期間を設定することで、特定の期間内の最近のインタラクションや行動にもとづいて、オーディエンスをターゲティングできます。

1. ワークスペースの右側にある「**オーディエンスプロパティ**」セクションで、オーディエンスの名前、説明、評価方法を指定して、オーディエンスプロパティを設定します。

1. オーディエンスを保存するには、**[!UICONTROL Save and Close]**&#x200B;をクリックします。

   オーディエンスの詳細は、**Audience** ダッシュボードに表示されます。

### &#x200B;2. [!DNL Commerce]宛先に対するオーディエンスのアクティブ化

[!DNL Commerce]宛先に対してオーディエンスをアクティブ化することで、[!DNL Commerce]でオーディエンスを利用できるようにします。

>[!IMPORTANT]
>
>データを受け取る利用可能な宛先として[!DNL Commerce]をまだ設定していない場合は、[Adobe [!DNL Commerce] 接続](https://experienceleague.adobe.com/ja/docs/experience-platform/destinations/catalog/personalization/adobe-commerce)のトピックを参照してください。

1. オーディエンスの「**詳細**」タブで、「**宛先にアクティベート**」をクリックします。

1. [!DNL Commerce]の宛先を選択します。 次に、**次へ**&#x200B;をクリックします。

1. **[!UICONTROL Finish]**&#x200B;をクリックして、アクティブ化プロセスを完了します。

## &#x200B;3. オーディエンスダッシュボードでのオーディエンスの表示

[!DNL Commerce]では、**Real-Time CDP Audiences** ダッシュボードを使用して、[!DNL Commerce] インスタンスに対してパーソナライズできるすべての[&#x200B; アクティブ &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-platform/destinations/ui/activate/activate-edge-personalization-destinations) オーディエンスを表示できます。

**Real-Time CDP Audiences** ダッシュボードにアクセスするには、_管理者_ サイドバーに移動し、**[!UICONTROL Customers]** > **[!UICONTROL Real-time CDP Audience]**&#x200B;に移動します。

ダッシュボードで、作成したオーディエンスを探します。 カート価格ルールまたはダイナミックブロックで使用されていないことに注意してください。 次のセクションでは、オーディエンスをカート価格ルールにリンクします。

![Real-Time CDP オーディエンスダッシュボード &#x200B;](assets/real-time-cdp-dashboard.png)

### &#x200B;4. オーディエンスに基づいてカートの価格ルールを作成します

このセクションでは、新しいオーディエンスに基づいてカート価格ルールを作成する方法について説明します。

1. 新しいオーディエンスが&#x200B;**Real-Time CDP Audiences** ダッシュボードに表示されていることを確認します。
1. [買い物かごの価格ルールを作成](https://experienceleague.adobe.com/ja/docs/commerce-admin/marketing/promotions/cart-rules/price-rules-cart-create)。
1. [新しいオーディエンスを使用して、カート価格ルールの条件](https://experienceleague.adobe.com/ja/docs/commerce-admin/marketing/promotions/cart-rules/price-rules-cart-create#use-real-time-cdp-audiences-to-set-a-condition)を設定します。
1. [商品がカートに追加されたときに実行するアクション &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-admin/marketing/promotions/cart-rules/price-rules-cart-create#step-3-define-the-actions)を設定します。
1. 引き続き、カート価格ルールを設定します。
1. サンドボックスインスタンスの顧客ビューに移動します。
1. オーディエンスを元にした商品をカートに追加します。 カート価格ルールが有効になっていることに注意してください。

## まとめ

この演習では、Real-Time CDPでオーディエンスを作成し、[!DNL Commerce]の宛先に対してアクティブ化しました。 次に、[!DNL Commerce]管理者で、そのオーディエンスに基づいてカート価格ルールを作成し、サンドボックス環境でルールを有効にしました。
