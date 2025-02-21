---
title: オンボード  [!DNL Payment Services]
description: いくつかのオ  [!DNL Payment Services]  ボーディング手順を完了して、インスタンスを機能と接続します。
role: User
level: Intermediate
feature: Payments, Checkout, Integration
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '336'
ht-degree: 0%

---

# Onboard [!DNL Payment Services]

[!DNL Adobe Commerce] および [!DNL Magento Open Source] で [!DNL Payment Services] の使用を開始するには、インスタンスを支払機能に接続するためにいくつかのオンボーディング手順を完了する必要があります。

## オンボーディングフロー

次のフロー図は、[!DNL Payment Services] ーザーをオンボーディングする一般的なプロセスを示しています。

![ オンボーディングフロー ](assets/onboarding-diagram.svg){width="600" zoomable="yes"}

>[!NOTE]
>
> Adobe Commerce バージョン 2.4.7 以降では、標準搭載の [!DNL Payment Services] が用意されているので、Marketplace 拡張機能の手順をスキップできます。

サンドボックスまたはライブ支払いのオンボーディングを完了すると、管理者の [!DNL Payment Services] から財務レポートにアクセスできます。

サンドボックスとライブ支払の両方がオンボーディングされ、有効になっている場合は、[!DNL Payment Services] ホームからこれらのモードを簡単に切り替えることができます。

## 前提条件

[!DNL Payment Services] を使用するには、すべての依存モジュールを有効にして、インスタンスで次の機能を使用できるようにする必要があります。

* サービスコネクタモジュール
* サービス ID モジュール
* API キー

サービスコネクタとサービス ID モジュールは、[ のインストール  [!DNL Payment Services]](install.md) 中に自動的にインストールされます。

インストールが完了したら、**[!UICONTROL Services]** - **[!UICONTROL Commerce Services Connector]** を展開すると、設定（**[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**）に新しいセクションが表示されます。

API キーを作成する方法や API キーにアクセスする方法については、[API 資格情報 ](#obtain-api-credentials) を参照してください。

## オンボーディング手順

1. [ 拡張機能をイ  [!DNL Payment Services]  ストールします ](install.md#get-payment-services)。
1. [API 資格情報を取得 ](connect.md#obtain-api-credentials)。
1. Commerce サービスに [ インスタンスを接続 ](connect.md#configure-commerce-services) します。 この接続は、Commerce インスタンスごとに 1 回だけ完了する必要があります。
1. [ テスト用の PayPal 支払い処理アカウントを使用して ](sandbox.md#enable-sandbox-testing) サンドボックスサービスを設定します [ または、別の環境で機能をテストした場合は ](sandbox.md#enable-live-payments) ライブ支払いの有効化）に進みます。
1. サンドボック  [!DNL Payment Services]  モードで [ 支払い方法として設定 ](production.md#set-payment-services-as-payment-method) し、テスト支払いの処理を開始します。
1. ライブオンボーディングを有効にする [ 支払い権限をリクエスト ](production.md#request-payments-entitlement-from-adobe)。
1. [ マーチャントのオンボーディングを完了 ](production.md#complete-merchant-onboarding) して、Commerce web サイトでライブ支払いを有効にします。
1. [ マーチャント ID [!DNL Payment Services]  取得し ](production.md#configure-pricing-tier)Sales に渡して、正しい価格レベルを設定します。
1. [ ライブモード  [!DNL Payment Services]  有効化 ](production.md#enable-live-payments) してライブ支払いの処理を開始します。
1. [ サンドボックス ](sandbox.md#test-in-sandbox-environment) 環境と [ 実稼動 ](production.md#test-in-production) 環境の両方で支払いをテストします。

>[!NOTE]
>
>管理者でCommerce サービスを設定しない場合（手順 3）、サンドボックスやライブ支払いを設定することはできません。

## トラブルシューティング

* [ トラブルシューティング  [!DNL Payment Services]  インストール ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/payments/payservices-install.html?lang=en)
* [PayPal サンドボックスアカウントが検証されていません ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/payments/payservices-paypal-acct.html)
* [ 遅延レポ  [!DNL Payment Services]  トデータ ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/payments/payservices-report-info-delayed.html)
* [ サンドボックス環境で支払いを処理する際に、PayPal でクレジットカードのテストが失敗する ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/payments/payservices-cc-sandbox-failure.html?lang=en)
