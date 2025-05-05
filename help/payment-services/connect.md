---
title: インスタンスの接続
description: API キーと秘密鍵を使用してCommerce インスタンスを接続し、設定内のデータスペースを指定します。
feature: Payments, Checkout, Configuration, Saas
exl-id: f2b3be02-e9dd-4bca-b9e4-c80a56bf8691
source-git-commit: 16bd0e7ed1e8982e1571e2593115824a2004b7dc
workflow-type: tm+mt
source-wordcount: '636'
ht-degree: 0%

---

# インスタンスの接続

[!DNL Payment Services] はCommerce サービスを活用し、SaaS （software as a service）としてデプロイされます。 API キーと秘密鍵を使用してCommerce インスタンスを接続し、[Commerce サービスコネクタ ](https://experienceleague.adobe.com/docs/commerce/user-guides/saas.html) を使用して、設定のデータスペースを指定します。 **この接続は 1 回だけ設定します。**

>[!VIDEO](https://video.tv.adobe.com/v/3448018?captions=jpn)

>[!INFO]
>
> 詳しくは、[[!DNL Adobe Commerce]  サービスコネクタ ](https://experienceleague.adobe.com/docs/commerce-learn/tutorials/admin/adobe-commerce-services/configure-adobe-commerce-services-connector.html?lang=ja) ビデオを参照してください。

* *既にインスタンスに接続している* 場合は、API 資格情報を取得して使用し、Commerce サービスを設定すると、[ テストサンドボックスの設定 ](https://experienceleague.adobe.com/docs/commerce/payment-services/get-started/sandbox.html?lang=ja) に進むことができます。
* *インスタンスを接続する必要がある* 場合は、このトピックの [API 資格情報の取得 ](#obtain-api-credentials) および [Commerce サービスの設定 ](#configure-commerce-services) を参照してください。
* *インスタンスが接続されているかどうかわからない* 場合は、**System** / サービス / **Commerce サービスコネクタ** に移動し、「[!UICONTROL Sandbox Keys]」セクションと「[!UICONTROL Production Keys]」セクションの公開鍵と秘密鍵の API キーの値を確認し、「[!UICONTROL SaaS Identifier]」セクションの「*プロジェクト*」フィールドと「*データスペース*」フィールドを確認します。 これらの値が存在する場合、インスタンスが接続されています。

>[!NOTE]
>
>支払いサービスの資格を持つすべてのマーチャントは、1 つの実稼動データスペースと 2 つのテストデータスペースを使用できます。

## API 資格情報の取得

Commerce SaaS サービスを使用するには、サンドボックスと実稼働環境の両方でインスタンスの API キー（Commerce公開 API キーと秘密キー）を使用する必要があります。このキーは、[ マイアカウントダッシュボード ](https://account.magento.com/customer/account/login) で作成および管理されます。 [ キーペア ](https://experienceleague.adobe.com/ja/docs/commerce-admin/config/services/saas) はCommerce アカウント用に作成できます（サンドボックス用に 1 つ、実稼動用に 1 つ）。ただし、一度にアクティブに使用できるペアは 1 つだけです。

>[!NOTE]
>
>[!UICONTROL My Account] ダッシュボードへのアクセスに関するサポートが必要な場合は、 [Commerce アカウントの作成 ](https://experienceleague.adobe.com/ja/docs/commerce-admin/start/commerce-account/commerce-account-create) を参照してください。

公開 API キーを作成すると、常にマイアカウントダッシュボードで使用できるようになります。 必要に応じて、コピーまたは削除できます。 秘密 API キーは、サンドボックスまたは実稼動用の公開 API キーを作成する際に表示されます。結果として表示されるダイアログボックスからのコピーまたは保存にのみ使用でき、後でアクセスすることはできません。

指定された API キーペアは、環境内のすべてのCommerce Services で有効です。そのため、お使いのインスタンスに既にCommerce Services が設定されている場合、API キーペアは既にCommerce Services コネクタに存在します。

API キーが失われた場合は、新しい API キーペアを [ 生成 ](https://experienceleague.adobe.com/docs/commerce/payment-services/get-started/connect.html?lang=ja#generate-an-api-key-and-private-key) および [ 適用 ](https://experienceleague.adobe.com/docs/commerce/payment-services/get-started/connect.html?lang=ja#configure-saas-project) して、管理者のCommerce サービスコネクタ設定に送信する必要があります。 間違ったキーが設定されている場合、または設定に何も存在しない場合、アカウントが検証されなかったことを通知するアカウント検証エラーダイアログが支払いサービスに表示されます。

[API を使用する使用可能なCommerce サービスのリスト ](https://experienceleague.adobe.com/ja/docs/commerce/user-guides/integration-services/saas#availableservices) を参照してください。

サンドボックス環境または実稼動環境用の API キーを生成する方法については、[ 資格情報 ](https://experienceleague.adobe.com/docs/commerce/user-guides/saas.html#apikey) を参照してください。

>[!IMPORTANT]
>
>アクティブな実稼動インスタンスで API キーペアを再生成したり *SaaS 識別子やデータ領域を変更したりしない* ことをお勧めします。 インスタンスが変更されると、そのインスタンスのデータは失われます。

## Commerce サービスの設定

同じ API キーを複数のインスタンスで使用できますが、各インスタンスには独自の [SaaS Data Space](https://experienceleague.adobe.com/docs/commerce/user-guides/saas.html#saasenv) が必要です。

>[!NOTE]
>
>マーチャントは、支払い権限に MageID 用に生成されたのと同じキーを使用する必要があります。

認証情報を取得したので、SaaS プロジェクトと Saas データ領域を設定できます。

1. _管理者_ サイドバーで、**[!UICONTROL Sales]**/**[!UICONTROL [!DNL Payment Services]]** に移動します。
1. 「**[!UICONTROL Configure Commerce Services]**」をクリックします。

   このオプションは、アカウントにCommerce サービスをまだ設定していない場合に表示されます。

   Commerce Services Connector を設定するには、管理者（**[!UICONTROL Stores]**/_[!UICONTROL Settings]_/**[!UICONTROL Configuration]**/**[!UICONTROL Commerce Services Connector]**）の設定領域に移動します。

1. Commerce サービスを設定するには、[SaaS 設定 ](https://experienceleague.adobe.com/docs/commerce/user-guides/integration-services/saas.html?lang=ja#saasenv) に記載されている手順に従ってください。

   >[!INFO]
   >
   > 詳しくは、[[!DNL Adobe Commerce]  サービスコネクタ ](https://experienceleague.adobe.com/docs/commerce-learn/tutorials/admin/adobe-commerce-services/configure-adobe-commerce-services-connector.html?lang=ja#configuration-faqs) ビデオを参照してください。

## エンドポイント

[!DNL Payment Services] は、[Commerce サービスコネクタ ](https://experienceleague.adobe.com/docs/commerce/user-guides/saas.html) を使用してCommerce サービスに接続し、SaaS としてデプロイします。 この [!DNL Commerce Services Connector] は、次の場所にあるエンドポイントを通じて通信します。

* サンドボックス環境用の `commerce-beta.adobe.io`。
* ライブ環境の `commerce.adobe.io for`。
