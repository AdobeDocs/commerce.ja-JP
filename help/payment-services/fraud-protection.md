---
title: Signifyd Fraud Protection
description: Signifydで [!DNL Payment Services] の自動不正防止を有効にします。
role: Admin, User
level: Intermediate
feature: Payments, Checkout, Configuration, Security, Paas, Saas
exl-id: 440296bb-a6ff-408b-8195-3027916e4f84
source-git-commit: 870c2497a2d6dcfc4066c07f20169fc9040ae81a
workflow-type: tm+mt
source-wordcount: '420'
ht-degree: 0%

---

# 重要な不正利用防止

[Signifyd拡張機能](https://commercemarketplace.adobe.com/signifyd-module-connect.html)を使用して、[!DNL Payment Services]の自動不正防止を有効にできます。

Adobe Commerceは、Signifyd バージョン 5.4.0以降をサポートしています。 [!DNL Payment Services]は、事前認証および事後認証のSignifyd フローをサポートしています。

Signifyd/[!DNL Payment Services]との統合により、クレジットカード、デビットカード、アークトカード、Admin経由でのチェックアウト、PayPalおよびApple Payの支払い方法に対応しています。 決済サービスとSignifydの間で取引の詳細の一部は共有されていませんが、Signifydはすべての支払い方法に包括的なリスクカバレッジを提供し、最大限の保護を確保しています。

>[!CAUTION]
>
> [Fastlane](payments-options.md#fastlane-button)はSignifydと互換性がありません。

拡張機能のインストールと設定について詳しくは、[Signifyd ドキュメント &#x200B;](https://community.signifyd.com/support/s/article/magento-2-extension-install-guide?language=en_US#downloadandinstallingmagento2extension)を参照してください。

## オンボーディング

[!DNL Payment Services]で使用するために拡張機能をオンボーディングするには、Signifydと直接通信する必要があります。[!DNL Payment Services]の設定は必要ありません。 インストールが完了したら、AdminでSignifyd拡張機能を設定できます。 この拡張機能に関連するすべてのサポートは、Signifydによって管理されます。

Signifydでオンボーディングを行う場合は、以下を行う必要があります。

1. 新しいアカウントを設定するには、Signifydにお問い合わせください。
1. デフォルトでは、Signifydは現在サポートしていない他の支払い方法をトリガーしないように[許可リストに加える](https://github.com/signifyd/magento2/blob/main/docs/RESTRICT-PAYMENTS.md)されています。 特定の決済方法を禁止する場合は、変更する必要があります。
1. PayPalは、Signifydが承認できるPaypalの加盟店の不正利用防止オプションにより、注文を拒否しないことをSignifydに確認します。
1. Signifyd拡張機能を有効にして[!DNL Payment Services]と互換性を持たせます：
   * _Live_ モードで[!DNL Payment Services]を使用する場合、Signifydは実稼動モードである必要があります。
   * _サンドボックス_ モードで[!DNL Payment Services]を使用する場合、Signifydはテストモードである必要があります。

## 設定

Signifydは注文に対して何らかのアクションを実行するため、[!DNL Payment Services]に設定した支払いアクションに基づいて適切に動作するように拡張機能を設定する必要があります。

これらの設定オプションは、決済サービスおよびSignifyd統合と互換性がありません。

* [!DNL Payment Services]が`Authorize`支払いアクション _と_&#x200B;で設定されている場合、Signifydは`PostAuth` モードで、_[!UICONTROL Decline Guarantees]_&#x200B;オプションが&#x200B;**クレジットメモを作成**&#x200B;に設定されています。

  理由：[!DNL Payment Services]は、Signifyが返金を試みる認証トランザクションを作成します。


* [!DNL Payment Services]は`Authorize and Capture`支払いアクション _で設定されており、_ Signifydは`PostAuth` モードで、_[!UICONTROL Decline Guarantees]_&#x200B;オプションが&#x200B;**注文をキャンセル**&#x200B;に設定されています。

  理由：[!DNL Payment Services]は、Signifydが無効化しようとするキャプチャ トランザクションを作成します。


拡張機能の設定[について詳しくは、Signifydのドキュメントを参照してください](https://community.signifyd.com/support/s/article/magento-2-extension-install-guide?language=en_US#configuringmagento2extension)。

注文ワークフローについて詳しくは、[に関するSignifydのドキュメントを参照してください](https://community.signifyd.com/support/s/article/magento-2-extension-install-guide?language=en_US#howmagento2works)。
