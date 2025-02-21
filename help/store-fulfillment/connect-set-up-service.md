---
title: ストアフルフィルメントソリューションの接続
description: Adobe Commerceと Store Fulfillment ソリューション間の接続を確立します。 Adobe Commerce統合を作成して認証し、Store Fulfillment アカウント資格情報をAdobe Commerce サービス設定に追加します。
role: Admin, Developer
level: Intermediate
feature: Shipping/Delivery, Install, Configuration, User Account, Tools and External Services
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 0%

---

# ストアフルフィルメントソリューションの接続

必要な認証資格情報と接続データをAdobe Commerce管理者に追加して、ストアフルフィルメントサービスをAdobe Commerceに接続します。

- **[Configure [!DNL Commerce integration settings]](#create-an-adobe-commerce-integration)** - Store Fulfillment サービスのAdobe Commerce統合を作成し、Store Fulfillment サーバーから受信リクエストを認証するためのアクセストークンを生成します。

- **[Store Fulfillment Services のアカウント資格情報を設定](#configure-store-fulfillment-account-credentials)** – 資格情報を追加して、Adobe Commerceを Store Fulfillment アカウントに接続します。

>[!NOTE]
>
>テストを開始する前に、接続設定を完了し、接続が正常に検証されていることを確認します。

## Adobe Commerce統合の作成

Adobe Commerceとストアフルフィルメントサービスを統合するには、Commerce統合を作成し、ストアフルフィルメントサーバーからのリクエストの認証に使用できるアクセストークンを生成します。 また、Adobe Commerceから [!DNL Store Fulfillment] サービスへのリクエストで応答エラーが発生しないよう `The consumer isn't authorized to access %resources.`、Adobe Commerce [!UICONTROL Consumer Settings] オプションを更新する必要もあります。

1. 管理者から、Store Fulfillment の統合を作成します。

   - 拡張機能に名前を付ける
   - メールアドレスを入力
   - 管理者アカウントのパスワードを入力

1. 以下を使用して、統合の API リソースのアクセス権限を設定します。

   - 「売上」 > 「BOPI オーダー更新」
   - システム/ストアフルフィルメントアプリの権限

1. 統合を保存して有効化することで、認証用のアクセストークンを生成します。

1. アクセストークンをコピーし、暗号化された安全な場所に保存します。

1. アカウントマネージャーと協力して、ストアフルフィルメントサイドの設定を完了し、統合を認証します。

1. 「Adobe Commerce [!UICONTROL Consumer Settings]」オプションを有効にして [!UICONTROL Allow OAuth Access Tokens to be used as standalone Bearer tokens] きます。

   - 管理者から、**[!UICONTROL Stores]**/[!UICONTROL Configuration]/**[!UICONTROL Services]**/**[!UICONTROL OAuth]**/**[!UICONTROL Consumer Settings]** に移動します。

   - [!UICONTROL Allow OAuth Access Tokens to be used as standalone Bearer tokens] オプションを **[!UICONTROL Yes]** に設定します。

>[!IMPORTANT]
>
> 統合トークンは環境に固有です。 別の環境のソース・データを使用して、ある環境のデータベースをリストアする場合（ステージング環境から本番データをリストアする場合など）、リストア操作中に統合トークンの詳細が上書きされないように、データベース・エクスポートから `oauth_token` のテーブルを除外します。


## Store Fulfillment アカウントの資格情報の設定

取り込みフォームを完了すると、Walmart Store フルフィルメントアカウントが作成されます。 利用可能な場合は、次の資格情報が提供されます。

- [!DNL Merchant ID]
- [!DNL Consumer ID]
- [!DNL Consumer Secret]
- [!DNL API Server URL]
- [!DNL Token Auth Server URL] （通常、上記の設定と同じ）

これらの資格情報は、ストアフルフィルメントを設定および使用するために必要です。

>[!NOTE]
>
>アカウントの作成プロセスが完了するまでに時間がかかる場合があります。 資格情報を待っている間に、[Store Fulfillment ソリューションのその他の設定を確認および構成 ](service-config-settings-overview.md) します。

### ストアフルフィルメントに接続するための資格情報を追加

1. 実稼動環境とサンドボックス環境に [ アカウント資格情報 ](enable-general.md) を設定します。

1. 管理者から、**[!UICONTROL Stores > Configuration > Services > Store Fulfillment by Walmart Commerce Technologies]** に移動します。

1. **[!UICONTROL Production environment]** ーザーに指定したアカウント資格情報を入力します。 すべてのフィールドが必要です。

1. 「**[!UICONTROL Save Config]**」を選択します。

1. **[!UICONTROL Validate Credentials]** を選択して接続をテストします。

>[!NOTE]
>
>資格情報が無効な場合は、各環境に正しい値を入力したことを確認し、再検証します。 接続で問題が解決しない場合は、アカウント担当者にお問い合わせください。
