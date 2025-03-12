---
title: '[!DNL Payment Services] リリースノート'
description: すべてのリリースについて詳しくは、リリースノ  [!DNL Payment Services]  トを参照してください。
feature: Payments, Release Notes
exl-id: 1d24ae27-4a57-4482-a36b-22bbcaaa1b6f
source-git-commit: 0ad77dca302d467ad5f037f0cd567e18bd148af0
workflow-type: tm+mt
source-wordcount: '3644'
ht-degree: 0%

---

# リリースノート

このリリースノートは、[!DNL Payment Services] の初期リリースを説明するもので、次のものが含まれます。

![ 新機能 ](../assets/new.svg) 新機能
![ 修正された問題 ](../assets/fix.svg) 修正および改善
![ 既知の問題 ](../assets/bug.svg)

通常の機能リリースバージョン以外でリリースされた機能の変更と修正については、_ホストサービスのアップデート_ の節を参照してください。

今後のリリース、製品のサポート、[!DNL Payment Services] 拡張機能をサポートするAdobe Commerce バージョンについて詳しくは、Adobe Commerce [ リリーススケジュール ](https://experienceleague.adobe.com/en/docs/commerce-operations/release/planning/schedule) および [ 製品の可用性 ](https://experienceleague.adobe.com/en/docs/commerce-operations/release/product-availability) のトピックを参照してください。

## ホステッド サービスの更新

これらのリリースノートでは、ホステッド サービスの通常の機能リリースの外部で発生した機能の変更と修正について説明します。

+++ホステッド サービスの更新

_2024 年 8 月 30 日_

![ 新しい問題 ](../assets/new.svg)<!-- Issue PAY-5658 --> マーチャントは、[ トランザクションレポート ](https://experienceleague.adobe.com/docs/commerce/payment-services/reporting/transactions.html) の支払詳細でトランザクションをフィルタリングして、より詳細で正確な支払方法のデータを取得できるようになりました。

_2024 年 7 月 15 日_

![ 新しい問題 ](../assets/new.svg)<!-- Issue PAY-5571 --> マーチャントは、[ トランザクションレポート ](https://experienceleague.adobe.com/docs/commerce/payment-services/reporting/transactions.html) のCommerce顧客メールでトランザクションをフィルタリングできるようになりました。 特定の電子メールのトランザクションをフィルタリングする顧客の電子メールを入力します。

_2024 年 7 月 9 日_

![ 新しい問題 ](../assets/new.svg)<!-- Issue PAY-5488 --> マーチャントは、[ トランザクションレポート ](https://experienceleague.adobe.com/docs/commerce/payment-services/reporting/transactions.html) の列としてCommerce顧客 ID を表示することで、特定の顧客が実行した取引を特定できるようになりました。 さらに、マーチャントは、このCommerce顧客 ID でトランザクションレポートをフィルタリングして、関連する注文を確認できます。

_2024 年 3 月 5 日_

![ 問題を修正 ](../assets/fix.svg)<!-- Issue PAY-5252 --> 単一セルの内容を選択することで、マーチャントがダッシュボードグリッドからデータをコピーできるようになりました。

_2023 年 10 月 10 日_

![ 新規問題 ](../assets/fix.svg)<!-- Issue PAY-4888 --> マーチャントは、[ 取引レポート ](https://experienceleague.adobe.com/docs/commerce/payment-services/reporting/transactions.html) のカード番号の最後の 4 桁でクレジットおよびデビットカード取引をフィルタリングできるようになりました。

_2023 年 7 月 12 日_

![ 修正された問題 ](../assets/fix.svg)<!-- Issue PAY-4587 --> [!DNL Payment Services] 2.1.0 リリースで導入された、以前の拡張機能バージョンで設定された認証ボイドが解決されるようになりました。 [!DNL Payment Services] の任意のバージョンを使用するマーチャントは、認証を無効にすることができます。

_2023 年 6 月 9 日_

![ 新規 ](../assets/new.svg)<!-- Issue PAY-4288 --> 現在、マーチャントは、[_設定のみ_ PayPal 支払いボタン ](https://experienceleague.adobe.com/docs/commerce/payment-services/payments-checkout/payments-options.html#use-only-paypal-payment-buttons) を使用できます _PayPal クレジットカード支払いオプションは使用できません_。 これにより、マーチャントは、Venmo や PayPal の支払いボタンなど様々な支払いオプションを提供したり、PayPal のクレジットカード支払いオプションの代わりに既存のクレジットカード会社を使用したりできます。

![ 新規 ](../assets/new.svg)<!-- Issue PAY-4050 --> 支払いサービスのホームに表示される、注文の支払いステータスレポート用の [ データビジュアライゼーションビュー ](https://experienceleague.adobe.com/docs/commerce/payment-services/reporting/order-payment-status.html#order-payment-status-data-visualization-view) を追加しました。

![ 問題を修正 ](../assets/fix.svg)<!-- Issue PAY-4486--> 以前は、PayPal PayLater ボタンが英国のマーチャントのチェックアウトに表示されていませんでした。 その問題は解決しました。

![ 修正された問題 ](../assets/fix.svg)<!-- Issue PAY-4485-->[!DNL Payment Services] が無効な場合、レポートデータビジュアライゼーションビューが [!DNL Payment Services] ホームに表示されるようになりました。

_2023 年 1 月 25 日_

![ 既知の問題 ](../assets/bug.svg)<!-- Issue PAY-4102 --> [!DNL Payment Services] の新規インストールでは、Commerce サービスを設定できず、レンダリング [!DNL Payment Services] 操作できません。 この問題を修正するには、[!DNL Payment Services] 拡張機能をバージョン 1.5.3 に更新します。

_2022 年 9 月 12 日_

![ 新規 ](../assets/new.svg)<!-- Issue PAY-3705 --> `increment_id` は、外部 ERP システムでの支払い調整に使用できるようになりました。 [`custom_id` _および_ `invoice_id`](https://experienceleague.adobe.com/docs/commerce/payment-services/reporting/data.html#reconcile-with-erp-system) に伝播され、支払い用の PayPal Webhook およびマーチャントアクティビティ詳細の両方に表示されます。

_2022 年 8 月 31 日_

![ 修正された問題 ](../assets/fix.svg)<!-- Issue PAY-3629 --> 新しいマーチャントが初めて [!DNL Payment Services] ホームにアクセスする際に、ページを更新する必要がなく、ページが直ちに読み込まれてコンテンツが表示されるようになりました。

_2021 年 8 月 9 日_

![ 新規 ](../assets/new.svg)<!-- Issue PAY-3420 --> Apple Pay が PayPal スマートボタンとして使用できるようになりました。 この [ 支払いオプション ](https://experienceleague.adobe.com/docs/commerce/payment-services/payments-options.html#apple-pay-button) により、お客様はiOSまたはmacOS デバイスで Touch ID 機能を使用して、Apple Pay を選択できます。 Apple Pay は、デバイスに保存されているクレジットカードとデビットカードの支払資格情報を使用して支払いを処理します。

_2021 年 6 月 28 日_

![ 新規 ](../assets/new.svg)<!-- Issue PAY-1720 --> 店舗注文の争議が [ 注文支払ステータス レポート ](https://experienceleague.adobe.com/docs/commerce/payment-services/reporting/order-payment-status.html#view-disputes) で利用できるようになりました。 [!DNL Payment Services] から PayPal 解決センターに直接移動することで、紛争に対処できます。

![ 新規 ](../assets/new.svg)<!-- Issue PAY-2854 -->[!DNL Payment Services] ホームのユーザーエクスペリエンスの向上には、現在の継承レベルでの設定を変更する機能や、ヘッダーとナビゲーションの表示を改善する機能が含まれます。

![ 新規 ](../assets/new.svg)<!-- Issue PAY-2854 --> サンドボックスモードから実稼動モードに切り替えた場合や、保存されていない更新でビューから移動しようとした場合に、警告が表示されるようになりました。

![ 新規 ](../assets/new.svg)<!-- Issue PAY-2761 --> 列設定コントロールを使用して、[ 注文支払いステータスレポート ](https://experienceleague.adobe.com/docs/commerce/payment-services/reporting/order-payment-status.html#show-and-hide-columns) および [ 支払いレポート ](https://experienceleague.adobe.com/docs/commerce/payment-services/reporting/payouts.html#show-and-hide-columns) に表示されるデータをカスタマイズできるようになりました。

+++

## v2.11.0

_2025 年 3 月 13 日_

[!BADGE  サポート対象 ]{type=Informative tooltip="サポート"}


![ 新機能 ](../assets/new.svg)<!-- PAY-5938 --> 現在は、マーチャント [!DNL Payment Services] 支払い設定を管理して、ビジネスの柔軟性を最大限に高めることができます。 このバージョンにより、マーチャントがサポートする地域とブランドに [ 複数の PayPal アカウント ](https://experienceleague.adobe.com/en/docs/commerce/payment-services/configure/settings#use-multiple-paypal-accounts) を添付する機能が向上します。 アドビのセールスチームは、web サイトとストアの表示範囲を設定するためのオンボーディングリンクを提供できます。

![ 新規 ](../assets/new.svg)<!-- PAY-5968 --> 現在は、[!DNL Payment Services] が **PayPal マーチャント ID** および **PayPal マーチャントステータス** 値で管理者設定を更新しています。 これらの値により、マーチャントは PayPal アカウントのステータスをより明確に把握できます。

![ 修正された問題 ](../assets/fix.svg)<!-- PAY-5816 --> バージョン v2.9.0 のすべての注文配置でエラーが発生していた問題を解決することで、[!DNL Payment Services] の通常の注文機能が復元されました。

![ 問題を修正 ](../assets/fix.svg)<!-- PAY-5825 -->Apple Pay ミニカートが、ログインしているお客様に対して誤った推定合計 URL を使用していた問題を修正しました。 現在は、正確 [!DNL Payment Services] 合計計算が保証されています。

![ 修正された問題 ](../assets/fix.svg)<!-- PAY-5826 --> 見積もりステータスを `inactive` に変更する際に HTTP 500 エラーが発生していた問題を解決し、注文管理の信頼性を向上しました。

![ 修正された問題 ](../assets/fix.svg)<!-- PAY-5849 --> 1 未満の 10 進数の数量に対して `LineItemProvider` が例外をスローした問題を修正しました。 現在、[!DNL Payment Services] は分数のサポートを強化しています。

![ 問題を修正 ](../assets/fix.svg)<!-- PAY-5868 --> チェックアウト中のギフトカードの金額エラーを修正しました。 チェックアウトプロセス中に [!DNL Payment Services] が正確な値を保証するようになりました。

![ 問題を修正 ](../assets/fix.svg)<!-- PAY-5911 --> 非 [!DNL Payment Services] ールのオンライン支払い方法を使用して注文を行った場合に、出荷作成時に発生するエラーを解決し、全体的な信頼性を向上しました。

![ 修正された問題 ](../assets/fix.svg)<!-- PAY-5954 --> [!DNL Payment Services] では、ウォレットで別のクレジットカードが選択されている場合にApple Pay が注文に失敗する問題を解決することで、よりスムーズなチェックアウトエクスペリエンスを提供するようになりました。

![ 修正された問題 ](../assets/fix.svg)<!-- PAY-5971 --> Apple Pay が失敗した場合に [!DNL Payment Services] が注文レビューページにリダイレクトされなくなり、不要なチェックアウトの中断を防ぎました。

## v2.10.3

_2025 年 2 月 24 日_

[!BADGE  サポート対象 ]{type=Informative tooltip="サポート"}

![ 修正された問題 ](../assets/fix.svg)<!-- PAY-xxxx --> 全体的な安定性とパフォーマンスが向上しました。

![ 修正された問題 ](../assets/fix.svg)<!-- PAY-xxxx --> 全般的な改善と最適化。 v2.10.2 の重大なバグを修正しました。

## v2.10.2

_2025 年 2 月 21 日_

[!BADGE  サポート対象 ]{type=Informative tooltip="サポート"}

![ 既知の問題 ](../assets/bug.svg)<!-- PAY-xxxx --> 安定性とパフォーマンスに影響を与える可能性のある重大なバグが含まれています。 Adobeでは、このバージョン（v2.10.2）を使用する代わりに v2.10.3 にアップグレードすることをお勧めします。

## v2.10.1

_2025 年 2 月 5 日_

[!BADGE  サポート対象 ]{type=Informative tooltip="サポート"}

![ 新規 ](../assets/new.svg)<!-- PAY-5813 --> Adobe Commerce 2.4.8 および PHP 8.4 がサポートされるようになりました。

## v2.10.0

_2024 年 12 月 13 日_

[!BADGE  サポート対象 ]{type=Informative tooltip="サポート"}

![ 新規 ](../assets/new.svg)<!-- PAY-5873 --> [!DNL Payment Services] は、Adobe Commerceの [Edge Delivery Services ストアフロント ](https://experienceleague.adobe.com/developer/commerce/storefront/dropins/payment-services/) で [[!DNL Payment Services]  ドロップインコンポーネント ](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/) をサポートするようになりました。

![ 新規 ](../assets/new.svg)<!-- PAY-5702 --> [!DNL Payment Services] は、購入せずに保管するための [GraphQL エンドポイント ](https://developer.adobe.com/commerce/webapi/graphql/payment-services-extension/queries/get-vault-config/) をサポートするようになりました。これにより、お客様は、トランザクションを完了することなく支払い方法を保存できます。

![ 新規 ](../assets/fix.svg)<!-- PAY-5789 --> [!DNL Payment Services] は、Google Pay](https://experienceleague.adobe.com/en/docs/commerce/payment-services/security-compliance/security#3ds) での [3D セキュア認証をサポートするようになり、支払い取引中のマーチャントおよびお客様のセキュリティを強化します。

![ 修正 ](../assets/fix.svg)<!-- PAY-5703 --> [!DNL Payment Services] では、[ 顧客が自分の **マイアカウント**](https://experienceleague.adobe.com/en/docs/commerce/payment-services/payments-checkout/vaulting) にカードを直接保存する機能が追加され、利便性が向上し、今後のチェックアウトが簡素化されます。`Vault without purchase functionality might not be 100% compatible with Adobe Commerce 2.4.4 due to a known issue with` [`GraphQL authorization mechanisms`](https://developer.adobe.com/commerce/webapi/graphql/usage/authorization-tokens/)。

![ 修正 ](../assets/fix.svg)<!-- PAY-5762 --> 注文が製品詳細ページ（PDP）から開始された際に、注文レビューページでクーポンコードが適用されない問題を修正しました。

![ 修正 ](../assets/fix.svg)<!-- PAY-5792 --> [!DNL Payment Services] では、[ チェックアウトページのヴォールトカード ](https://experienceleague.adobe.com/en/docs/commerce/payment-services/payments-checkout/vaulting) の説明と請求先住所が表示されるようになり、顧客は保存済みの支払い方法をより明確に把握できるようになりました。

![ 修正 ](../assets/fix.svg)<!-- PAY-5793 --> [!DNL Payment Services] を使用すると、マーチャントはチェックアウトページから直接保管されたカードの請求先住所を保存できるので、正確で完全な支払い情報を確保できます。

## v2.9.0

_2024 年 11 月 7 日_

[!BADGE  サポート対象 ]{type=Informative tooltip="サポート"}

![ 新規 ](../assets/new.svg)<!-- PAY-5629 --> [!DNL Payment Services] は、Apple Pay 用に **アップグレードされたSDK URL** をサポートするようになり、Apple Pay を使用するマーチャントの統合を強化しました。 この機能はmacOS 14 以降と互換性があり、以前のバージョンのmacOSが動作するデバイスには表示されません。

![ 新規 ](../assets/new.svg)<!-- PAY-5630 --> **チェックアウト**、**商品**、**買い物かご** および **ミニ買い物かご** ページを更新して、**Apple Pay 用にアップグレードされたSDK URL** をサポートし、支払いオプションとしてApple Pay を提供するマーチャントのユーザーエクスペリエンスを強化しました。

![ 新規 ](../assets/new.svg)<!-- PAY-5635 --> 配送見積もりを改善 **Apple Pay アドレスに基づく** し、お客様はチェックアウト時に正確な配送料を確認できるようになりました。

![ 修正 ](../assets/fix.svg)<!-- PAY-5661 --> チェックアウト時の様々な **[!DNL Payment Services]の問題** を修正し、マーチャントと買い物客の支払いプロセスの信頼性を向上させました。

![ 修正 ](../assets/fix.svg)<!-- PAY-5692 --> **高速チェックアウト用のスマートボタン** を使用したときに **顧客の姓と名** が注文に追加されない問題を修正しました。

![ 修正 ](../assets/fix.svg)<!-- PAY-5712 --> 合計金額が無料の場合に、マーチャントが **小計ゼロのチェックアウト支払オプションを使用してチェックアウトを完了できない** 問題を解決しました。

## v2.8.1

_2024 年 9 月 13 日_

[!BADGE  サポート対象 ]{type=Informative tooltip="サポート"}

![ 修正 ](../assets/fix.svg)<!-- PAY-5644 --> [!DNL Payment Services] で複数のスコープを使用する場合の、SDK パラメーターのキャッシュの問題を修正しました。 SDK設定は、単一のキーの下ではなく、スコープごとに個別にキャッシュされるようになりました。 これにより、各範囲のキャッシュが個別に無効化されるため、複数の範囲を管理する際の信頼性が向上します。

## v2.8.0

_2024 年 9 月 13 日_

[!BADGE  サポート対象 ]{type=Informative tooltip="サポート"}

![ 新規 ](../assets/new.svg)<!-- PAY-5499 --> [!DNL Payment Services] は、Adobe Commerceで [ トラッキング番号が入力された ](track-shipment.md) 場合の PayPal へのトラッキング番号情報の送信をサポートするようになりました。

![ 修正 ](../assets/fix.svg)<!-- PAY-5626 --> [!DNL Payment Services] は、お客様がCommerceのチェックアウトページにアクセスした際の、マーチャントレジストリに対するリクエストプロセスを最適化しました。 以前は、支払い方法（ホストされているフィールド、Google Pay、Apple Pay、スマートボタン）ごとに別々のリクエストが行われていました。 この改善により、呼び出し数が減り、チェックアウトプロセス中のパフォーマンスと効率が向上します。

![ 修正 ](../assets/fix.svg)<!-- PAY-5645 --> 買い物客 [!DNL Payment Services]、チェックアウトページでマーチャントがカスタム利用条件の作成に同意しない場合、PayPal/Google Pay のポップアップが開かなくなりました。

![ 修正 ](../assets/fix.svg)<!-- PAY-5648 -->  [!DNL Payment Services] は、PayPal ポータルの明細行項目の税分類に関する問題を解決しました。 注文の送料に税金が関連付けられている場合、その税金は送料の一部として含まれ、PayPal ポータルに表示される明細項目の詳細にこの方法で表示されます。

## v2.7.0

_2024 年 8 月 2 日_

[!BADGE  サポート対象 ]{type=Informative tooltip="サポート"}

![ 新規 ](../assets/new.svg)<!-- PAY-4844 --> [!DNL Payment Services] では、[ 注文レベルでの行項目データ ](https://experienceleague.adobe.com/en/docs/commerce/payment-services/payments-checkout/manage/line-items) をサポートするようになりました。 この機能を使用すると、マーチャントは、商品の詳細、数量、価格（消費税、割引、その他の関連情報を含む）など、注文の品目に関する詳細情報を表示できます。

![ 新規 ](../assets/new.svg)<!-- PAY-5380 --> [!DNL Payment Services] では、マーチャント向けの [ 管理での設定 ](https://experienceleague.adobe.com/en/docs/commerce/payment-services/configure/configure-admin#general-configuration) エクスペリエンスが改善され、より簡単で直感的なオンボーディングプロセスが実現しました。 この機能を使用すると、マーチャントは [!DNL Payment Services] ID をリセットできます。

![ 新規 ](../assets/new.svg)<!-- PAY-5255 --> [!DNL Payment Services] には [ 支払い失敗通知 ](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/point-of-purchase/checkout/checkout-payment-failed-emails) が含まれます。 この機能により、マーチャントへの支払い失敗をほぼリアルタイムで通知できるので、買い物客に連絡することで注文を保存でき、場合によっては問題の解決を向上させることができます。

![ 修正 ](../assets/fix.svg)<!-- PAY-5469 --> **Google Pay のポップアップが Safari** によってブロックされる問題を修正しました。 買い物客は、Safari でGoogle Pay の支払い取引を行うことができるようになりました。

![ 修正 ](../assets/fix.svg)<!-- PAY-5492 --> マーチャントがカスタマイズされた利用条件をチェックアウトページに追加した際の問題を修正しました。 [ エクスプレスチェックアウト ](https://experienceleague.adobe.com/en/docs/commerce/payment-services/payments-checkout/payments-options#standard-vs-advanced-payments-experience) 中、買い物客はこれらの利用条件に同意して、問題なくチェックアウトを完了できるようになりました。

![ 修正 ](../assets/fix.svg)<!-- PAY-5532 --> **InstantPurchase** により、店舗内ピックアップ（ISPU）機能が改善されました。 **InstantPurchase** で買い物客が注文を行った際、**ISPU 配信方法** が表示されなくなりました。

![ 修正 ](../assets/fix.svg)<!-- PAY-5606 --> マーチャントの国が **ドイツ** に設定されている場合に発生した **設定ページ** 国セレクター内の問題を修正しました。

## v2.6.0

_2024 年 6 月 4 日_

[!BADGE  サポート対象 ]{type=Informative tooltip="サポート"}

![ 新規 ](../assets/new.svg)<!-- PAY-4877 --> 現在、[!DNL Payment Services] は [L2/L3 の価格設定機能をサポートしています ](https://experienceleague.adobe.com/docs/commerce/payment-services/reporting/levels-card-payment-transactions.html)。 この機能は、IC++の価格が有効になっている [!DNL Payment Services] のお客様のみが利用できます。 [!DNL Payment Services] に L2/L3 処理データを使用する場合は、[!DNL Payment Services] のアカウントマネージャーにお問い合わせください。

![ 修正 ](../assets/fix.svg)<!-- PAY-5455 -->[!DNL Payment Services] を使用すると、[ ドメイン関連付けファイル ](https://developer.paypal.com/docs/checkout/apm/apple-pay/#register-your-live-domain) をダウンロードしてホストすることなく、拡張機能から直接Apple Pay を有効にできます。

## v2.5.0

_2024 年 4 月 23 日_

[!BADGE  サポート対象 ]{type=Informative tooltip="サポート"}

![ 修正 ](../assets/fix.svg)<!-- Issue PAY-5396 -->[!DNL Payment Services]Adobe Commerce バージョン 2.4.7 以降で、[`--db-prefix` パラメーターのAdobe Commerce ガイドライン ](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/advanced#install-from-the-command-line) がサポートされるようになりました。

## v2.4.3

_2024 年 4 月 16 日_

[!BADGE  サポート対象 ]{type=Informative tooltip="サポート"}

![ 修正 ](../assets/fix.svg)<!-- Issue PAY-5106 -->PayPal とAdobe Commerceの間のチェックアウト時に、注文金額の合計が正しく入力されない問題を修正しました。 マーチャントは、注文を行う際に注文金額の合計が正しいことを確認できるようになりました。

## v2.4.2

_2024 年 4 月 11 日_

[!BADGE  サポート対象 ]{type=Informative tooltip="サポート"}

![ 新規 ](../assets/new.svg)<!-- Issue xxx -->Adobe Commerce 2.4.7 がサポートされるようになりました。

## v2.4.1

_2024 年 4 月 4 日_

[!BADGE  サポート対象 ]{type=Informative tooltip="サポート"}

![ 修正 ](../assets/fix.svg)<!-- PAY-5322 --> 新しいAdobe Commerce リリースとの PCI 互換性の問題を修正しました。 現在は、支払 [!DNL Payment Services] オプションとしてAdobe Commerceのチェックアウト要件に適応しています。

![Fix](../assets/fix.svg)<!-- PAY-5323 -->PayLater および Venmo がAdobe Commerceで正しく表示されます。 管理者に PayLater と Venmo の切り替えオプションを表示できなかったエラーを修正しました。

## v2.4.0

_2024 年 3 月 20 日_

[!BADGE  サポート対象 ]{type=Informative tooltip="サポート"}

![ 新機能 ](../assets/new.svg)<!-- PAY-4868 --> マーチャントは、管理者を通じて [!DNL Payment Services] の他の支払いボタンと同様に、[ 購入エクスペリエンス全体を通してGoogle Pay を設定 ](https://experienceleague.adobe.com/docs/commerce/payment-services/payments-checkout/payments-options.html) できます。

![ 新規 ](../assets/new.svg)<!-- PAY-4381 --> [ 支払いサービスは、GraphQLを通じてGoogle Pay をサポートしており ](https://developer.adobe.com/commerce/webapi/graphql/payment-services/) マーチャントはGoogle Pay 支払い方法でヘッドレスなCommerce エクスペリエンスを得ることができます。

![ 新機能 ](../assets/new.svg)<!-- PAY-4878 -->Adobe CommerceおよびMagento Open Sourceのマーチャントには、[!DNL Payment Services] の基本的なチェックアウト機能がバンドルされるようになりました。[!DNL Payment Services] は、世界中の 200 か所の地域で、ビジネスを行うマーチャントをサポートできるようになりました。基本的 [!DNL Payment Services] チェックアウトでは、デビット/クレジット、PayPal、Venmo （利用可能な場合）、PayLater （利用可能な場合）のオプションがセルフサービスのオンボーディングで提供されます。

![ 修正 ](../assets/fix.svg)<!-- PAY-5291 --> 一部の取引について、支払い確認の受信が遅延する場合があります。 その場合、マーチャントは注文の更新された支払いステータスを取得できるようになりました。 [Payment Services は、保留中の取引を検出し ](https://experienceleague.adobe.com/docs/commerce/payment-services/reporting/order-payment-status.html) これらの取引をプロアクティブに監視し、保留中のステータスが取得されたときに更新することで、支払い取引の保留中のステータスを順番に検出します。

## v2.3.4

_2024 年 3 月 1 日_

[!BADGE  サポート対象 ]{type=Informative tooltip="サポート"}

![ 新規 ](../assets/new.svg)<!-- PAY-5244 --> 非同期チェックアウトの互換性を修正しました。

![ 修正 ](../assets/fix.svg)<!-- PAY-5253 --> [!DNL Payment Services] に属していない Vault トークンを削除できないエラーを修正しました。

## v2.3.3

_2024 年 2 月 14 日_

[!BADGE  サポート対象 ]{type=Informative tooltip="サポート"}

![ 新規 ](../assets/new.svg)<!-- PAY-5048 -->PHP 8.3 のサポートを追加

![ 修正 ](../assets/fix.svg)<!-- PAY-5048 --> `is_deleted` フラグのエラーを修正しました。 現在は、拡張機能から送信された `Rejected` ステータスが原因で注文が失敗することはありません。

## v2.3.2

_2024 年 1 月 26 日_

[!BADGE  サポート対象 ]{type=Informative tooltip="サポート"}

![ 修正 ](../assets/fix.svg)<!-- PAY-5183 -->REST/GraphQLのパフォーマンスの問題を修正しました。 現在は、API を介して取得された際に、クレジットカードのボタンがレンダリングされるようになりました。

## v2.3.1

_2023 年 12 月 7 日_

[!BADGE  サポート対象 ]{type=Informative tooltip="サポート"}

![ 新規 ](../assets/new.svg)<!-- PAY-5047 --> クレジット/デビットカードのブランドまたは支払方法タイプを、次の場所から使用できるようになりました。

- ストアフロントの顧客注文ページ
- 買い物客に送信された注文確認メール
- Commerce Admin の [ 注文の詳細ビュー ](https://experienceleague.adobe.com/docs/commerce-admin/stores-sales/order-management/orders/order-processing.html#view-an-order) から。

## v2.3.0

_2023 年 12 月 1 日（PT）_

[!BADGE  サポート対象 ]{type=Informative tooltip="サポート"}

![ 新規 ](../assets/new.svg)<!-- PAY-4381 --> [ 支払いサービスでGraphQL統合がサポートされるようになりました ](https://developer.adobe.com/commerce/webapi/graphql/payment-services/)。 GraphQLの PayPal 支払いボタン、ホストフィールド、Apple Pay のサポートにより [!DNL Payment Services] ヘッドレス Commerceの設定がサポートされるようになりました。

## v2.2.1

_2023 年 9 月 27 日_

[!BADGE  サポート対象 ]{type=Informative tooltip="サポート"}

![ 修正された問題 ](../assets/fix.svg)<!-- Issue PAY-4870 --> 最新リリースで拡張機能バージョンを送信する際に、ストアフロントで新しいヘッダー属性が正しく入力されない問題を修正しました。 以前のリリースでは、Commerce Services コネクタの `1.3.0` では、[!DNL Payment Services] 拡張機能から `User-Agent header` を拡張できませんでした。

## v2.2.0

_2023 年 8 月 30 日_

[!BADGE  サポート対象 ]{type=Informative tooltip="サポート"}

![ 新規 ](../assets/new.svg)<!-- PAY-4638 --> 自動の不正保護サービスを提供する [Signifyd との統合 ](https://experienceleague.adobe.com/docs/commerce/payment-services/security-compliance/fraud-protection.html) を追加しました。

![ 新規 ](../assets/new.svg)<!-- PAY-3981 --> [Apple Pay を別の支払いオプションに昇格 ](https://experienceleague.adobe.com/docs/commerce/payment-services/payments-checkout/payments-options.html?lang=en#apple-pay-button) し、PayPal 支払いボタンの外側で、買い物客の支払いオプションの可視性を高め、マーチャントがApple Pay の配置とスタイル設定を制御できるようにします。

![ 新規 ](../assets/new.svg)<!-- PAY-4002 --> 支払いアイコンの追加などのスタイル設定の強化を含む、クレジットカードフィールドのチェックアウトのユーザーエクスペリエンスを改善して、買い物客の認知負荷を減らし、コンバージョンを増やしました。

![ 新規 ](../assets/new.svg)<!-- PAY-4002 --> マーチャントが特定の支払いオプションに優先順位を付ける [ 支払いオプションの順序を並べ替える ](https://experienceleague.adobe.com/docs/commerce/payment-services/configure/settings.html#payment-buttons) ことができる機能を追加しました。 この機能により、チェックアウトの会話率を高くすることをお勧めします。

![ 新規 ](../assets/new.svg)<!-- PAY-4035 --> マーチャントは、[!DNL Payment Services]Admin ホームページから使用できる新しい [ トランザクションレポート ](https://experienceleague.adobe.com/docs/commerce/payment-services/reporting/transactions.html) を使用して、ストアの正常性を効率的に監視し、トランザクションの問題を特定できるようになりました。 このレポートには、トランザクションの承認レートと負のトランザクションのトレンドに関するデータも表示されます。

## v2.1.0

_2023 年 6 月 9 日_

[!BADGE  サポート対象 ]{type=Informative tooltip="サポート"}

![ 新規 ](../assets/new.svg)<!-- Issue xxx -->Adobe Commerce 2.4.7-beta1 がサポートされるようになりました。

![ 新規 ](../assets/new.svg)<!-- Issue xxx -->[ オーストラリア、フランス、英国の国および関連通貨での提供 ](https://experienceleague.adobe.com/docs/commerce/payment-services/overview.html#availability) を追加しました。

![ 新規 ](../assets/new.svg)<!-- Issue PAY-4296 --> 管理者ロール用に拡張されたリソース [ が追加されました ](https://experienceleague.adobe.com/docs/commerce/payment-services/configure/settings.html#configure-roles) 管理者ユーザーが顧客の注文を作成および管理でき、セールスメニューで表示できる [!DNL Payment Services] ようにします。

![ 新規 ](../assets/new.svg)<!-- Issue PAY-4236 -->[ チェックアウト中にエラーが発生する注文の自動無効化 ](https://experienceleague.adobe.com/docs/commerce/payment-services/payments-checkout/checkout.html#order-auto-voided-if-error) を追加しました。

![ 新規 ](../assets/new.svg)<!-- Issue PAY-4183 --> チェックアウトページに [ クレジット/デビットカード支払いオプションボタンを表示 ](https://experienceleague.adobe.com/docs/commerce/payment-services/payments-checkout/payments-options.html#debit-or-credit-card-button) する機能が作成されました。

## v2.0.0

_2023 年 3 月 10 日_

[!BADGE  サポート対象 ]{type=Informative tooltip="サポート"}

![ 新規 ](../assets/new.svg)<!-- Issue PAY-4152 -->PHP 8.2 およびAdobe Commerce 2.4.6 がサポートされるようになりました。PHP 7.x との互換性はありません。

## v1.6.1

_2023 年 3 月 10 日_

[!BADGE  サポート対象 ]{type=Informative tooltip="サポート"}

![ 修正 ](../assets/fix.svg)<!-- Issue PAY-4226 --> 新しい [!DNL Payment Services] マーチャントが管理でチェックアウトを使用できない問題を修正しました。以前 [!DNL Payment Services]、Commerceの顧客 ID を使用していましたが、これは新規のお客様には存在しません。

![ 修正 ](../assets/fix.svg)<!-- Issue PAY-4205 --> [PayPal オプション ](https://experienceleague.adobe.com/docs/commerce/payment-services/payments-checkout/payments-options.html#paypal-smart-buttons) を使用してチェックアウト時に、指定された配送先住所の州がデフォルトの税金設定の州に置き換えられる問題を修正しました。 これで、顧客は注文をマーチャントの税金設定でデフォルトとして設定された以外の州に出荷できます。

![ 修正 ](../assets/fix.svg)<!-- Issue PAY-4202 --> 顧客がカードボルトを使用して購入を完了したり、（`Authorize and Capture` の支払いアクションを使用して [ 店舗のボルトを使用した支払い方法を削除したりできない問題を修正しました ](https://experienceleague.adobe.com/docs/commerce/payment-services/get-started/production.html#set-payment-services-as-payment-method)。 以前は、お客様がボールトに登録されているクレジットカードを使用または変更しようとすると、「Provider Vault ID が見つかりません」というエラーが表示されていました。

## v1.6.0

_2023 年 2 月 17 日_

[!BADGE  サポート対象 ]{type=Informative tooltip="サポート"}

![ 新規 ](../assets/new.svg)<!-- Issue PAY-3540 --> 欧州連合（EU）および英国で取引を行う商社向けに [PCI 3DS コンプライアンス機能 ](security.md#3ds) が追加されました。 この追加のセキュリティレイヤーは、購入者にクレジットカード発行者との認証を求め、オンラインでの詐欺を防ぐのに役立ち、欧州連合（EU）のコンプライアンス規制の一部として必要です。

![ 新規 ](../assets/new.svg)<!-- Issue PAY-3609 --> 管理者でカードボルトを有効にする [ 機能を追加しまし ](vaulting.md#use-vaulting-in-the-admin)。 これにより、マーチャントは、ボールト内の支払い方法を使用して、管理者で顧客の注文を作成できます。

## v1.5.4

_2023 年 1 月 29 日_

[!BADGE  サポート対象 ]{type=Informative tooltip="サポート"}

![ 修正された問題 ](../assets/fix.svg)<!-- Issue PAY-4110 --> 購入者が商品ページ、ミニカートおよびカートの支払いボタンを使用して注文できない問題を修正しました。 バイヤーは正常に注文を完了できるようになりました。

## v1.5.3

_2023 年 1 月 25 日_

[!BADGE  サポート対象 ]{type=Informative tooltip="サポート"}

![ 修正された問題 ](../assets/fix.svg)<!-- Issue PAY-4102 --> 後方互換性のない既知の問題に対する修正をリリースしました。 このリリースでは、サービス ID 拡張機能のバージョンが最新の安定したバージョンにロックされているので、新しい [!DNL Payment Services] インストールでCommerce サービスを設定することが再び可能になります。

## v1.5.2

_2022 年 12 月 22 日_

[!BADGE  サポート対象 ]{type=Informative tooltip="サポート"}

![ 修正された問題 ](../assets/fix.svg)<!-- Issue PAY-3992 --> 支払い方法が却下された場合の [!DNL Payment Services] の請求を改善しました。

![ 修正された問題 ](../assets/fix.svg)<!-- Issue PAY-3999 -->[!DNL Payment Services] では、チェックアウトページの [Fire Checkout&#39;s](https://commercemarketplace.adobe.com/swissup-firecheckout.html){target=_blank} カスタムテンプレートを使用して、マーチャントに対して PayPal 支払いボタンが正しく表示されるようになりました。 以前は、ミニカートは断続的にボタンを表示していました。

## v1.5.1

_2022 年 11 月 23 日_

[!BADGE  サポート対象 ]{type=Informative tooltip="サポート"}

![ 新規 ](../assets/new.svg)<!-- Issue PAY-3923 -->[!DNL Payment Services] に、ユーザーエージェントヘッダーにバージョン番号が含まれるようになりました。これにより、リクエストで未使用のエンドポイントを追跡、フィルタリングまたは非推奨（廃止予定）にできるようになりました。

![ 修正された問題 ](../assets/fix.svg)<!-- Issue PAY-3968 -->[!DNL Payment Services] 支払いボタンを使用して製品ページから注文する際に、注文データが正しく表示されるようになりました。

## v1.5.0

_2022 年 11 月 18 日_

[!BADGE  サポート対象 ]{type=Informative tooltip="サポート"}

![ 新規 ](../assets/new.svg)<!-- Issue PAY-3880 --> 買い物客は、チェックアウト時にクレジットカード情報を [vault （保存） ](https://experienceleague.adobe.com/docs/commerce/payment-services/payments-checkout/vaulting.html) し、後で同じ販売者アカウント内の同じ店舗または別の店舗で使用できるようになりました。

![ 新機能 ](../assets/new.svg)<!-- Issue PAY-3950 --> マーチャントは、店舗に対して [ インスタント購入Commerce機能 ](https://experienceleague.adobe.com/docs/commerce-admin/stores-sales/point-of-purchase/checkout-instant-purchase.html) を有効にできるようになりました。これにより、買い物客は（[ ボールトに登録されたクレジットカード情報 ](https://experienceleague.adobe.com/docs/commerce/payment-services/payments-checkout/vaulting.html) を使用）でチェックアウトを迅速化できます。

## v1.4.1

_2022 年 10 月 14 日_

[!BADGE  サポート対象 ]{type=Informative tooltip="サポート"}

![ 修正 ](../assets/fix.svg)<!-- Issue PAY-3766 --> 顧客の支払い方法が拒否された場合、表示されるエラーメッセージはより説明的です。 支払い情報を再度入力し、もう一度試すか、別の支払い方法を試すか、または拒否されたトランザクションについて銀行に連絡することを顧客に勧めます。

## v1.4.0

_2022 年 9 月 30 日_

[!BADGE  サポート対象 ]{type=Informative tooltip="サポート"}

![ 新規 ](../assets/new.svg)<!-- Issue PAY-784 -->[!DNL Payment Services] に、マーチャントアカウントを設定して [ 複数の PayPal ビジネスアカウントを使用 ](https://experienceleague.adobe.com/docs/commerce/payment-services/configure/settings.html#use-multiple-paypal-accounts) する機能が含まれるようになりました。 これにより、マーチャントは、異なる通貨を使用して複数の国で店舗を運営したり、ビジネスの一部にAdobe Commerceを使用したりできます。

![ 新規 ](../assets/new.svg)<!-- Issue PAY-3231 --> マーチャントは、[ 顧客トランザクションの銀行取引明細書に表示される、ブランド、ストアまたは製品ラインを記述する [!UICONTROL Soft Descriptor]](https://experienceleague.adobe.com/docs/commerce/payment-services/configure/settings.html#add-soft-descriptor) ールを web サイトまたは個々のストアビューに追加できます。

![ 新規 ](../assets/new.svg)<!-- Issue PAY-3707 --> [ クレジットカードのフィールドと PayPal の支払いボタンを有効または無効にする ](https://experienceleague.adobe.com/docs/commerce/payment-services/configure/settings.html#configure-payment-options) チェックアウト [!DNL Payment Services] 設定。

![ 修正された問題 ](../assets/fix.svg)<!-- Issue PAY-3546 --> 顧客が **[!UICONTROL Edit cart]** をクリックすると、ページは買い物かごページにリダイレクトされ、空の買い物かごを表示する代わりに、更新された項目が表示されます。

## v1.3.1

_2022 年 9 月 6 日_

[!BADGE  サポート対象 ]{type=Informative tooltip="サポート"}

![ 問題を修正 ](../assets/fix.svg)<!-- Issue PAY-3663 --> 非世界通貨で承認された注文をマーチャントストアが取り込む際に、取り込みプロセスが完了し、エラーが表示されなくなりました。

## v1.3.0

_2022 年 8 月 9 日_

[!BADGE  サポート対象 ]{type=Informative tooltip="サポート"}

![ 新規 ](../assets/new.svg)<!-- Issue PAY-XX --> 一般提供リリース – [!DNL Payment Services] が [ バージョン 2.4.0 ～ 2.4.5 で  [!DNL Adobe Commerce]  および  [!DNL Magento Open Source]  サポート ](https://experienceleague.adobe.com/en/docs/commerce-operations/release/product-availability) になりました。

![ 修正された問題 ](../assets/fix.svg)<!-- Issue PAY-x -->Apple Pay は、モバイルおよびデスクトップ上の Safari ブラウザー v15.5 と互換性を持つようになりました。

## v1.2.0

_2022 年 6 月 29 日_

[!BADGE  サポート対象 ]{type=Informative tooltip="サポート"}

![ 既知の問題 ](../assets/bug.svg)<!-- Issue PAY-x -->Apple Pay は、モバイルおよびデスクトップ上の Safari ブラウザー v15.5 と互換性がありません。 Safari バージョン 15.5 をご利用の場合、Apple Pay でチェックアウトを完了できません。

![ 問題を修正 ](../assets/fix.svg)<!-- Issue PAY-3264 --> 以前、ログインユーザーが自分のアカウントのデフォルトの住所以外の請求/配送先住所を選択すると、チェックアウトに失敗していました。 これで、デフォルトの保存済み住所ではなく、選択した請求先/配送先住所が送信され、チェックアウトが正常に完了します。

![ 修正された問題 ](../assets/fix.svg)<!-- Issue PAY-3314 --> チェックアウト時に PayPal 支払いボタンを無効にした場合、エラーは表示されません。

![ 修正された問題 ](../assets/fix.svg)<!-- Issue PAY-3330 --> ゲストユーザーがダッシュを含む電話番号を入力した場合に、チェックアウト中に支払いが失敗しなくなりました。

![ 修正された問題 ](../assets/fix.svg)<!-- Issue PAY-3338 PAY-2502 -->Commerce サービスの資格情報が無効な場合、[!DNL Payment Services] 管理者の [!DNL Payment Services] ホームに資格情報エラーが表示されてアラートが表示されるようになりました。

![ 既知の問題 ](../assets/bug.svg)<!-- Issue PAY-0 --> [!DNL Payment Services] は `commerce-data-export` v101.20 以降と互換性がないので、[[!DNL Channel manager] extension](https://experienceleague.adobe.com/docs/commerce-channels/channel-manager/guide-overview.html) と互換性がありません。

## v1.1.0

_2022 年 3 月 31 日_

[!BADGE  サポート対象 ]{type=Informative tooltip="サポート"}

![ 新規 ](../assets/new.svg)<!-- Issue PAY-2127 --> 一般提供リリース – [!DNL Payment Services] が [ バージョン 2.4.0 ～ 2.4.4 で  [!DNL Adobe Commerce]  および  [!DNL Magento Open Source]  サポート ](https://experienceleague.adobe.com/en/docs/commerce-operations/release/product-availability) になりました。

![ 新規 ](../assets/new.svg)<!-- Issue PAY-2682 --> カナダのマーチャントが [!DNL Adobe Commerce] および [!DNL Magento Open Source] の [!DNL Payment Services] 拡張機能を使用できるようになりました。 マーチャントは、支払設定を [ フランス語 ](https://experienceleague.adobe.com/docs/commerce/payment-services/overview.html?lang=fr#carte-de-cr%C3%A9dit-et-devises-accept%C3%A9es) または [ 英語 ](https://experienceleague.adobe.com/docs/commerce/payment-services/overview.html#accepted-credit-cards-and-currencies) で表示できます。

![ 新規 ](../assets/new.svg)<!-- Issue PAY-2681 --> [!DNL Payment Services] は、クレジットカードと PayPal のトランザクションで [ カナダドル（CAD） ](overview.md#accepted-credit-cards-and-currencies) をサポートしています。

![ 新規 ](../assets/new.svg)<!-- Issue PAY-2680 --> マーチャントは、英語またはフランス語の言語で [ オンボーディング  [!DNL Payment Services]](onboard.md) 拡張機能を使用できます。

![ 新規 ](../assets/new.svg)<!-- Issue PAY-2678 --> マーチャントは、[ 注文支払いステータス ](order-payment-status.md) および [ 支払いレポート ](payouts.md) の両方の財務レポートを、カナダドル（CAD）で表示できるようになりました。

![ 修正された問題 ](../assets/fix.svg)<!-- Issue PAY-2710 -->[!DNL Payment Services] は、[PHP 8.1](https://www.php.net/releases/8.1/en.php) と互換性を持つようになりました。

![ 問題を修正しました ](../assets/fix.svg)<!-- Issue PAY-3017 --> サンドボックスモードのアラートが改善され、複数のストアに対して適切なアラートが表示されるようになりました。

![ 修正された問題 ](../assets/fix.svg)<!-- Issue PAY-2742 --> ストア表示レベルで、Venmo などの使用可能な支払い方法を有効または無効にできるようになりました。 以前は、web サイトごとにのみ支払い方法を設定できました。

![ 問題を修正 ](../assets/fix.svg)<!-- Issue PAY-2277 --> 個々の PayPal 支払いボタンを選択的に有効または無効にする [ ことができるようになりました ](settings.md#payment-buttons)。

![ 修正された問題 ](../assets/fix.svg)<!-- Issue PAY-2561 --> 以前に削除された製品が _レビュー注文_ ページの買い物かごに表示されません。

![ 既知の問題 ](../assets/bug.svg)<!-- Issue PAY-2842 --> サンドボックス環境で支払いを処理すると、クレジットカードトランザクションをテスト [PayPal で失敗する可能性があります ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/payments/payservices-cc-sandbox-failure.html) です。

## v1.0.0

_2021 年 11 月 29 日_

[!BADGE  サポート対象 ]{type=Informative tooltip="サポート"}

![ 新規 ](../assets/new.svg)<!-- Issue PAY-2127 --> 一般提供リリース – [[!DNL Payment Services]](https://commercemarketplace.adobe.com/magento-payment-services.html) は、[!DNL Adobe Commerce] および [!DNL Magento Open Source] バージョン 2.4.0 ～ 2.4.3-p1 でサポートされるようになりました。

![ 新規 ](../assets/new.svg)<!-- Issue PAY-124 -->[!DNL Adobe Commerce] および [!DNL Magento Open Source] の [!DNL Payment Services] 拡張機能は、[[!DNL Adobe Commerce]  オンクラウドインフラストラクチャ ](install.md#adobe-commerce-on-cloud-infrastructure) または [ オンプレミス ](install.md#on-premises) インスタンス用にインストールできます。 これらのメソッドを使用するには、コマンドラインインターフェイスを使用する必要があります。

![ 新規 ](../assets/new.svg)<!-- Issue PAY-1986 --> [!DNL Payment Services] は、マーチャントがテストモードで拡張機能を評価できる [ サンドボックスアカウント ](sandbox.md) をサポートしています。

![ 新規 ](../assets/new.svg)<!-- Issue PAY-666 --> マーチャントは、サンドボックス環境または実稼動環境の切り替えを利用するなど、基本的な支払い動作で ](settings.md) 支払いサービス [`Authorize and Capture`](production.md#set-payment-services-as-payment-method) 拡張機能を [ 設定」できます。

![ 新規 ](../assets/new.svg)<!-- Issue PAY-780 --> 買い物客は、[!DNL Payment Services] を使用するか、[ 手動の注文作成 ](create-order.md) を介してチェックアウトできます。

![ 新規 ](../assets/new.svg)<!-- Issue PAY-1856 --> [ 注文支払いステータス ](order-payment-status.md) および [ 支払いレポート ](payouts.md) を介した包括的なレポートは、店舗の注文と関連する支払いを明確に把握する [!DNL Payment Services] めに利用できます。

![ 新規 ](../assets/new.svg)<!-- Issue PAY-311 --> [!DNL Payment Services] は、総処理量に基づいて、あらゆる販売会社に合わせた柔軟な階層価格をサポートしています。

![ 新規 ](../assets/new.svg)<!-- Issue PAY-1443 -->[!DNL Payment Services] 拡張機能の PayPal 支払いボタンとクレジットカードフィールドを、簡単に [ ルックアンドフィールをカスタマイズ ](payments-options.md) できます。

![ 既知の問題 ](../assets/bug.svg)<!-- Issue PAY-2473 --> 拡張機能のインストール中に [Composer キーが正しくない ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/payments/payservices-install.html) を使用すると、ユーザーは正しい `MAGEID` で [ 認証 ](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/prerequisites/authentication-keys) できません。

![ 既知の問題 ](../assets/bug.svg)<!-- Issue PAY-2474 --> [!DNL Payment Services] レポート [ すぐには同期されない場合があります ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/payments/payservices-report-info-delayed.html)。

![ 既知の問題 ](../assets/bug.svg)<!-- Issue PAY-2475 --> オンボーディング中に [PayPal サンドボックスアカウント ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/payments/payservices-paypal-acct.html) を作成すると、[!DNL Payment Services] のアカウントを検証できません。
