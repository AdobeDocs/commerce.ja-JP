---
title: 概要  [!DNL Payment Services]
description: Web サイトに自動で堅牢で安全な支払  [!DNL Payment Services]  処理ソリューションをインストールして使用する方法について説明  [!DNL Adobe Commerce]  ま  [!DNL Magento Open Source] 。
role: User
level: Intermediate
feature: Payments, Checkout
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 0%

---

# [!DNL Payment Services] の概要

[!DNL Payment Services] for [!DNL Adobe Commerce] and [!DNL Magento Open Source] は、Commerce web サイトに対して堅牢で安全な支払い処理を提供するための、サンドボックステストやシンプルなセットアップを含む、自動セルフサービスソリューションです。

この支払いソリューションは、小規模ビジネス、中堅企業、大企業を問わず、運用にかかる諸経費の削減、収益の増加、買い物客エクスペリエンス全体の改善に役立つツールの提供に役立ちます。

[!DNL Payment Services] は：

* セットアップとメンテナンスが容易
* 利益を最大化するように設計
* 安全でセキュア
* お客様のすべての支払いニーズを満たすように設計
* 管理者内での自己完結型

## 機能

>[!NOTE]
>
>ここで説明する機能の一部は、まだ GA （一般提供）リリースでは使用できない場合があります。

[!DNL Payment Services] は、オンラインチェックアウト（決済と払い戻しから支払い済みまで）のためのワンストップショップです。 購入者にとって最適なエクスペリエンスを作成するために必要なインサイトと制御を提供する強力なツールを提供します。

* [**オンボーディング**](onboard.md) – このプロセスは、商用のサインアップ、技術設定、使用権限、サンドボックス環境設定、ライブ支払いの有効化について順を追って説明します。
* [**支払いオプション**](payments-options.md) – 支払いオプションを設定して、ストア（またはマルチストア）の顧客が使用できる方法をカスタマイズします。
* **キャッシュ・フロー管理の財務レポート** - [ 支払いの詳細 ](order-payment-status.md) とオーダーを同期して、処理量、支払い残高、[ 支払い ](payouts.md)、詳細な [ トランザクション・レベルのレポート ](transactions.md) を完全に把握し、財務調整を行い、トランザクションの可視性を最大限に高めます。
* **透明な価格設定**：価格は明確かつ事前に設定されており、表示される内容が実際の価格になります。
* **効率的なチェックアウトエクスペリエンス** - [ カードヴォールティング ](vaulting.md) および [ 即時購入 ](https://experienceleague.adobe.com/docs/commerce-admin/stores-sales/point-of-purchase/checkout-instant-purchase.html) （デフォルトでAdobe Commerceで有効）機能により、迅速でシンプルなチェックアウトの障壁を取り除き、常連客を作成します。

## 対象

[!DNL Payment Services] は [!DNL Adobe Commerce] と [!DNL Magento Open Source] で使用できます。 [!DNL Payment Services] 拡張機能は、[!DNL Adobe Commerce] バージョン 2.4.4 ～ 2.4.7-p3 と互換性があります。

現在、[!DNL Payment Services] は、これらの国のすべての支払いオプションに対して（[ 高度なオンボーディング ](../payment-services/production.md#advanced-onboarding) を介して）完全なサポートを提供しています。

* 米国（米国）
* カナダ （カナダ）
* オーストラリア （AUS）
* フランス （FR）
* 英国（UK）

支払いサービスは、他の [ オンボーディング中に利用可能な国 ](../payment-services/payments-options.md) に [ エクスプレスチェックアウト機能 ](../payment-services/production.md#complete-merchant-onboarding) （支払いオプションのサブセット）を提供します。

リリースおよびバージョン固有の情報について詳しくは、[ ライフサイクルポリシー ](https://experienceleague.adobe.com/docs/commerce-operations/release/planning/lifecycle-policy.html) および [[!DNL Payment Services]  リリースノート ](release-notes.md) ページを参照してください。

### 使用可能なクレジットカードおよび通貨

[!DNL Payment Services] は、（利用可能な [ 国の通貨を受け入れ ](#availability) す。 詳しくは、[ 通貨の設定 ](https://experienceleague.adobe.com/docs/commerce-admin/stores-sales/site-store/currency/currency-configuration.html) を参照してください。

PayPal がサポートする通貨を確認するには、[ サポートされる通貨に関するドキュメント ](https://developer.paypal.com/docs/reports/reference/paypal-supported-currencies/) を参照してください。

PayPal がサポートする支払い方法を確認するには、その [ 支払い方法のドキュメント ](https://developer.paypal.com/docs/checkout/payment-methods/) を参照してください。

## 基本を学ぶ

オンボーディングと [!DNL Payment Services] の設定はほんの数手順で完了します。

1. [[!DNL Payment Services]  拡張機能 ](install.md) を取得します。
1. Commerce インスタンスをCommerce サービスに接続します。
1. オンボードし、サンドボックスサービスを設定します。
1. お支払い方法として [!DNL Payment Services] を有効にし、テスト支払い処理を開始します。
1. マーチャントのオンボーディングを完了して、web サイトのライブ支払いを有効にします。
1. ライブ モードで [!DNL Payment Services] を有効化して、ライブ支払の処理を開始します。

すべての手順を取得し、オンボーディングプロセスを開始するには、[ オンボード  [!DNL Payment Services]](onboard.md) を参照してください。

## [!DNL Payment Services] デモ

[!DNL Payment Services] について詳しくは、このビデオをご覧ください。

>[!VIDEO](https://video.tv.adobe.com/v/343990?quality=12)
