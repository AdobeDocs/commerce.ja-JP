---
title: インスタンスの接続
description: API キーと秘密鍵を使用してCommerce インスタンスを接続し、設定でデータスペースを指定します。
exl-id: 5038fd31-bac5-419e-a172-66919a9b5272
feature: Payments, Checkout, Configuration, Paas
badgePaas: label="PaaSのみ" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce on Cloud プロジェクト（Adobeで管理されるPaaS インフラストラクチャ）とオンプレミス プロジェクトにのみ適用されます。"
source-git-commit: 73814f5ac5d53399131263f47e170e612643e903
workflow-type: tm+mt
source-wordcount: '698'
ht-degree: 0%

---


# インスタンスの接続

API キーと秘密鍵を使用してCommerce インスタンスを接続し、[Commerce Services Connector](../landing/saas.md)を使用して設定のデータスペースを指定します。 **この接続は1回だけ設定されています。**

>[!VIDEO](https://video.tv.adobe.com/v/3447835)

>[!INFO]
>
> 詳しくは、[[!DNL Adobe Commerce]  サービスコネクタ ](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/admin/adobe-commerce-services/configure-adobe-commerce-services-connector)のビデオを参照してください。

* *すでにインスタンスを接続している場合*、API資格情報を取得して使用し、Commerce サービスを設定することで、テストサンドボックスの設定[に進むことができます](sandbox.md)。
* まだ&#x200B;*インスタンスを接続する必要がある場合*&#x200B;は、[API資格情報の取得](#obtain-api-credentials)および[Commerce サービスの設定](#configure-commerce-services)に関するこのトピックの情報を参照してください。
* インスタンスが接続されているかどうかわからない&#x200B;*場合*、**System** > Services > **Commerce Services Connector**&#x200B;に移動し、[!UICONTROL Sandbox Keys]および[!UICONTROL Production Keys] セクションの公開および非公開のAPI キー値、および&#x200B;*Project*&#x200B;および&#x200B;*Data Space* フィールドを[!UICONTROL SaaS Identifier] セクションで表示します。 これらの値が存在する場合は、インスタンスが接続されます。

>[!NOTE]
>
>決済サービスの資格を持つすべてのマーチャントは、1つの実稼動データスペースと2つのテストデータスペースを使用できます。

## API資格情報の取得

Commerce SaaS サービスを利用するには、インスタンスのAPI キー（Commerceの公開API キーと秘密鍵）をサンドボックスと実稼動環境の両方に使用する必要があります。サンドボックスと実稼動環境は、[ マイアカウントダッシュボード ](https://account.magento.com/customer/account/login)で作成および管理されます。 [ キーペア ](https://experienceleague.adobe.com/en/docs/commerce-admin/config/services/saas)は、Commerce アカウント（サンドボックス用と実稼動用）に作成できますが、一度にアクティブに使用できるのは1つのペアのみです。

>[!NOTE]
>
>[!UICONTROL My Account] ダッシュボードへのアクセスに関するサポートが必要ですか？ [Commerce アカウントの作成](https://experienceleague.adobe.com/en/docs/commerce-admin/start/commerce-account/commerce-account-create)を参照してください。

公開用API キーは、一度作成すれば、常にマイアカウントダッシュボードで使用できます。 必要に応じてコピーまたは削除できます。 プライベート API キーは、サンドボックスまたは実稼動用のパブリック API キーを作成すると表示されます。これは、コピーまたは保存のダイアログボックスでのみ使用でき、後からアクセスすることはできません。

特定のAPI キーペアは、環境内のすべてのCommerce サービスに対して有効なので、インスタンスに対してCommerce サービスが既に設定されている場合、API キーペアは既にCommerce サービスコネクタに存在します。

API キーが失われた場合は、新しいAPI キーペアを[生成](../landing/saas.md#genapikey)し、[適用](../landing/saas.md#createsaasenv)してAdminのCommerce Services Connector設定にする必要があります。 誤ったキーが設定されているか、設定に存在しない場合は、アカウントが確認されていないことを通知するアカウント確認エラーダイアログがPayment Servicesに表示されます。

API](../landing/saas.md#availableservices)を使用する利用可能なCommerce サービスの[一覧を参照してください。

サンドボックス環境または実稼動環境のAPI キーを生成する方法については、[資格情報](../landing/saas.md#apikey)を参照してください。

>[!IMPORTANT]
>
>API キーペア *および*&#x200B;を再生成して、アクティブな実稼動インスタンスのSaaS IDおよび/またはデータ領域を変更しないことをお勧めします。 インスタンスのデータが変更された場合、そのデータは失われます。

## Commerce サービスの設定

同じAPI キーをインスタンス間で使用できますが、各インスタンスには独自の[SaaS データスペース ](../landing/saas.md#saasenv)が必要です。

>[!NOTE]
>
>加盟店は、支払い資格にMageIDで生成された同じキーを使用する必要があります。

認証情報を取得したら、SaaS プロジェクトとSaas データスペースを設定できます。

1. _管理者_ サイドバーで、**[!UICONTROL Sales]** > **[!UICONTROL [!DNL Payment Services]]**&#x200B;に移動します。
1. **[!UICONTROL Configure Commerce Services]**&#x200B;をクリックします。

   このオプションは、アカウントにCommerce サービスをまだ設定していない場合に表示されます。

   管理者の&#x200B;**[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**>**[!UICONTROL Commerce Services Connector]**の設定領域に移動して、Commerce Services Connectorを設定します。

1. Commerce サービスを設定するには、[SaaS設定](../landing/saas.md#saasenv)に記載されている手順に従います。

   >[!INFO]
   >
   > 詳しくは、[[!DNL Adobe Commerce]  サービスコネクタ ](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/admin/adobe-commerce-services/configure-adobe-commerce-services-connector#configuration-faqs)のビデオを参照してください。

## エンドポイント

[!DNL Payment Services]は[Commerce Services Connector](../landing/saas.md)を使用してCommerce Servicesに接続し、SaaSとしてデプロイします。 この[!DNL Commerce Services Connector]は、次のエンドポイントを通じて通信します。

* サンドボックス環境の`commerce-beta.adobe.io`。
* ライブ環境の`commerce.adobe.io for`。
