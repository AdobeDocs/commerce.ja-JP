---
title: Onboarding [!DNL Payment Services] flow
description: いくつかのオ  [!DNL Payment Services]  ボーディング手順を完了して、インスタンスを機能と接続します。
role: User
level: Intermediate
exl-id: 1ee8c660-0941-4378-a1d7-ae45de3de211
feature: Payments, Checkout, Integration, Paas, Saas
source-git-commit: 9f7690ae325853b9b4a590b3d1cd538909a26462
workflow-type: tm+mt
source-wordcount: '591'
ht-degree: 0%

---

# オンボーディング [!DNL Payment Services] フロー

[!DNL Payment Services] の使用を開始するには、いくつかのオンボーディング手順を完了する必要があります。 正確なガイダンスを得るには、組織のインスタンスとバージョンに最も適した以下のAdobe Commerce オプションを選択してください。

次のフロー図は、すべてのバージョンで [!DNL Payment Services] をオンボーディングする一般的なプロセスを示しています。

![ オンボーディングフロー ](assets/flow-payment-services.png){width="700" zoomable="yes"}

[!DNL Payment Services] でオンボーディングする具体的なAdobe Commerceのバージョンについては、以下を参照してください。

## インスタンスとバージョンの検索をサポート

### Adobe CommerceまたはMagento Open Source | v2.4.7+

次のフロー図は、v2.4.7 より新しいAdobe CommerceまたはMagento Open Sourceを使用して [!DNL Payment Services] ーザーをオンボーディングする一般的なプロセスを示しています。

>[!BEGINTABS]

>[!TAB  サンドボックス ]

次のフロー図は、v2.4.7 より新しいAdobe CommerceまたはMagento Open Sourceを使用したオンボーディングサンドボックスプロセスを示 [!DNL Payment Services] ています。ここでは、Adobe Commerceが標準で使用されています。

![ オンボーディングフロー ](assets/flow-sandbox-configuration-onboarding-2.4.7.png){width="700" zoomable="yes"}

**バージョン v2.4.7 以降のオンボーディング手順（パート 1）：サンドボックス**

1. Commerce サービスに [ インスタンスを接続 ](connect.md#configure-commerce-services) します。 この接続は、Commerce インスタンスごとに 1 回だけ完了する必要があります。 [!BADGE PaaS のみ ]{type=Informative tooltip="クラウドプロジェクト上のAdobe Commerceにのみ適用されます（Adobeが管理する PaaS インフラストラクチャ）。"}
1. [ テスト用の PayPal 支払い処理アカウントを使用して ](sandbox.md#enable-sandbox-testing) サンドボックスサービスを設定します [ または、別の環境で機能をテストした場合は ](sandbox.md#enable-live-payments) ライブ支払いの有効化）に進みます。
1. [ サンドボックス ](sandbox.md#test-in-sandbox-environment) 環境で支払いをテストします。

[![ 詳細情報 ](assets/learn-more-button.svg)](https://helpx.adobe.com/legal/product-descriptions/payment-services-for-Adobe-Commerce-and-Magento-Open-Source-On-demand-Services.html)

>[!TAB  実稼動 ]

次のフロー図は、[!DNL Payment Services] を有効にするために必要な実稼動ステップを示しています。

![ オンボーディングフロー ](assets/flow-production-payment-services.png){width="700" zoomable="yes"}

**バージョン v2.4.7 以降のオンボーディング手順（パート 2）実稼動**

1. サンドボック  [!DNL Payment Services]  モードで [ 支払い方法として設定 ](production.md#set-payment-services-as-payment-method) し、テスト支払いの処理を開始します。
1. ライブオンボーディングを有効にする [ 支払い権限をリクエスト ](production.md#request-payments-entitlement-from-adobe)。
1. [ マーチャントのオンボーディングを完了 ](production.md#complete-merchant-onboarding) して、Commerce web サイトでライブ支払いを有効にします。
1. [ マーチャント ID [!DNL Payment Services]  取得し ](production.md#configure-pricing-tier)Sales に渡して、正しい価格レベルを設定します。
1. [ ライブモード  [!DNL Payment Services]  有効化 ](production.md#enable-live-payments) してライブ支払いの処理を開始します。
1. [ サンドボックス ](sandbox.md#test-in-sandbox-environment) 環境と [ 実稼動 ](production.md#test-in-production) 環境の両方で支払いをテストします。

[![ 詳細情報 ](assets/learn-more-button.svg)](production.md)

>[!ENDTABS]

### Adobe CommerceまたはMagento Open Source | v2.4.0～2.4.6[!BADGE PaaS のみ ]{type=Informative tooltip="クラウドプロジェクト上のAdobe Commerceにのみ適用されます（Adobeが管理する PaaS インフラストラクチャ）。"}

次のフロー図は、Adobe CommerceまたはMagento Open Source バージョン 2.4.0 ～ 2.4.6 で [!DNL Payment Services] をオンボーディングする一般的なプロセスを示しています。オンボーディングを開始するには、[!DNL Payment Services] をダウンロードしてインストールする必要があります。

>[!BEGINTABS]

>[!TAB  サンドボックス ]

次のフロー図は、Adobe CommerceまたはMagento Open Source バージョン 2.4.0 から 2.4.6 への [!DNL Payment Services] ンボーディングに必要なサンドボックスの手順を示しています。

![ オンボーディングフロー ](assets/flow-sandbox-installation-configuration-onboarding-2.4.0.png){width="700" zoomable="yes"}

**バージョン v2.4.0～2.4.6 のオンボーディング手順（パート 1）：サンドボックス**

1. [ 必要に応じて ](install.md#get-payment-services) 拡張  [!DNL Payment Services]  能をインストールします。
1. [API 資格情報を取得 ](connect.md#obtain-api-credentials)。
1. Commerce サービスに [ インスタンスを接続 ](connect.md#configure-commerce-services) します。 この接続は、Commerce インスタンスごとに 1 回だけ完了する必要があります。
1. [ テスト用の PayPal 支払い処理アカウントを使用して ](sandbox.md#enable-sandbox-testing) サンドボックスサービスを設定します [ または、別の環境で機能をテストした場合は ](sandbox.md#enable-live-payments) ライブ支払いの有効化）に進みます。
1. [ サンドボックス ](sandbox.md#test-in-sandbox-environment) 環境で支払いをテストします。

[![ 詳細情報 ](assets/learn-more-button.svg)](https://helpx.adobe.com/legal/product-descriptions/payment-services-for-Adobe-Commerce-and-Magento-Open-Source-On-demand-Services.html)

>[!TAB  実稼動 ]

次のフロー図は、Adobe CommerceまたはMagento Open Source バージョン 2.4.0 から 2.4.6 を使用した実稼動環境で [!DNL Payment Services] を有効にする一般的なプロセスを示しています。

![ オンボーディングフロー ](assets/flow-production-payment-services.png){width="700" zoomable="yes"}

**バージョン v2.4.0～2.4.6 のオンボーディング手順（パート 2）実稼動**

1. サンドボック  [!DNL Payment Services]  モードで [ 支払い方法として設定 ](production.md#set-payment-services-as-payment-method) し、テスト支払いの処理を開始します。
1. ライブオンボーディングを有効にする [ 支払い権限をリクエスト ](production.md#request-payments-entitlement-from-adobe)。
1. [ マーチャントのオンボーディングを完了 ](production.md#complete-merchant-onboarding) して、Commerce web サイトでライブ支払いを有効にします。
1. [ マーチャント ID [!DNL Payment Services]  取得し ](production.md#configure-pricing-tier)Sales に渡して、正しい価格レベルを設定します。
1. [ ライブモード  [!DNL Payment Services]  有効化 ](production.md#enable-live-payments) してライブ支払いの処理を開始します。
1. [ サンドボックス ](sandbox.md#test-in-sandbox-environment) 環境と [ 実稼動 ](production.md#test-in-production) 環境の両方で支払いをテストします。

[![ 詳細情報 ](assets/learn-more-button.svg)](onboard.md)

>[!ENDTABS]

>[!NOTE]
>
>管理者（パート 1）でCommerce サービスを設定しない場合、サンドボックスやライブ支払いを設定することはできません。

>[!MORELIKETHIS]
>
> * [ トラブルシューティング  [!DNL Payment Services]  インストール ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/payments/payservices-install.html?lang=en)
> * [PayPal サンドボックスアカウントが検証されていません ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/payments/payservices-paypal-acct.html)
> * [ 遅延レポ  [!DNL Payment Services]  トデータ ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/payments/payservices-report-info-delayed.html)
> * [ サンドボックス環境で支払いを処理する際に、PayPal でクレジットカードのテストが失敗する ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/payments/payservices-cc-sandbox-failure.html?lang=en)