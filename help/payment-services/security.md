---
title: セキュリティとコンプライアンス
description: サイトのセキュリティとコンプライアンスの要件を確認する。
exl-id: 083c5a12-1d78-48b5-b9e3-612b104ce7e0
feature: Payments, Checkout, Compliance
redirect_from: https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/security.html?lang=ja
source-git-commit: f8c44e088fa66ec506934a0155f1ff819a9db7d4
workflow-type: tm+mt
source-wordcount: '695'
ht-degree: 0%

---

# セキュリティとコンプライアンス

[!DNL Payment Services]ではセキュリティが最も重要であり、プライベートまたは支払いカード業界（PCI）で規制された情報が[!DNL Payment Services]に渡されることはありません。

## Commerce セキュリティ

[!DNL Adobe Commerce]と[!DNL Magento Open Source]には、いくつかのセキュリティ機能のサポートが含まれています。

セキュリティのベストプラクティスを確認するには、コアユーザーガイドの「[&#x200B; セキュリティ &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-admin/systems/security/security){target="_blank"}」を参照し、管理者セッションと資格情報の管理方法、CAPTCHAの実装およびweb サイト制限の管理方法について説明します。

## PCI認定

PCI （Payment Card Insutry）は、インターネット上でクレジットカードによる支払いを受け付ける企業に一連の要件を定めました。 顧客のクレジットカード情報を扱うマーチャントは、安全な環境を維持することに加えて、いくつかの標準的なガイドラインを満たす責任があります。

詳しくは、[PCI認定ガイドライン &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-admin/start/compliance/payments/compliance-pci){target="_blank"}を参照してください。

加盟店は、[自己評価アンケート（SAQ） &#x200B;](https://www.pcisecuritystandards.org/pci_security/completing_self_assessment){target="_blank"}に回答できます。これは、クレジットカード情報のセキュリティを評価するための自己検証ツールです。

### クレジットカード情報フィールド

クレジットカードのフィールドでは、PCIで規制されたデータがサービス間で渡されることはありません。 データを保存したり維持したりする必要がないため、PCI認定に関する懸念を大幅に軽減できます。

### 3DS

PCI 3-D Secure （3DS）は、オンラインでクレジットカードを購入する際に、クレジットカード発行元による購入者認証を可能にします。 この追加のセキュリティレイヤーは、オンラインでの不正行為の防止に役立ち、EU （欧州連合）のコンプライアンス規制の一部として必須です。

[!UICONTROL Payment Services]は、加盟店がEUの規制に準拠し、顧客と加盟店をストアでの不正行為から保護するための3DS機能を提供します。

3DSの準拠が必要なEUまたは英国内の加盟店である場合は、[構成管理](configure-admin.md#credit-card-fields)で3DSを手動で有効にする必要があります（デフォルトでは`Off`です）。

3DSは、**[クレジットカードのフィールド](configure-admin.md#credit-card-fields)**&#x200B;と&#x200B;**[[!DNL Google Pay]](configure-admin.md#google-pay)**&#x200B;の両方でサポートされています。 各支払い方法には、管理画面で独自の3D セキュア認証設定があります。この設定は、`Always`、`When required`、または`Off`に設定できます。

>[!IMPORTANT]
>
>3DS要件は、ビジネスとクレジットカード所有者の銀行が[欧州経済地域](https://www.efta.int/eea) （EEA）と英国に位置する取引に適用されます。 米国のマーチャントは3DSを必要としませんが、必要に応じてトランザクションに使用できます。

加盟店または店舗の担当者が購入者に対して行う注文は、3DS コンプライアンス対策で設定されません。 ただし、カード発行者が3DSを必要とする場合、[!UICONTROL Payment Services]設定に関係なく、この手順を回避することはできません。

>[!MORELIKETHIS]
>
> * 詳しくは、設定[&#128279;](configure-admin.md#3ds)の3DSを参照してください。
> * 3DS テスト用の特定のクレジットカードについて詳しくは、PayPal開発者ドキュメントの[&#x200B; テストカード &#x200B;](https://developer.paypal.com/docs/checkout/advanced/customize/3d-secure/test/)を参照してください。

### カード保管

買い物客[が店舗で今後の購入のために自分のクレジットカード情報](vaulting.md)を保管（保存）すると、最小限のクレジットカード情報が買い物客と共有されます（最後の4桁、カードの有効期限、カードのブランド）。 クレジットカード情報は決済代行会社と共に保存されます。 カードの有効期限が切れた場合、または情報を保存する必要がなくなった場合は、そのトークンを削除して、情報が支払いプロバイダーによって保存されないようにすることができます。

詳しくは、[&#x200B; クレジットカードの保管](vaulting.md)を参照してください。

### PayPal支払いボタン

PayPalの支払いボタンを使用すれば、PCIで規制されたデータがサービスをまたいで渡されることはありません。 データを保存したり維持したりする必要がないため、PCI認定に関する懸念を大幅に軽減できます。

セキュリティ上の理由から、PayPalはチェックアウト時に請求先住所を渡しません。使用される請求情報は、国、メールアドレス、名前のみです。 オプションで、サイトのPayPal チェックアウトを有効にして、PayPalに連絡して検証プロセスを完了することで、完全な請求先住所を返すことができます。

PayPalには、マシンラーニング（機械学習）を利用した不正防止も統合されています。 詳しくは、PayPalの[販売者保護ドキュメント &#x200B;](https://www.paypal.com/us/webapps/mpp/security/seller-protection)を参照してください。

## 不正行為の防止

[Signifyd拡張機能](https://commercemarketplace.adobe.com/signifyd-module-connect.html)を使用すると、決済サービスの自動不正防止を有効にできます。 詳しくは、[Signifyd詐欺防止](fraud-protection.md)を参照してください。

PayPalは、開発者ドキュメントで[詐欺防止](https://www.paypal.com/us/cshelp/article/what-is-fraud-protection-help1014){target=_blank}の他のオプションを提供しています。

* 詳しくは、[詐欺防止の詳細](https://www.paypal.com/us/enterprise/fraud-protection-advanced#fraud-protection-advanced){target=_blank}を参照してください。
* 詳しくは、[&#x200B; チャージバック保護](https://www.paypal.com/us/cshelp/article/what-is-chargeback-protection-help608){target=_blank}を参照してください。
