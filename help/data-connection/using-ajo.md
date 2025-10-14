---
title: Adobe Journey Optimizerを使用して、放棄された買い物かごのメールを送信する
description: Adobe Journey Optimizerを使用して、放棄された買い物かごのメールを送信する方法を説明します。
role: Admin, Developer
feature: Personalization, Integration
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '1262'
ht-degree: 0%

---

# Adobe Journey Optimizerを使用して、放棄された買い物かごにメールを送信

買い物かごやブラウザーセッションが放棄された場合に、パーソナライズされた再エンゲージメントメールまたは通知を配信する方法を説明します。 この記事では、多数の製品やカテゴリを閲覧した顧客、製品にエンゲージした顧客、ページで時間を費やした顧客から生成されたデータを使用します。

## どのデータの使用を検討すればよいですか？

ストアフロントおよびバックオフィスイベントのデータを使用して、放棄された買い物かごの作成、メールの参照、通知を行います。

| データタイプ | ストアフロントデータ（行動イベント） | バックオフィスデータ（サーバーサイドイベント） |
|---|---|---|
| **定義** | サイトに対する顧客のクリックまたはアクション。 | 各注文のライフサイクルと詳細（過去および現在）に関する情報。 |
| **Adobe Commerceのイベント** | [pageView](https://experienceleague.adobe.com/ja/docs/commerce/data-connection/event-forwarding/events#pageview)<br>[productPageView](https://experienceleague.adobe.com/ja/docs/commerce/data-connection/event-forwarding/events)<br>[addToCart](https://experienceleague.adobe.com/ja/docs/commerce/data-connection/event-forwarding/events#addtocart)<br>[openCart](https://experienceleague.adobe.com/ja/docs/commerce/data-connection/event-forwarding/events#opencart)<br>[startCheckout](https://experienceleague.adobe.com/ja/docs/commerce/data-connection/event-forwarding/events#startcheckout)<br>[completeCheckout](https://experienceleague.adobe.com/ja/docs/commerce/data-connection/event-forwarding/events#completecheckout) | [orderPlaced](https://experienceleague.adobe.com/ja/docs/commerce/data-connection/event-forwarding/events-backoffice#orderplaced)<br>[Order history](https://experienceleague.adobe.com/ja/docs/commerce/data-connection/fundamentals/connect-data#send-historical-order-data) |

### 他の顧客は何を達成しましたか？

Adobe [!DNL Commerce] のお客様は、Adobe [!DNL Commerce]、Adobe [!DNL Journey Optimizer]、Adobe [!DNL Real-Time CDP] を使用してパーソナライズされた放棄キャンペーンを実装することで、大きなビジネス上の影響を実現しています。

グローバルなマルチブランドのアパレル小売業者が達成した成果：

- 新しいキャンペーンからのクリックによる 1.9 倍のコンバージョン
- オムニチャネル離脱ジャーニーによる売上高が 57% 増加
- 再エンゲージメントキャンペーンのコンバージョン率が 41% 増加
- 1 週間に 1,000 人以上の新規買い物客がエンゲージ

世界的な飲料企業は以下を達成しました。

- 再エンゲージメントメールの開封率 36%
- クリックスルー率が 21% 向上
- コンバージョン率が 8.5% 向上
- 再関与した放棄者の 89% がコンバージョン

## それでは、始めましょう

この特定の使用例では、[!DNL Commerce] インスタンスからのデータを使用して放棄された買い物かごメールを作成し、Adobe [!DNL Journey Optimizer] に送信することに焦点を当てています。

### Adobe Journey Optimizerとは

[Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/get-started.html?lang=ja) は、買い物客向けにコマースエクスペリエンスをパーソナライズするのに役立ちます。 例えば、Journey Optimizerを使用して、小売店向けの週別プロモーションなどのスケジュールされたマーケティングキャンペーンを作成して配信したり、顧客が買い物かごに商品を追加したもののチェックアウトプロセスを完了しなかった場合に、放棄された買い物かごのメールを生成したりできます。

このトピックでは、[!DNL Commerce] インスタンスから生成された `checkout` イベントをリッスンし、Journey Optimizerでそのイベントに応答することで、放棄された買い物かごメールを作成する方法を説明します。

>[!IMPORTANT]
>
>デモンストレーションの目的では、Experience Platformに送信するストアフロントおよびバックオフィスイベントデータで実稼動イベントデータを薄めないよう、[!DNL Commerce] サンドボックス環境を使用します。

### 前提条件

これらの手順を開始する前に、以下を確認します。

- Adobe [!DNL Journey Optimizer] を使用するようにプロビジョニングされています。 不明な場合は、システムインテグレーターまたはプロジェクトや環境を管理する開発チームにお問い合わせください。
- [!DNL Commerce] で [!DNL Data Connection] 拡張機能を [&#x200B; インストール &#x200B;](install.md) および [&#x200B; 設定 &#x200B;](connect-data.md) しました。
- [!DNL Commerce] イベントデータがExperience Platform Edge に届いていることを [&#x200B; 確認 &#x200B;](connect-data.md#confirm-that-event-data-is-collected) しました。

## 手順 1:[!DNL Commerce] サンドボックス環境でのユーザーの作成

サンドボックス環境でユーザーを作成し、そのユーザーアカウント情報がExperience Platformに表示されることを確認します。 指定したメールが、このセクションで後ほど放棄された買い物かごメールを送信する際に使用するメールとして有効であることを確認します。

1. [!DNL Commerce] サンドボックス環境でログインまたはアカウントを作成します。

   ![&#x200B; テストアカウントにログインする &#x200B;](assets/sign-in-account.png){width="700" zoomable="yes"}

   [!DNL Data Connection] 拡張機能がインストールおよび設定されると、このアカウント情報はプロファイルとしてExperience Platformに送信されます。

1. Experience Platformの「**[!UICONTROL Profile]**」セクションにユーザーアカウント情報が表示されていることを確認します。

   Adobe Experience Platformで **[!UICONTROL Profiles]** に移動します。 プロファイルの **[!UICONTROL Detail]** をクリックして、作成したプロファイルを表示します。

   ![&#x200B; プロファイルを確認 &#x200B;](assets/check-event-profile.png){width="700" zoomable="yes"}

## 手順 2:Journey Optimizerでイベントを表示する

[!DNL Commerce] サンドボックス環境では、商品ページの表示、買い物かごへの商品の追加、買い物客が実行するその他の様々なアクティビティの完了などにより、ストアフロントでトリガーイベントが発生します。 次に、これらのイベントがJourney Optimizerに送信されていることを確認します。

1. [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/user-interface.html?lang=ja) を起動します。
1. 「**[!UICONTROL Profiles]**」を選択します。
1. **[!UICONTROL Identity namespace]** を `Email` に設定します。
1. **[!UICONTROL Identity value]** をメールアドレスに設定します。
1. プロファイルを選択し、「**[!UICONTROL Events]**」タブを選択します。

   ![&#x200B; イベントの詳細を確認 &#x200B;](assets/check-event-details.png){width="700" zoomable="yes"}

   `commerce.checkouts` イベントを探し、イベントペイロードを調べます。

   ```json
   "personID": "84281643067178465783746543501073369488", 
   "eventType": "commerce.checkouts", 
   "_id": "4b41703f-e42e-485b-8d63-7001e3580856-0", 
   "commerce": { 
       "cart": {}, 
       "checkouts": { 
           "value": 1 
       } 
   ```

   ご覧のように、完全なイベントペイロードには豊富なイベントデータが含まれています。 次の節では、[!DNL Commerce] ストアフロントから生成された `commerce.checkouts` イベントをリッスンし、応答するように、Journey Optimizerでイベントを設定します。

## 手順 3:Journey Optimizerでのイベントの設定

Journey Optimizerで 2 つのイベントを設定します。1 つはCommerceから `commerce.checkouts` イベントをリッスンし、もう 1 つは放棄された買い物かごのメールをトリガーするまでに特定の時間の間待機する基本的なタイムアウトイベントです。

### リスナーイベントの作成

1. [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/user-interface.html?lang=ja) を起動します。

1. 左側のペインの **[!UICONTROL Administration]** セクションの下にある「**[!UICONTROL Configurations]**」をクリックします。

1. **[!UICONTROL Events]** タイルで、「**[!UICONTROL Manage]**」をクリックします。

   ![Journey Optimizer イベントの構成 &#x200B;](assets/ajo-config.png){width="700" zoomable="yes"}

1. **[!UICONTROL Events]** ページで「**[!UICONTROL Create Event]**」をクリックします。

1. 右側のナビゲーションで、イベントを次のように設定します。

   1. **[!UICONTROL Name]** を `firstname_lastname_checkout` に設定します。
   1. **[!UICONTROL Type]** を **[!UICONTROL Unitary]** に設定します。
   1. **[!UICONTROL Event id typ]e** を **[!UICONTROL Rule based]** に設定します。
   1. **[!UICONTROL Schema]** を [!DNL Commerce] [&#x200B; スキーマ &#x200B;](update-xdm.md) に設定します。
   1. 「**[!UICONTROL Fields]**」を選択して、**[!UICONTROL Fields]** ページを開きます。 次に、このイベントで役立つフィールドを選択します。 例えば、**[!UICONTROL Product list items]**、**[!UICONTROL Commerce]**、**[!UICONTROL eventType]**、**[!UICONTROL Web]** の下のすべてのフィールドを選択します。
   1. 「**[!UICONTROL OK]**」をクリックして、選択したフィールドを保存します。
   1. 「**[!UICONTROL Event id condition]**」フィールド内をクリックします。 次に、条件を作成します。`eventType` は `commerce.checkouts` と等しく、`personalEmail.address` は前の節でプロファイルを作成した際に使用したメールアドレスと等しい。

      ![Journey Optimizer セットの条件 &#x200B;](assets/ajo-set-condition.png){width="700" zoomable="yes"}

   1. 「**[!UICONTROL OK]**」をクリックします。
   1. 「**[!UICONTROL Save]**」をクリックしてイベントを保存します。

### タイムアウトイベントの作成

1. 以前と同様に、Journey Optimizerでイベントを作成します。

1. 右側のナビゲーションで、イベントを次のように設定します。

   1. **[!UICONTROL Name]** を `firstname_lastname_timeout` に設定します。
   1. **[!UICONTROL Type]** を **[!UICONTROL Unitary]** に設定します。
   1. **[!UICONTROL Event id type]** を **[!UICONTROL Rule based]** に設定します。
   1. **[!UICONTROL Schema]** を [!DNL Commerce] [&#x200B; スキーマ &#x200B;](update-xdm.md) に設定します。
   1. **[!UICONTROL Schema]**、**[!UICONTROL Fields]**、**[!UICONTROL Event id condition]** を上記と同じに設定します。
   1. 「**[!UICONTROL Save]**」をクリックしてイベントを保存します。

これら 2 つのイベントを設定し、放棄された買い物かごメールを送信するジャーニーを作成します。

## 手順 4：チェックアウトジャーニーの作成

`commerce.checkouts` イベントをリッスンし、指定された時間が経過すると放棄された買い物かごのメールを送信するジャーニーを作成します。

1. Journey Optimizerで、「**J[!UICONTROL OURNEY MANAGEMENT]**」の下の「**[!UICONTROL Journeys]**」を選択します。
1. 「**[!UICONTROL Create Journey]**」をクリックします。
1. ジャーニーの名前を指定します。
1. 「**[!UICONTROL OK]**」をクリックして、ジャーニーを保存します。
1. 左側のナビゲーションの「**[!UICONTROL EVENTS]**」セクションで、以前に作成したチェックアウトイベントを検索し `firstname_lastname_checkout` キャンバスにドラッグ&amp;ドロップします。

   >[!TIP]
   >
   >イベントをダブルクリックすると、そのイベントがキャンバスに自動的に追加されます。

1. タイムアウトイベントを検索して、キャンバスに追加します。
1. タイムアウトイベントをダブルクリックします。

   1. 「**[!UICONTROL Timeout]**」セクションで、「**[!UICONTROL Define the event time]**」チェックボックスを選択します。
   1. **[!UICONTROL Wait for]** フィールドに「`1`」と「`Minute`」と入力します。
   1. 「**[!UICONTROL Set a timeout path]**」チェックボックスをオンにします。

   このタイムアウト設定を使用すると、チェックアウトを実行したが、このタイムアウト分岐で 1 分トリガー以内に注文が完了しない買い物客が発生します。 実際の実稼動環境では、これを 24 時間などの長い期間に設定します。

1. **[!UICONTROL ACTIONS]** の下の左側のナビゲーションで、タイムアウトブランチに **[!UICONTROL Email]** アクションを追加します。 ジャーニーは次のようになります。

   ![Journey Optimizer キャンバス &#x200B;](assets/ajo-canvas.png){width="700" zoomable="yes"}

### 放棄された買い物かごのメールの作成

放棄された買い物かごが検出されたときに送信される、放棄された買い物かごメールを作成します。

1. 上記で作成したジャーニーで、キャンバス上の **[!UICONTROL Email]** アイコンをダブルクリックします。

1. Journey Optimizer ガイドの [&#x200B; 手順 &#x200B;](https://experienceleague.adobe.com/docs/journey-optimizer/using/content-management/personalization/personalization-use-cases/personalization-use-case-helper-functions.html?lang=ja#configure-email) に従って、放棄された買い物かごのメールを作成します。

これで、Journey Optimizerで [!DNL Commerce] ストアからの `commerce.checkouts` イベントをリッスンするジャーニーと、一定期間経過後に送信される放棄された買い物かごメールが作成されました。 次の節では、ジャーニーのテスト方法を説明します。

## 手順 5：チェックアウトイベントのリアルタイムトリガー

この節では、リアルタイムでイベントをテストします。

1. Journey Optimizerで、「テストモード」をオンにします。

   ![&#x200B; テストモードを有効にする &#x200B;](assets/ajo-enable-test.png){width="700" zoomable="yes"}

1. このジャーニーをリアルタイムでテストするには、別のブラウザータブを開き、サンドボックス環境の [!DNL Commerce] web サイトに移動します。

   1. 商品を買い物かごに追加します。
   1. チェックアウトページに移動します。
   1. チェックアウトページからメインページに戻るかタブを閉じて、買い物かごを放棄します。

      これで、ジャーニーがトリガーされます。 確認するには、Journey Optimizerでジャーニーを持つタブを開きます。 ユーザーが通過したパスを示す緑の矢印が表示されます。

1. メールのインボックスを確認します。
