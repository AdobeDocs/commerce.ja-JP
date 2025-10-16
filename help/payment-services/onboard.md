---
title: Onboarding [!DNL Payment Services] flow
description: いくつかのオ  [!DNL Payment Services]  ボーディング手順を完了して、インスタンスを機能と接続します。
role: User
level: Intermediate
exl-id: 1ee8c660-0941-4378-a1d7-ae45de3de211
feature: Payments, Checkout, Integration, Paas, Saas
source-git-commit: 999407f00b118441abe39209a15f587ec73fa75d
workflow-type: tm+mt
source-wordcount: '595'
ht-degree: 0%

---

# オンボーディング [!DNL Payment Services] フロー

[!DNL Payment Services] の使用を開始するには、いくつかのオンボーディング手順を完了する必要があります。 正確なガイダンスを得るには、組織のインスタンスとバージョンに最も適した以下のAdobe Commerce オプションを選択してください。

次のフロー図は、すべてのバージョンで [!DNL Payment Services] をオンボーディングする一般的なプロセスを示しています。

![&#x200B; オンボーディングフロー &#x200B;](assets/flow-payment-services.png){width="700" zoomable="yes"}

[!DNL Payment Services] でオンボーディングする具体的なAdobe Commerceのバージョンについては、以下を参照してください。

## インスタンスとバージョンの検索をサポート

### Adobe CommerceまたはMagento Open Source | v2.4.7+

次のフロー図は、v2.4.7 より新しいAdobe CommerceまたはMagento Open Sourceを使用して [!DNL Payment Services] ーザーをオンボーディングする一般的なプロセスを示しています。

>[!BEGINTABS]

>[!TAB  サンドボックス ]

次のフロー図は、v2.4.7 より新しいAdobe CommerceまたはMagento Open Sourceを使用したオンボーディングサンドボックスプロセスを示 [!DNL Payment Services] ています。ここでは、Adobe Commerceが標準で使用されています。

![&#x200B; オンボーディングフロー &#x200B;](assets/flow-sandbox-configuration-onboarding-2.4.7.png){width="700" zoomable="yes"}

**バージョン v2.4.7 以降のオンボーディング手順（パート 1）：サンドボックス**

1. Commerce サービスに [&#x200B; インスタンスを接続 &#x200B;](connect.md#configure-commerce-services) します。 この接続は、Commerce インスタンスごとに 1 回だけ完了する必要があります。 [!BADGE PaaS のみ &#x200B;]{type=Informative tooltip="クラウドプロジェクト上のAdobe Commerceにのみ適用されます（Adobeが管理する PaaS インフラストラクチャ）。"}
1. [&#x200B; テスト用の PayPal 支払い処理アカウントを使用して &#x200B;](sandbox.md#enable-sandbox-testing) サンドボックスサービスを設定します [&#x200B; または、別の環境で機能をテストした場合は &#x200B;](sandbox.md#enable-live-payments) ライブ支払いの有効化）に進みます。
1. [&#x200B; サンドボックス &#x200B;](sandbox.md#test-in-sandbox-environment) 環境で支払いをテストします。

[![&#x200B; 詳細情報 &#x200B;](assets/learn-more-button.svg)](https://helpx.adobe.com/legal/product-descriptions/payment-services-for-Adobe-Commerce-and-Magento-Open-Source-On-demand-Services.html)

>[!TAB  実稼動 ]

次のフロー図は、[!DNL Payment Services] を有効にするために必要な実稼動ステップを示しています。

![&#x200B; オンボーディングフロー &#x200B;](assets/flow-production-payment-services.png){width="700" zoomable="yes"}

**バージョン v2.4.7 以降のオンボーディング手順（パート 2）実稼動**

1. サンドボック [&#x200B; モードで  [!DNL Payment Services]  支払い方法として設定 &#x200B;](production.md#set-payment-services-as-payment-method) し、テスト支払いの処理を開始します。
1. ライブオンボーディングを有効にする [&#x200B; 支払い権限をリクエスト &#x200B;](production.md#request-payments-entitlement-from-adobe)。
1. [&#x200B; マーチャントのオンボーディングを完了 &#x200B;](production.md#complete-merchant-onboarding) して、Commerce web サイトでライブ支払いを有効にします。
1. [&#x200B; マーチャント ID [!DNL Payment Services]  取得し &#x200B;](production.md#configure-pricing-tier)Sales に渡して、正しい価格レベルを設定します。
1. [&#x200B; ライブモード  [!DNL Payment Services]  有効化 &#x200B;](production.md#enable-live-payments) してライブ支払いの処理を開始します。
1. [&#x200B; サンドボックス &#x200B;](sandbox.md#test-in-sandbox-environment) 環境と [&#x200B; 実稼動 &#x200B;](production.md#test-in-production) 環境の両方で支払いをテストします。

[![&#x200B; 詳細情報 &#x200B;](assets/learn-more-button.svg)](production.md)

>[!ENDTABS]

### Adobe CommerceまたはMagento Open Source | v2.4.0～2.4.6[!BADGE PaaS のみ &#x200B;]{type=Informative tooltip="クラウドプロジェクト上のAdobe Commerceにのみ適用されます（Adobeが管理する PaaS インフラストラクチャ）。"}

次のフロー図は、Adobe CommerceまたはMagento Open Source バージョン 2.4.0 ～ 2.4.6 で [!DNL Payment Services] をオンボーディングする一般的なプロセスを示しています。オンボーディングを開始するには、[!DNL Payment Services] をダウンロードしてインストールする必要があります。

>[!BEGINTABS]

>[!TAB  サンドボックス ]

次のフロー図は、Adobe CommerceまたはMagento Open Source バージョン 2.4.0 から 2.4.6 への [!DNL Payment Services] ンボーディングに必要なサンドボックスの手順を示しています。

![&#x200B; オンボーディングフロー &#x200B;](assets/flow-sandbox-installation-configuration-onboarding-2.4.0.png){width="700" zoomable="yes"}

**バージョン v2.4.0～2.4.6 のオンボーディング手順（パート 1）：サンドボックス**

1. [&#x200B; 必要に応じて  [!DNL Payment Services]  拡張 &#x200B;](install.md#get-payment-services) 能をインストールします。
1. [API 資格情報を取得 &#x200B;](connect.md#obtain-api-credentials)。
1. Commerce サービスに [&#x200B; インスタンスを接続 &#x200B;](connect.md#configure-commerce-services) します。 この接続は、Commerce インスタンスごとに 1 回だけ完了する必要があります。
1. [&#x200B; テスト用の PayPal 支払い処理アカウントを使用して &#x200B;](sandbox.md#enable-sandbox-testing) サンドボックスサービスを設定します [&#x200B; または、別の環境で機能をテストした場合は &#x200B;](sandbox.md#enable-live-payments) ライブ支払いの有効化）に進みます。
1. [&#x200B; サンドボックス &#x200B;](sandbox.md#test-in-sandbox-environment) 環境で支払いをテストします。

[![&#x200B; 詳細情報 &#x200B;](assets/learn-more-button.svg)](https://helpx.adobe.com/legal/product-descriptions/payment-services-for-Adobe-Commerce-and-Magento-Open-Source-On-demand-Services.html)

>[!TAB  実稼動 ]

次のフロー図は、Adobe CommerceまたはMagento Open Source バージョン 2.4.0 から 2.4.6 を使用した実稼動環境で [!DNL Payment Services] を有効にする一般的なプロセスを示しています。

![&#x200B; オンボーディングフロー &#x200B;](assets/flow-production-payment-services.png){width="700" zoomable="yes"}

**バージョン v2.4.0～2.4.6 のオンボーディング手順（パート 2）実稼動**

1. サンドボック [&#x200B; モードで  [!DNL Payment Services]  支払い方法として設定 &#x200B;](production.md#set-payment-services-as-payment-method) し、テスト支払いの処理を開始します。
1. ライブオンボーディングを有効にする [&#x200B; 支払い権限をリクエスト &#x200B;](production.md#request-payments-entitlement-from-adobe)。
1. [&#x200B; マーチャントのオンボーディングを完了 &#x200B;](production.md#complete-merchant-onboarding) して、Commerce web サイトでライブ支払いを有効にします。
1. [&#x200B; マーチャント ID [!DNL Payment Services]  取得し &#x200B;](production.md#configure-pricing-tier)Sales に渡して、正しい価格レベルを設定します。
1. [&#x200B; ライブモード  [!DNL Payment Services]  有効化 &#x200B;](production.md#enable-live-payments) してライブ支払いの処理を開始します。
1. [&#x200B; サンドボックス &#x200B;](sandbox.md#test-in-sandbox-environment) 環境と [&#x200B; 実稼動 &#x200B;](production.md#test-in-production) 環境の両方で支払いをテストします。

[![&#x200B; 詳細情報 &#x200B;](assets/learn-more-button.svg)](onboard.md)

>[!ENDTABS]

>[!NOTE]
>
>管理者（パート 1）でCommerce サービスを設定しない場合、サンドボックスやライブ支払いを設定することはできません。

>[!MORELIKETHIS]
>
> * [&#x200B; トラブルシューティング  [!DNL Payment Services]  インストール &#x200B;](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/payments/payservices-install.html?lang=en)
> * [PayPal サンドボックスアカウントが検証されていません &#x200B;](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/payments/payservices-paypal-acct.html)
> * [&#x200B; 遅延レポ  [!DNL Payment Services]  トデータ &#x200B;](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/payments/payservices-report-info-delayed.html)
> * [&#x200B; サンドボックス環境で支払いを処理する際に、PayPal でクレジットカードのテストが失敗する &#x200B;](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/payments/payservices-cc-sandbox-failure.html?lang=en)
> * [&#x200B; 拡張機能  [!DNL Payment Services]  無効にする &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/configure-store/extensions#manage-extensions-1)