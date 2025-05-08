---
title: セキュリティとコンプライアンス
description: サイトのセキュリティおよびコンプライアンス要件を確認します。
exl-id: 083c5a12-1d78-48b5-b9e3-612b104ce7e0
feature: Payments, Checkout, Compliance
redirect_from: https://experienceleague.adobe.com/docs/commerce-merchant-services/payment-services/security.html?lang=ja
source-git-commit: 9f7690ae325853b9b4a590b3d1cd538909a26462
workflow-type: tm+mt
source-wordcount: '571'
ht-degree: 0%

---

# セキュリティとコンプライアンス

セキュリティは [!DNL Payment Services] において最も重要な懸念事項であり、プライベートまたは PCI （Payment Card Industry）で規制された情報が [!DNL Payment Services] 内に渡されることはありません。

## Commerce セキュリティ

[!DNL Adobe Commerce] と [!DNL Magento Open Source] には、複数のセキュリティ機能がサポートされています。

セキュリティのベストプラクティスを確認し、管理セッションと資格情報の管理、CAPTCHA の実装、web サイト制限の管理方法については、コアユーザーガイドの [ セキュリティ ](https://experienceleague.adobe.com/ja/docs/commerce-admin/systems/security/security){target="_blank"} を参照してください。

## PCI コンプライアンス

Payment Card Industry （PCI）は、インターネット上でクレジットカードによる支払いを受け入れる企業に対して一連の要件を確立しました。 顧客のクレジットカード情報を扱うマーチャントは、安全な環境を維持するだけでなく、いくつかの標準的なガイドラインを満たす責任があります。

詳しくは、[PCI コンプライアンスガイドライン ](https://experienceleague.adobe.com/ja/docs/commerce-admin/start/compliance/payments/compliance-pci){target="_blank"} を参照してください。

マーチャントは、カード所有者データのセキュリティを評価するための自己検証ツールである [ 自己評価アンケート （SAQ） ](https://www.pcisecuritystandards.org/pci_security/completing_self_assessment){target="_blank"} を完了できます。

### クレジットカードのフィールド

クレジットカードのフィールドを使用すると、PCI で規制されたデータがサービス全体に渡されることはありません。 データを保存または維持する必要がないので、PCI コンプライアンスの懸念が大幅に軽減されます。

### 3DS

PCI 3-D Secure （3DS）は、オンラインでのクレジットカード購入の際に、買い手がクレジットカード発行者と認証できるようにします。 この追加のセキュリティレイヤーは、オンライン詐欺の防止に役立ち、欧州連合（EU）のコンプライアンス規制の一部として必要です。

[!UICONTROL Payment Services] は、マーチャントが EU 規制に準拠し、ストア内での不正行為から顧客やマーチャントを保護するための 3DS 機能を提供します。

3DS コンプライアンスが必要な EU またはイギリスのマーチャントの場合、[ 設定 ](settings.md#credit-card-fields) で手動で 3DS をオンにする必要があります（デフォルトでは `Off` です）。

>[!IMPORTANT]
>
>3DS 要件は、ビジネスとカード所有者の銀行が [ 欧州経済地域 ](https://www.efta.int/eea) （EEA）と英国に所在する取引に適用されます。 米国のマーチャントは 3DS を必要としませんが、必要に応じて取引で有効にすることができます。

商店の担当者が購入者に対して行った注文は、3DS コンプライアンス対策で構成されていません。

>[!MORELIKETHIS]
>
> * 詳しくは、設定の [3DS](settings.md#3ds) を参照してください。
> * 3DS テスト用の特定のクレジットカードについて詳しくは、PayPal 開発者用ドキュメントの [ テストカード ](https://developer.paypal.com/docs/checkout/advanced/customize/3d-secure/test/) を参照してください。

### カードボルト

買い物客 [Vault）（クレジットカード情報を「保存」する）と ](vaulting.md) 店舗での今後の購入で、最小限のクレジットカード情報が買い物客（最後の 4 桁、カードの有効期限、カードのブランド）と共有されます。 クレジットカード情報は、支払いプロバイダに保存されます。 カードの有効期限が切れたり、情報を保存する必要がなくなった場合は、そのトークンを削除して、支払いプロバイダーが情報を保存しないようにすることができます。

詳しくは、[ クレジットカードボルト ](vaulting.md) を参照してください。

### PayPal 支払いボタン

PayPal の支払いボタンを使用すると、PCI で規制されたデータがサービス全体に渡されることはありません。 データを保存または維持する必要がないので、PCI コンプライアンスの懸念が大幅に軽減されます。

セキュリティ上の理由から、PayPal はチェックアウト時に請求先住所を渡しません。使用される請求情報は、国、メール、名前のみです。 オプションで、サイトの PayPal チェックアウトを有効にして、PayPal に連絡して検証プロセスを完了することにより、完全な請求先住所を返すことができます。

また、PayPal は、機械学習を使用して不正との戦いを支援する統合不正対策も備えています。 詳しくは、PayPal の [ 販売者保護ドキュメント ](https://www.paypal.com/us/webapps/mpp/security/seller-protection) を参照してください。

## 不正保護

[Signifyd 拡張機能 ](https://commercemarketplace.adobe.com/signifyd-module-connect.html) を使用して、支払いサービスの自動不正保護を有効にできます。 詳しくは、[ 重大な不正防止 ](fraud-protection.md) を参照してください。

PayPal は、開発者向けドキュメントに [ 不正保護 ](https://www.paypal.com/us/cshelp/article/what-is-fraud-protection-help1014){target=_blank} のその他のオプションを用意しています。

* 詳しくは、[ 不正防止の詳細 ](https://www.paypal.com/us/enterprise/fraud-protection-advanced#fraud-protection-advanced){target=_blank} を参照してください。
* 詳細は、「[ チャージバック保護 ](https://www.paypal.com/us/cshelp/article/what-is-chargeback-protection-help608){target=_blank}」を参照してください。
