---
title: 重大な不正保護
description: Signifyd を使用した  [!DNL Payment Services]  の自動不正保護を有効にします。
role: Admin, User
level: Intermediate
feature: Payments, Checkout, Configuration, Security, Paas, Saas
exl-id: 440296bb-a6ff-408b-8195-3027916e4f84
source-git-commit: 5271668c99e7a66fbe857cd3ae26edfa54211621
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 0%

---

# 重大な不正保護

[Signifyd 拡張機能 ](https://commercemarketplace.adobe.com/signifyd-module-connect.html) を使用して、[!DNL Payment Services] の自動不正保護を有効にできます。

Adobe Commerceは、Signifyd バージョン 5.4.0 以降をサポートしています。 [!DNL Payment Services] では、認証前および認証後の Signifyd フローをサポートしています。

Signifyd と [!DNL Payment Services] の統合により、クレジットカード、デビットカード、ボールトカード、管理者によるチェックアウト、PayPal およびApple Pay の支払い方法がサポートされます。 取引の詳細は Payment Services と Signifyd の間で共有されていませんが、Signifyd はすべての支払い方法に包括的なリスクカバレッジを提供し、最大限の保護を確保しています。

拡張機能のインストールと設定について詳しくは、[Signifyd のドキュメント ](https://community.signifyd.com/support/s/article/magento-2-extension-install-guide?language=en_US#downloadandinstallingmagento2extension) を参照してください。

## オンボーディング

[!DNL Payment Services] で使用する拡張機能をオンボーディングするには、Signifyd と直接通信する必要があります。[!DNL Payment Services] の設定は必要ありません。 インストールが完了したら、管理者で Signifyd 拡張機能を設定できます。 この拡張機能に関連するすべてのサポートは、Signifyd によって管理されます。

Signifyd でオンボーディングする場合、次の操作が必要です。

1. 新しいアカウントを設定する場合は、Signifyd にお問い合わせください。
1. Signifyd は現在サポートしていない他のお支払い方法をトリガーしないように ](https://github.com/signifyd/magento2/blob/main/docs/RESTRICT-PAYMENTS.md) デフォルトで [許可リストに加えるされています。 特定の支払い方法を禁止する場合は、変更を加える必要があります。
1. PayPal が承認できる Paypal のマーチャントの不正防止の設定を介して、PayPal が注文を拒否しないことを Signifyd に確認します。
1. [!DNL Payment Services] と互換性を持たせるために Signifyd 拡張機能を有効にします。
   * [!DNL Payment Services] を _ライブ_ モードで使用する場合、Signifyd は実稼動モードになっている必要があります。
   * [!DNL Payment Services] を _サンドボックス_ モードで使用する場合、Signifyd はテストモードになっている必要があります。

## 設定

Signifyd は注文に対して何らかのアクションを実行するので、[!DNL Payment Services] に設定した支払いアクションに基づいて適切に動作するように拡張機能を設定する必要があります。

以下の設定オプションは、支払いサービスおよび Signifyd の統合と互換性がありません。

* `Authorize` 支払アクション _および_ で [!DNL Payment Services] が設定されている場合、Signifyd は _[!UICONTROL Decline Guarantees]_オプションが&#x200B;**クレジットメモを作成**に設定された `PostAuth` モードです。

  理由：[!DNL Payment Services] によって認証取引が作成され、Signify によって払戻が試行されます。


* [!DNL Payment Services] は `Authorize and Capture` 支払いアクション _で構成され_ Signifyd は _[!UICONTROL Decline Guarantees]_オプションが&#x200B;**注文のキャンセル**に設定された `PostAuth` モードです。

  理由：[!DNL Payment Services] は、Signifyd が無効化を試行する取得トランザクションを作成します。


[ 拡張機能の設定 ](https://community.signifyd.com/support/s/article/magento-2-extension-install-guide?language=en_US#configuringmagento2extension) については、Signifyd のドキュメントを参照してください。

詳しくは、Signifyd のドキュメント [ 注文ワークフローの詳細 ](https://community.signifyd.com/support/s/article/magento-2-extension-install-guide?language=en_US#howmagento2works) を参照してください。
