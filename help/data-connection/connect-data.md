---
title: Commerce Data のAdobe Experience Platformへの接続
description: Commerce データをAdobe Experience Platformに接続する方法を説明します。
feature: Personalization, Integration, Configuration
exl-id: 8ba33277-38a5-45af-86e0-906cfb3b998d
source-git-commit: 5f7565f5bb80fcc65cbbcdc31c5c3b12fed4e5ee
workflow-type: tm+mt
source-wordcount: '2917'
ht-degree: 0%

---

# Commerce データのAdobe Experience Platformへの接続

[!DNL Data Connection] 拡張機能をインストールすると、Commerce **管理者** の **サービス** の下の _システム_ メニューに 2 つの新しい設定ページが表示されます。

- Commerce サービスコネクタ
- [!DNL Data Connection]

Adobe Commerce インスタンスをAdobe Experience Platformに接続するには、まずCommerce サービスコネクタを設定し、最後に [!DNL Data Connection] 拡張機能を設定して、両方のコネクタを設定する必要があります。

## Commerce サービスコネクタの設定

以前にCommerce サービスをインストールしている場合は、Adobe Commerce サービスコネクタは既に設定されているはずです。 そうでない場合は、[Commerce サービスコネクタ ](../landing/saas.md) ページで次のタスクを実行する必要があります。

1. Commerce アカウントにログインして [ 実稼動用およびサンドボックス用の API キーを取得 ](../landing/saas.md#credentials) します。
1. [SaaS データ空間 ](../landing/saas.md#saas-configuration) を選択します。
1. Adobe アカウントにログインして [ 組織 ID を取得 ](../landing/saas.md#ims-organization-optional) します。

Commerce サービスコネクタを設定したら、[!DNL Data Connection] 拡張機能を設定します。

## [!DNL Data Connection] 拡張機能の設定

この節では、[!DNL Data Connection] 拡張機能の設定方法について説明します。

### サービスアカウントと資格情報の詳細の追加

[ 注文履歴データ ](#send-historical-order-data) または [ 顧客プロファイルデータ ](#send-customer-profile-data) を収集して送信する予定の場合は、サービスアカウントと資格情報の詳細を追加する必要があります。 また、[Audience Activation](https://experienceleague.adobe.com/docs/commerce-admin/customers/audience-activation.html?lang=ja) 拡張機能を設定する場合は、次の手順を実行する必要があります。

ストアフロントまたはバックオフィスのデータを収集して送信するだけの場合は、「[ 一般 ](#general)」セクションにスキップできます。

#### 手順 1:Adobe Developer Consoleでプロジェクトを作成する

Experience Platform API を呼び出せるように、Commerceを認証するプロジェクトをAdobe Developer Consoleで作成します。

プロジェクトを作成するには、[Experience Platform API の認証とアクセス ](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=ja) チュートリアルで説明されている手順に従います。

チュートリアルを進める際は、プロジェクトに次のものが含まれていることを確認します。

- 次の [ 製品プロファイル ](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=ja#select-product-profiles) にアクセス：**デフォルトの実稼動環境のすべてのアクセス** および **AEPデフォルトのすべてのアクセス**。
- 正しい [ 役割と権限が設定されている ](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=ja#assign-api-to-a-role)。
- サーバー間認証方法として JSON web トークン（JWT）を使用することにした場合は、秘密鍵もアップロードする必要があります。

この手順の結果、次の手順で使用する設定ファイルが作成されます。

#### 手順 2：設定ファイルのダウンロード

[ ワークスペース設定ファイル ](https://developer.adobe.com/commerce/extensibility/events/project-setup/#download-the-workspace-configuration-file) をダウンロードします。 `<workspace-name>.json` ファイルには、Commerce管理者の **サービスアカウント /資格情報の詳細** ページに入力する必要のあるすべての値が含まれています。

![[!DNL Data Connection] Admin Configuration](./assets/epc-admin-config.png){width="700" zoomable="yes"}

1. Commerce管理者で、**ストア**/設定/**設定**/**サービス**/**[!DNL Data Connection]** に移動します。

1. 実装したサーバー間認証方法を **Adobe Developer認証タイプ** メニューから選択します。 Adobeでは、OAuth を使用することをお勧めします。 JWT は非推奨（廃止予定）になりました。 [学習を増やす](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/)。

1. （JWT のみ） `private.key` ファイルの内容をコピーして、「**クライアントの秘密鍵**」フィールドに貼り付けます。 次のコマンドを使用して、コンテンツをコピーします。

   ```bash
   cat config/private.key | pbcopy
   ```

   [ ファイルについて詳しくは、](https://developer.adobe.com/developer-console/docs/guides/authentication/JWT/) サービスアカウント（JWT）認証 `private.key` を参照してください。

1. `<workspace-name>.json` ファイルの内容を **サービスアカウント /資格情報の詳細** フィールド（`"client_id"`、`"client_secrets"`、`"technical_account_email"`、`"technical_account_id"` など）にコピーします。

1. 「**設定を保存**」をクリックします。

1. [**[!UICONTROL Test connection]**] ボタンをクリックし、入力したサービス アカウントと認証情報が正しいことを確認します。

### 一般

1. 管理者で、**システム**/サービス/**[!DNL Data Connection]** に移動します。

   ![[!DNL Data Connection] Settings](./assets/epc-settings.png){width="700" zoomable="yes"}

1. **一般** の下の **設定** タブで、[Commerce サービスコネクタ ](../landing/saas.md#organizationid) で設定されているように、Adobe Experience Platform アカウントに関連付けられている ID を確認します。 組織 ID はグローバルです。 Adobe Commerce インスタンスごとに関連付けることができる組織 ID は 1 つだけです。

1. **範囲** ドロップダウンで、コンテキストを **Web サイト** に設定します。

1. （オプション） [AEP Web SDK（alloy）を既にサイトにデプロイしている場合は ](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html?lang=ja) このチェックボックスを有効にして、AEP Web SDKの名前を追加します。 それ以外の場合は、これらのフィールドを空白のままにすると、[!DNL Data Connection] 拡張機能によって自動的にデプロイされます。

   >[!NOTE]
   >
   >独自のAEP Web SDKを指定する場合、[!DNL Data Connection] 拡張機能では、このページで指定されたデータストリーム ID （存在する場合）ではなく、そのSDKに関連付けられたデータストリーム ID が使用されます。

### データ収集

このセクションでは、Experience Platform Edge に収集して送信するデータのタイプを指定します。 データには次の 3 つのタイプがあります。

- **行動** （クライアントサイドのデータ）は、ストアフロントでキャプチャされたデータです。 これには、`View Page`、`View Product`、`Add to Cart`、[ 購入リスト ](events.md#b2b-events) 情報（B2B マーチャント向け）などの買い物客のインタラクションが含まれます。

- **バックオフィス** （サーバーサイドデータ）は、Commerce サーバーで取得されたデータです。 注文のステータスに関する情報（注文が行われた、キャンセルされた、払い戻された、出荷された、完了したかどうかなど）が含まれます。 また、[ 過去の注文データ ](#send-historical-order-data) も含まれます。

- **プロファイル** は、買い物客のプロファイル情報に関連するデータです。 詳細情報 [ 詳細情報 ](#send-customer-profile-data)。

Adobe Commerce インスタンスがデータ収集を開始できるようにするには、[ 前提条件 ](overview.md#prerequisites) を確認してください。

[ ストアフロント ](events.md#storefront-events)、[ バックオフィス ](events-backoffice.md)、および [ プロファイル ](events-backoffice.md#customer-profile-events-server-side) イベントについて詳しくは、イベントトピックを参照してください。

>[!NOTE]
>
>**データ収集** セクションのすべてのフィールドは、**Web サイト** の範囲以上に適用されます。

1. ストアフロントの行動データを送信する場合は、「**ストアフロントイベント**」を選択します。

1. 注文が行われた、キャンセルされた、返金された、発送されたかなど、注文ステータス情報を送信する場合は、**バックオフィスイベント** を選択します。

   >[!NOTE]
   >
   >**バックオフィスイベント** を選択すると、すべてのバックオフィスデータがExperience Platform Edge に送信されます。 買い物客がデータ収集のオプトアウトを選択した場合は、Experience Platformで買い物客のプライバシー環境設定を明示的に設定する必要があります。 これは、コレクターが既に買い物客の好みに基づいて同意を処理するストアフロントイベントとは異なります。 Experience Platformでの買い物客のプライバシー環境設定について [ 詳細 ](https://experienceleague.adobe.com/docs/experience-platform/landing/governance-privacy-security/consent/adobe/dataset.html?lang=ja) 説明します。

1. （独自のAEP Web SDKを使用している場合は、この手順をスキップしてください。） [ 作成 ](https://experienceleague.adobe.com/docs/experience-platform/datastreams/configure.html?lang=ja#create) Adobe Experience Platformのデータストリーム、または収集に使用する既存のデータストリームを選択します。 そのデータストリーム ID を **データストリーム ID** フィールドに入力します。

1. Commerce データを格納する **データセット ID** を入力します。 データセット ID を見つけるには：

   1. Experience Platform UI を開き、左側のナビゲーションで **データセット** を選択して **データセット** ダッシュボードを開きます。 ダッシュボードには、組織で使用可能なすべてのデータセットが一覧表示されます。 リストに表示された各データセットに関する詳細（名前、データセットが準拠するスキーマ、最新の取得実行のステータスなど）が表示されます。
   1. データストリームに関連付けられたデータセットを開きます。
   1. 右側のパネルで、データセットに関する詳細を表示します。 データセット ID をコピーします。

1. [cron](https://experienceleague.adobe.com/docs/commerce-admin/systems/tools/cron.html?lang=ja) ジョブに従ってスケジュールに基づいてバックオフィスイベントデータが確実に更新されるようにするには、`Sales Orders Feed` インデックスを `Update by Schedule` に変更する必要があります。

   1. _管理者_ サイドバーで、**[!UICONTROL System]**/_[!UICONTROL Tools]_/**[!UICONTROL Index Management]**&#x200B;に移動します。

   1. `Sales Orders Feed` インデクサーのチェックボックスを選択します。

   1. **[!UICONTROL Actions]** を `Update by Schedule` に設定します。

   1. 初めてバックオフィスのデータを有効にする場合は、次のコマンドを実行して再インデックスを実行し、再同期をトリガーします。 [cron](https://experienceleague.adobe.com/docs/commerce-admin/systems/tools/cron.html?lang=ja) ジョブが正しく設定されている限り、それ以降の再同期は自動的に実行されます。

      ```bash
      bin/magento index:reindex sales_order_data_exporter_v2
      ```

      ```bash
      bin/magento saas:resync --feed orders
      ```

#### フィールドの説明

| フィールド | 説明 |
|--- |--- |
| 範囲 | 設定を適用する特定の web サイト。 |
| 組織 ID （グローバル） | Adobe DX 製品を購入した組織に属する ID。 この ID は、Adobe Commerce インスタンスをAdobe Experience Platformにリンクします。 |
| は、AEP Web SDKが既にサイトにデプロイされているかどうかを示します | 独自のAEP Web SDKをサイトにデプロイした場合は、このチェックボックスをオンにします |
| AEP Web SDK名（グローバル） | Experience Platform Web SDKが既にサイトにデプロイされている場合は、このフィールドにそのSDKの名前を指定します。 これにより、ストアフロントイベントコレクターおよびストアフロントイベントSDKは、[!DNL Data Connection] 拡張機能によってデプロイされたバージョンではなく、Experience Platform Web SDKを使用できます。 Experience Platform Web SDKをサイトにデプロイしていない場合は、このフィールドを空白のままにすると、[!DNL Data Connection] 拡張機能によってデプロイされます。 |
| ストアフロントイベント | 組織 ID とデータストリーム ID が有効な場合、デフォルトではがオンになっています。 ストアフロントイベントは、サイトを閲覧する買い物客から匿名化された行動データを収集します。 |
| バックオフィスイベント | オンにした場合、イベントペイロードには、注文が行われた、キャンセルされた、払い戻された、出荷されたかなど、匿名の注文ステータス情報が含まれます。 |
| データストリーム ID （web サイト） | Adobe Experience Platformから他のAdobe DX 製品にデータを送信するための ID。 この ID は、特定のAdobe Commerce インスタンス内の特定の web サイトに関連付ける必要があります。 独自のExperience Platform Web SDKを指定する場合、このフィールドにはデータストリーム ID を指定しないでください。 [!DNL Data Connection] 拡張機能は、そのSDKに関連付けられたデータストリーム ID を使用し、このフィールドで指定されたデータストリーム ID （ある場合）を無視します。 |
| データセット ID （web サイト） | Commerce データを含むデータセットの ID。 「**ストアフロントイベント**」チェックボックスまたは「**バックオフィスイベント**」チェックボックスをオフにしない限り、このフィールドは必須です。 また、独自のExperience Platform Web SDKを使用していて、データストリーム ID を指定していない場合でも、データストリームに関連付けられているデータセット ID を追加する必要があります。 それ以外の場合は、このフォームを保存できません。 |

オンボーディング後、ストアフロントデータがExperience Platform Edge に送られ始めます。 バックオフィスのデータがエッジに表示されるまでに約 5 分かかります。 その後の更新は、cron スケジュールに基づいてエッジに表示されます。

### 顧客プロファイルデータの送信

Experience Platformに送信できるプロファイルデータには、プロファイルレコードと時系列プロファイルイベントの 2 種類があります。

プロファイルレコードには、買い物客がCommerce インスタンスでプロファイルを作成する際に保存されるデータ（買い物客の名前など）が含まれています。 スキーマとデータセットが [ 適切に設定 ](profile-data.md) されると、プロファイルレコードがExperience Platformに送信され、Adobeのプロファイル管理およびセグメント化サービス [Real-Time CDP](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=ja) に転送されます。

時系列プロファイルイベントには、サイト上でアカウントが作成、編集、削除されたかどうかなど、買い物客のプロファイル情報に関するデータが含まれます。 プロファイルイベントデータがExperience Platformに送信されると、他の DX 製品で使用できるデータセットに格納されます。

1. サービスアカウントと資格情報の詳細が [ 指定 ](#add-service-account-and-credential-details) されていることを確認します。

1. [ プロファイルレコードデータの取り込み ](profile-data.md) および [ 時系列プロファイルイベントデータの取り込み ](update-xdm.md#time-series-profile-event-data) 用にスキーマとデータセットが指定されていることを確認します。

1. プロファイルデータをExperience Platformに送信する場合は、「**顧客プロファイル**」チェックボックスにチェックマークを付けます。

1. **プロファイルデータセット ID** を入力します。

   プロファイルレコードデータでは、行動およびバックオフィスイベントデータに現在使用しているデータセットとは異なるデータセットを使用する必要があります。

1. 行動データとバックオフィスデータに使用しているものと同じデータストリーム ID でプロファイルイベントをストリーミングしない場合は、**同じデータストリーム ID で顧客プロファイルをストリーミングする** のチェックマークを削除し、代わりに使用するデータストリーム ID を入力します。

Real-Time CDPでプロファイルレコードが使用可能になるまで、約 10 分かかることがあります。 プロファイルイベントのストリーミングは直ちに開始されます。

>[!TIP]
>
>Experience Platformにプロファイルデータが表示されない場合のトラブルシューティングの提案については、[Commerce ナレッジベース ](https://experienceleague.adobe.com/ja/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/data-connection-customer-profiles-not-exported) を参照してください。

#### フィールドの説明

| フィールド | 説明 |
|--- |--- |
| 顧客プロファイル | 顧客プロファイルレコードを収集して送信する場合は、このチェックボックスを選択します。 |
| プロファイルデータセット ID | プロファイルレコードでは、行動イベントやバックオフィスイベントに使用するデータセットとは異なるデータセットを使用する必要があります。 |
| 同じデータストリーム ID を使用した顧客プロファイルのストリーミング | 行動イベントとバックオフィスイベントで現在使用されているのと同じデータストリームを使用するかどうかを決定します。 |
| 顧客プロファイルのデータストリーム | 顧客プロファイルレコード固有のデータストリームを指定します。 |

### 注文履歴データの送信

Adobe Commerceは、最大 5 年間の注文の履歴データとステータス [ を収集 ](events-backoffice.md#back-office-events) ます。 [!DNL Data Connection] 拡張機能を使用して、その履歴データをExperience Platformに送信し、顧客プロファイルを充実させ、過去の注文に基づいてカスタマーエクスペリエンスをパーソナライズできます。 データは、Experience Platform内のデータセットに保存されます。

Commerceでは既に注文の履歴データを収集していますが、それらのデータをExperience Platformに送信するには、いくつかの手順を実行する必要があります。

注文履歴の詳細については、このビデオをご覧ください。次の手順を完了して、注文履歴の収集を実装します。

>[!VIDEO](https://video.tv.adobe.com/v/3450228?captions=jpn)

#### Order Sync サービスの設定

注文同期サービスは、[ メッセージキューフレームワーク ](https://developer.adobe.com/commerce/php/development/components/message-queues/) と RabbitMQ を使用します。 これらの手順を完了すると、注文ステータスデータを SaaS に同期できます。この同期は、Experience Platformに送信する前に必要になります。

1. サービスアカウントと資格情報の詳細が [ 指定 ](#add-service-account-and-credential-details) されていることを確認します。

1. RabbitMQ[ 有効にする ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure/service/rabbitmq.html?lang=ja)。

   >[!NOTE]
   >
   >RabbitMQ は、Commerce バージョン 2.4.7 以降に対応するように既に設定されていますが、コンシューマーを有効にする必要があります。

1. 環境変数を使用して、`.magento.env.yaml` の cron ジョブでメッセージキューコンシューマー `CRON_CONSUMERS_RUNNER` 有効にします。

   ```yaml
      stage:
        deploy:
          CRON_CONSUMERS_RUNNER:
            cron_run: true
   ```

   >[!NOTE]
   >
   >使用可能なすべての設定オプションについては、[ 変数のデプロイ ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure/env/stage/variables-deploy.html?lang=ja#cron_consumers_runner) のドキュメントを参照してください。

注文同期サービスを有効にすると、**[!UICONTROL [!DNL Data Connection]]** のページで過去の注文日付範囲を指定できるようになります。

#### 注文履歴の日付範囲の指定

Experience Platformに送信する注文履歴の日付範囲を指定します。

1. 管理者で、**システム**/サービス/**[!DNL Data Connection]** に移動します。

1. 「**注文履歴**」タブを選択します。

   ![[!DNL Data Connection] Order History](./assets/epc-order-history.png){width="700" zoomable="yes"}

1. **注文履歴の同期** で、「**設定からデータセット ID をコピー**」チェックボックスが既に有効になっています。 これにより、「**設定** タブで指定したデータセットと同じデータセットを使用していることになります。

1. **From** および **To** フィールドで、送信する過去の注文データの日付範囲を指定します。 日付範囲は 5 年を超えることはできません。

1. 「**[!UICONTROL Start Sync]**」を選択すると、開始する同期がトリガーされます。 注文の履歴データは、ストリーミングデータであるストアフロントおよびバックオフィスデータとは対照的に、バッチデータです。 バッチデータがExperience Platformに到着するまで約 45 分かかります。

##### フィールドの説明

| フィールド | 説明 |
|--- |--- |
| 設定からデータセット ID をコピー | 「**設定** タブに入力したデータセット ID をコピーします。 |
| データセット ID （web サイト） | Commerce データを含むデータセットの ID。 「**ストアフロントイベント**」チェックボックスまたは「**バックオフィスイベント**」チェックボックスをオフにしない限り、このフィールドは必須です。 また、独自のExperience Platform Web SDKを使用していて、データストリーム ID を指定していない場合でも、データストリームに関連付けられているデータセット ID を追加する必要があります。 それ以外の場合は、このフォームを保存できません。 |
| 送信元 | 注文履歴データの収集を開始する日付。 |
| 終了 | 注文履歴データの収集を終了する日付。 |
| 同期を開始 | 注文履歴データをExperience Platform Edge に同期するプロセスを開始します。 このボタンは、**[!UICONTROL Dataset ID]** フィールドが空白の場合やデータセット ID が無効な場合は無効になります。 |

### データのカスタマイズ

「**データのカスタマイズ**」タブでは、[!DNL Commerce] で設定されてExperience Platformに送信されたカスタム属性を表示できます。

![[!DNL Data Connection] データのカスタマイズ ](./assets/epc-data-customization.png){width="700" zoomable="yes"}

>[!IMPORTANT]
>
>[ データ収集 ](#data-collection) タブで **指定** したデータストリーム ID が、カスタム属性を取り込むためにスキーマにリンクされた ID と一致することを確認します。

注文のカスタム属性を作成してExperience Platformに送信する場合、Commerceの属性名がExperience Platformの [!DNL Commerce] スキーマの属性名と一致する必要があります。 一致しない場合は、違いを特定するのが難しい可能性があります。 名前が一致しない場合は、**カスタム順序属性** テーブルが問題の解決に役立ちます。

**カスタム注文属性** テーブルを使用すると、バックオフィスとExperience Platformの [!DNL Commerce] スキーマとの間のカスタム注文属性の設 [!DNL Commerce] とマッピングを視覚的に確認できます。 このテーブルを使用すると、様々なソースをまたいで注文レベルおよび注文品目レベルのカスタム属性を表示でき、見つからない属性や調整が正しくない属性を簡単に識別できます。 また、データセット ID も表示されるので、ライブデータセットと履歴データセットを区別するのに役立ちます。各データセットには独自のカスタム属性を設定できるからです。

テーブルのカスタム属性名の横に緑色のチェックマークが表示されない場合は、ソースの属性名が一致していないことを示しています。 1 つのソースの属性名を修正すると、緑色のチェックマークが表示され、名前が一致したことが示されます。

- Experience Platformのスキーマで属性名が更新された場合、「**データのカスタマイズ**」タブで設定を保存して、Experience Platform スキーマの変更をトリガーする必要があります。 この変更は、「**」ボタンをクリックすると** カスタム注文属性 **[!UICONTROL Refresh]** テーブルに反映されます。
- [!DNL Commerce] で属性名を更新する場合は、注文イベントを生成して **カスタム注文属性** テーブルの名前を更新する必要があります。 変更は約 60 分後に反映されます。

詳しくは、[ カスタム属性の設定 ](custom-attributes.md) を参照してください。

#### フィールドの説明

| フィールド | 説明 |
|--- |--- |
| データセット | カスタム属性を含むデータセットを表示します。 ライブデータセットと履歴データセットには、独自のカスタム属性を設定できます。 |
| Adobe Commerce | バックオフィスで作成されたカスタム属性 [!DNL Commerce] 表示します。 |
| Experience Platform | Experience Platformの [!DNL Commerce] スキーマで指定されたカスタム属性を表示します。 |
| 更新 | Experience Platformの [!DNL Commerce] スキーマからカスタム属性名を取得します。 |

## イベントデータが収集されることを確認します

データがCommerce ストアから収集されていることを確認するには、[Adobe Experience Platform debugger](https://experienceleague.adobe.com/docs/experience-platform/debugger/home.html?lang=ja) を使用してCommerce サイトを調べます。 データが収集されていることを確認したら、[ 作成したデータセット ](overview.md#prerequisites) からデータを返すクエリを実行して、ストアフロントおよびバックオフィスイベントデータがエッジに表示されることを確認できます。

1. Experience Platformの左側のナビゲーションで「**クエリ**」を選択し、「[!UICONTROL Create Query]」をクリックします。

   ![ クエリエディター ](assets/query-editor.png)

1. クエリエディターが開いたら、データセットからデータを選択するクエリを入力します。

   ![ クエリを作成 ](assets/create-query.png)

   例えば、クエリは次のようになります。

   ```sql
   SELECT * from `your_dataset_name` ORDER by TIMESTAMP DESC
   ```

1. クエリを実行すると、結果が「**コンソール** タブの横の「**結果** タブに表示されます。 このビューには、クエリの表形式出力が表示されます。

   ![ クエリエディター ](assets/query-results.png)

この例では、[`commerce.productListAdds`](events.md#addtocart)、[`commerce.productViews`](events.md#productpageview)、[`web.webpagedetails.pageViews`](events.md#pageview) などからのイベントデータが表示されます。 このビューを使用すると、Commerce データがエッジに到達したことを確認できます。

結果が期待どおりでない場合は、データセットを開いて、失敗したバッチの読み込みを探します。 詳しくは、[ バッチインポートのトラブルシューティング ](https://experienceleague.adobe.com/docs/experience-platform/ingestion/batch/troubleshooting.html?lang=ja) を参照してください。

### プロファイルデータがExperience Platformに表示されることを確認

Experience Platformにプロファイルデータが表示されない場合のトラブルシューティングの提案については、[Commerce ナレッジベース ](https://experienceleague.adobe.com/ja/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/data-connection-customer-profiles-not-exported) を参照してください。

## 次の手順

Commerce データがExperience Platform エッジに送信されると、Adobe Journey Optimizerなどの他のAdobe Experience Cloud製品でそのデータを使用できます。 例えば、特定のイベントをリッスンするようにJourney Optimizerを設定し、そのイベントデータに基づいて、初回ユーザーの場合はメールをトリガーし、放棄された買い物かごがある場合はメッセージを送信することができます。 Journey Optimizerで [ カスタマージャーニーを作成 ](using-ajo.md) してCommerce プラットフォームを拡張する方法を説明します。
