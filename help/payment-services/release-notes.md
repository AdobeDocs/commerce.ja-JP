---
title: '[!DNL Payment Services] リリースノート'
description: すべての [!DNL Payment Services]  リリースについて詳しくは、リリースノートを参照してください。
exl-id: 104aa2c7-7735-4ac2-8ed1-a03cd9911273
feature: Payments, Release Notes
source-git-commit: 14c4178338859d55a7391139033d51d1aa6f7678
workflow-type: tm+mt
source-wordcount: '4679'
ht-degree: 0%

---


# リリースノート

これらのリリースノートには、[!DNL Payment Services]のすべてのリリースが記載されており、次の内容が含まれています。

![新機能](../assets/new.svg)
![修正された問題](../assets/fix.svg)修正と改善
![既知の問題](../assets/bug.svg)既知の問題

通常の機能リリースバージョン以外でリリースされた機能の変更と修正については、_ホスト型サービスの更新_&#x200B;の節を参照してください。

今後のリリース、製品サポート、および[!DNL Payment Services]拡張機能をサポートするAdobe Commerce バージョンについて詳しくは、Adobe Commerce [&#x200B; リリーススケジュール &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-operations/release/planning/schedule)および[製品の可用性](https://experienceleague.adobe.com/en/docs/commerce-operations/release/product-availability)のトピックを参照してください。

## ホスト型サービスの更新

このリリースノートでは、ホストされたサービスの通常の機能リリース以外で発生した機能変更と修正について説明します。

+++ホスト型サービスの更新

_2026年1月21日_

![新しい問題](../assets/new.svg)<!-- Issue PAY-6374 -->現在、**ダッシュボードの**&#x200B;設定[!DNL Payment Services] ボタンは、支払い方法の管理者設定ページにリダイレクトされ、支払い設定を管理するためのより合理的なワークフローが提供されます。

_2026年1月19日_

![新しい問題](../assets/new.svg)<!-- Issue PAY-6325 -->これで、加盟店は[取引レポート &#x200B;](reporting.md#transactions-report-view)の列としてPayPal販売者IDを表示し、特定の顧客が配置した取引を識別できます。

_2025年4月25日_

![新しい問題](../assets/new.svg)<!-- Issue PAY-6051 -->現在、[!DNL Payment Services] ダッシュボードには、現在の拡張機能のバージョンとダッシュボードのバージョンの両方が表示されます。

_2024年8月30日_

![新しい問題](../assets/new.svg)<!-- Issue PAY-5658 -->販売者は、より詳細で正確な支払い方法データを取得するために、[&#x200B; トランザクションレポート &#x200B;](reporting.md#transactions-report-view)の支払い詳細でトランザクションをフィルタリングできるようになりました。

_2024年7月15日_

![新しい問題](../assets/new.svg)<!-- Issue PAY-5571 -->これで、販売者は[取引レポート &#x200B;](reporting.md#transactions-report-view)で、Commerceのお客様の電子メールで取引をフィルタリングできるようになりました。 顧客の電子メールを入力して、その電子メールのトランザクションをフィルタリングします。

_2024年7月9日_

![新しい問題](../assets/new.svg)<!-- Issue PAY-5488 -->これで、マーチャントはCommerceのお客様IDを[&#x200B; トランザクションレポート &#x200B;](reporting.md#transactions-report-view)の列として表示して、特定のお客様が設定したトランザクションを特定できます。 さらに、関連する注文について、このCommerceのお客様IDでトランザクションレポートをフィルタリングできます。

_2024年3月5日_

![修正された問題](../assets/fix.svg)<!-- Issue PAY-5252 -->これで、マーチャントは1つのセルのコンテンツを選択して、ダッシュボードグリッドからデータをコピーできます。

_2023年10月10日_

![新しい問題](../assets/fix.svg)<!-- Issue PAY-4888 -->これで、加盟店は、[取引報告書](reporting.md#transactions-report-view)のカード番号の最後の4桁で、クレジットカードとデビットカードの取引をフィルタリングできるようになりました。

_2023年7月12日_

![修正された問題](../assets/fix.svg)<!-- Issue PAY-4587 -->以前の拡張機能バージョンで行われた認証ボイドを防いだ[!DNL Payment Services] 2.1.0 リリースで導入された問題が解決されました。 任意のバージョンの[!DNL Payment Services]を使用している販売者は、承認を無効にできます。

_2023年6月9日_

![新規](../assets/new.svg)<!-- Issue PAY-4288 -->現在、販売者は[PayPal支払いボタンを&#x200B;_のみ_&#x200B;設定できます](payments-options.md#use-only-paypal-payment-buttons)。また&#x200B;_は_ PayPal クレジットカード支払いオプションを使用できません。 これにより、VenmoやPayPalの支払いボタンなど、さまざまな支払いオプションを提供することができます。また、PayPalのクレジットカード支払いオプションの代わりに、既存のクレジットカード会社を利用することもできます。

![新規](../assets/new.svg)<!-- Issue PAY-4050 -->注文支払い状況レポート用に、支払いサービスホームに表示される[&#x200B; データビジュアライゼーションビュー](payouts.md#payouts-data-visualization-view)を追加しました。

![修正済みの問題](../assets/fix.svg)<!-- Issue PAY-4486-->以前は、英国のマーチャントのチェックアウトにPayPal PayLater ボタンが表示されませんでした。 その問題は解決されました。

![修正済みの問題](../assets/fix.svg)<!-- Issue PAY-4485--> [!DNL Payment Services]が無効になっている場合、[!DNL Payment Services] ホームにレポート データ ビジュアライゼーション ビューが表示されるようになりました。

_2023年1月25日_

![既知の問題](../assets/bug.svg)<!-- Issue PAY-4102 -->新しい[!DNL Payment Services]のインストールでCommerce サービスを構成できず、[!DNL Payment Services]が操作不能になっています。 この問題を修正するには、[!DNL Payment Services]拡張機能をバージョン 1.5.3に更新してください。

_2022年9月12日_

![新規](../assets/new.svg)<!-- Issue PAY-3705 -->外部ERP システムでの支払いの調整に`increment_id`を使用できるようになりました。 `custom_id` _および_ `invoice_id`に反映され、支払いのPayPal Webhookと加盟店アクティビティの詳細の両方に表示されます。

_2022年8月31日_

![修正済みの問題](../assets/fix.svg)<!-- Issue PAY-3629 -->新しいマーチャントが[!DNL Payment Services] ホームに初めてアクセスした場合、ページが読み込まれるようになり、ページの更新を必要とせずにコンテンツを表示できるようになりました。

_2021年8月9日_

![New](../assets/new.svg)<!-- Issue PAY-3420 --> Apple PayがPayPal スマートボタンとして利用可能になりました。 この[支払いオプション &#x200B;](payments-options.md#apple-pay-button)を使用すると、お客様はiOSまたはmacOS デバイスのTouch ID機能を使用してApple Payを選択できます。 Apple Payでは、デバイスに保存されているクレジットカードとデビットカードの支払い資格情報を使用して支払いを処理します。

_2021年6月28日_

![新しい](../assets/new.svg)<!-- Issue PAY-1720 -->店舗での注文に関する紛争が、[注文支払い状況レポート &#x200B;](order-payment-status.md#view-disputes)で利用できるようになりました。 [!DNL Payment Services]からPayPal解決センターに直接移動して、紛争に対処できます。

![新規](../assets/new.svg)<!-- Issue PAY-2854 --> [!DNL Payment Services] ホームからのユーザーエクスペリエンスの改善には、現在の継承レベルで設定を変更する機能と、ヘッダーとナビゲーションの表示の改善が含まれます。

![新規](../assets/new.svg)<!-- Issue PAY-2854 --> サンドボックスモードから実稼動モードに切り替えた場合や、保存されていない更新を含むビューから移動しようとすると、警告が表示されるようになりました。

![新規](../assets/new.svg)<!-- Issue PAY-2761 -->列の設定コントロールを使用して、列を表示または非表示にすることで、[注文支払い状況レポート &#x200B;](order-payment-status.md#show-and-hide-columns)および[支払い状況レポート &#x200B;](payouts.md#show-and-hide-columns)に表示されるデータをカスタマイズできるようになりました。

+++

>[!NOTE]
>
> リリースは、必要に応じて新しい機能や修正を提供するために頻繁に発生します。 リリーススケジュールは固定されていません。

## v2.14.0

_2026年2月26日_

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.4以降

![新規](../assets/new.svg)<!-- PAY-6400 --> PayPalへの行項目と金額の内訳の送信を有効または無効にする&#x200B;**[!UICONTROL Line Items Enabled]**&#x200B;設定を追加しました。 この設定は、サードパーティの拡張機能が[!DNL Payment Services]でサポートされていないカスタム料金を追加する際のチェックアウトの問題を解決するのに役立ちます。 詳しくは、[行項目](line-items.md)を参照してください。

![新規](../assets/new.svg)<!-- PAY-6457 --> チェックアウトの開始時に[Express支払いボタンを追加しました](payments-options.md#express-checkout-buttons)。より迅速なチェックアウトを促進します。

![新規](../assets/new.svg)<!-- PAY-6458 -->地域固有およびローカルの支払いオプションに対する[&#x200B; ローカル支払い方法（LPM） &#x200B;](payments-options.md#local-payment-methods)のサポートを追加しました。 マーチャントは、[Commerce](configure-admin.md#local-payment-methods)内で利用可能なLPMを直接有効または無効にできます。

![新規](../assets/new.svg)<!-- PAY-6377 --> [購入者の国](sandbox.md#buyers-country) サンドボックス設定を追加して、購入者の場所をシミュレートし、どの支払い方法をレンダリングするかを制御しました。

![修正された問題](../assets/fix.svg)<!-- PAY-6458 -->購入者のメールアドレス データを渡すことで、PayPalの不正フィルターとの互換性を改善し、不正利用防止機能を強化しました。

![修正済みの問題](../assets/fix.svg)<!-- PAY-6413 -->配送先住所が見つからないため、バーチャル製品のPayPal チェックアウトを完了できない問題を修正しました。

![修正済みの問題](../assets/fix.svg)<!-- PAY-6450 -->商品詳細ページ、ミニカート、カート、チェックアウトの上部でPayPal ボタンのチェックアウトエラーが正しく処理されない問題を修正しました。

![修正済みの問題](../assets/fix.svg)<!-- PAY-6453 --> チェックアウト時の競合を防ぐために、GraphQL チェックアウトで無効になったサーバーサイドの送料コールバック フロー。

![修正済みの問題](../assets/fix.svg)<!-- PAY-6456 --> Appleが未検証ドメインからの支払いを拒否することを明確にするために、[Apple Pay](configure-admin.md#apple-pay)設定の説明を更新しました。 加盟店は、Appleの「支払い」ボタンが使用されているドメインを確認する必要があります。 国の制限が適用されます。

## v2.13.3

_2026年1月14日_

![修正済みの問題](../assets/fix.svg)<!-- PAY-6399 -->管理者のチェックアウト中に間違ったボールト カードが使用されていた問題を修正しました。 これで、選択したカードは注文するときに正しく使用されるようになりました。

## v2.13.2

_2026年1月5日_

![修正された問題](../assets/fix.svg)<!-- PAY-6390 -->改善されたJSの縮小を実装することで、一般的な改善と最適化が行われました。

## v2.13.1

_2025年12月18日_

![修正済みの問題](../assets/fix.svg)<!-- PAY-6355 --> チェックアウト時に販売者が配送方法を選択できない問題を修正しました。

![修正済みの問題](../assets/fix.svg)<!-- PAY-6347 -->不要なAPI呼び出しを削除して、チェックアウトの回復力を向上させました。

![修正済みの問題](../assets/fix.svg)<!-- PAY-6368 --> プライマリドメインが利用できない場合にPayments SDKを読み込むためのフォールバックメカニズムを実装し、チェックアウト中もクレジットカードのフィールドにアクセスできるようにしました。

## v2.13.0

_2025年11月10日_

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.4以降

![新規](../assets/new.svg)<!-- PAY-xxxx -->現在、[!DNL Payment Services]はPayPalの&#x200B;**One-Time Checkout （OTC）** モーダルをサポートしており、連絡先情報と配信情報が組み込まれています。

![新規](../assets/new.svg)<!-- PAY-xxxx --> **PayPal アプリ切り替え認証**&#x200B;を通じてモバイルエクスペリエンスを強化し、さらにスムーズなユーザージャーニーを実現するためのAPI統合を改善しました。 この機能は、米国[!DNL Payment Services] ベースのお客様のみが利用できます。

![新規](../assets/new.svg)<!-- PAY-xxxx -->では、**強力な顧客認証（SCA）**&#x200B;の要件を満たすために、Fastlaneの&#x200B;**3D セキュア （3DS）認証**&#x200B;のサポートが追加されました。 これにより、英国およびEU [!DNL Payment Services]の販売者は、**3DS認証**&#x200B;を使用してトランザクションを処理できるようになり、不正行為の防止が強化され、地域の規制への準拠が保証されます。

![新規](../assets/new.svg)<!-- PAY-xxxx -->現在、[!DNL Payment Services]人のマーチャントは、Fastlane チェックアウトコンポーネントの&#x200B;**明るいテーマと暗いテーマ**&#x200B;を選択でき、チェックアウトページをサイトデザインに合わせることができます。 カスタムスタイルがアクセシビリティ標準を満たさない場合、システムは自動的にデフォルト設定に戻ります。

![修正された問題](../assets/fix.svg)<!-- PAY-xxxx --> 3DS チャレンジ **を使用した**&#x200B;管理者チェックアウト中のローダーの問題を修正しました。

![修正済みの問題](../assets/fix.svg)<!-- PAY-xxxx --> APIを介して支払い設定&#x200B;**を保存する際の**&#x200B;検証を改善しました。

## v2.12.2

_2025年9月23日_

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.4以降

![修正済みの問題](../assets/fix.svg)<!-- PAY-6275 --> キャプチャモードで[!DNL Fastlane]件のトランザクションが拒否され、Commerceで注文が作成されなくなりました。

## v2.12.1

_2025年9月18日_

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.4以降

![修正された問題](../assets/fix.svg)<!-- PAY-6164 -->現在、[!DNL Payment Services]は[PayPal サーバーサイドの配送コールバック （SSSC） &#x200B;](https://developer.paypal.com/docs/multiparty/checkout/standard/customize/shipping-module/)で利用可能な配送方法に基本通貨を使用しています。

![修正された問題](../assets/fix.svg)<!-- PAY-6267 --> **実店舗での受け取り（ISPU）**&#x200B;が選択されている場合、**出荷先** ブロックはチェックアウトページに表示されません。

![修正された問題](../assets/fix.svg)<!-- PAY-6271 -->現在、[!DNL Payment Services]様は&#x200B;**顧客アカウント** > **保存済みの支払い方法** セクションにPayPal PayFlowから保存されたクレジットカードの詳細を表示しています。

## v2.12.0

_2025年8月20日_

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.4以降

![新規](../assets/new.svg)<!-- PAY-6022 --> [Fastlane](https://experienceleague.adobe.com/en/docs/commerce/payment-services/payments-checkout/payments-options)では、ゲストチェックアウト時に購入を高速化できます。

![新規](../assets/new.svg)<!-- PAY-6168 -->よりスムーズな移行とカートの再利用を可能にするために、[`addProductsToNewCart`](https://developer.adobe.com/commerce/webapi/graphql/payment-services-extension/mutations/)の変異を[!DNL Payment Services]に追加しました。

![新規](../assets/new.svg)<!-- PAY-6169 -->見積もりライフサイクル管理を改善するために、[`setCartAsInactive`](https://developer.adobe.com/commerce/webapi/graphql/payment-services-extension/mutations/)の変異を[!DNL Payment Services]に追加しました。

![新規](../assets/new.svg)<!-- PAY-6227 --> PayPalでチェックアウトする際、[!DNL Payment Services]は注文確認ポップアップをスキップして、より迅速な購入プロセスを実現します。 これは、[&#x200B; サーバーサイドの配送コールバック &#x200B;](payments-options.md#server-side-shipping-callbacks-for-paypal-payment-buttons)によって有効になり、PayPal レビューページ内で直接送料と合計を計算します。

![新規](../assets/new.svg)<!-- PAY-6234 --> [後で支払い](https://experienceleague.adobe.com/en/docs/commerce/payment-services/payments-checkout/payments-options)支払いオプションの新機能を追加しました。 現在、BNPL メッセージングコンフィギュレーターは、後払いBNPL メッセージを顧客チェックアウトページに表示する際により柔軟な機能を提供します。

![修正された問題](../assets/fix.svg)<!-- PAY-5505 -->現在、[!DNL Payment Services]は、Google PayまたはPayPalのポップアップが商品ページ内で閉じられたときに、見積もりを非アクティブとして設定します。

![修正された問題](../assets/fix.svg)<!-- PAY-5754 --> [!DNL Payment Services]では、空の引用符から注文を作成できなくなりました。

## v2.11.1

_2025年3月14日_

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.4以降

![修正済みの問題](../assets/fix.svg)<!-- PAY-5849 --> チェックアウト中に[行項目](line-items.md)に影響を与えた問題を修正しました。 現在、[!DNL Payment Services]は、**行項目**&#x200B;のチェックアウトプロセスの信頼性を向上させました。 同様の問題が発生した場合は、[!DNL Payment Services]の営業担当者にお問い合わせください。

## v2.11.0

_2025年3月13日_

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.4以降


![新規](../assets/new.svg)<!-- PAY-5938 -->現在、[!DNL Payment Services]では、販売者は支払い設定を管理して、ビジネスの柔軟性を最大限に高めることができます。 このバージョンでは、加盟店がサポートする地域とブランドに対して[複数のPayPal アカウント &#x200B;](configure-admin.md#use-multiple-paypal-accounts)を添付する機能が強化されます。 アドビの営業部門が、web サイトとストアビューの範囲を設定するためのオンボーディングリンクを提供します。

![新規](../assets/new.svg)<!-- PAY-5968 -->現在、[!DNL Payment Services]は&#x200B;**PayPal Merchant ID**&#x200B;および&#x200B;**PayPal Merchant Status**&#x200B;の値で管理者設定を更新します。 これらの値により、加盟店はPayPal アカウントのステータスをより詳細に把握できます。

![修正済みの問題](../assets/fix.svg)<!-- PAY-5816 --> バージョン v2.9.0のすべての注文プレースメントでエラーが発生していた問題を解決することで、[!DNL Payment Services]の通常の注文機能を復元しました。

![修正済みの問題](../assets/fix.svg)<!-- PAY-5825 --> Apple Pay ミニカートで、ログイン済みのお客様に誤った見積もり合計URLが使用される問題を修正しました。 これで、[!DNL Payment Services]は正確な合計計算を保証します。

![修正済みの問題](../assets/fix.svg)<!-- PAY-5826 -->見積もりステータスを`inactive`に変更する際にHTTP 500 エラーが発生した問題を解決することで、注文管理の信頼性を向上しました。

![修正済みの問題](../assets/fix.svg)<!-- PAY-5849 --> `LineItemProvider`が1未満の10進数の例外をスローした問題を修正しました。 現在、[!DNL Payment Services]は分数のサポートを強化しています。

![修正済みの問題](../assets/fix.svg)<!-- PAY-5868 --> チェックアウト時のギフトカードの金額エラーを修正しました。 [!DNL Payment Services]は、チェックアウトプロセス中に正確な値を保証するようになりました。

![問題を修正](../assets/fix.svg)<!-- PAY-5911 -->非[!DNL Payment Services] オンライン支払い方法を使用して行われた注文の出荷作成時のエラーを解決し、全体的な信頼性を向上しました。

![修正された問題](../assets/fix.svg)<!-- PAY-5954 --> [!DNL Payment Services]では、ウォレットで別のクレジットカードが選択されたときにApple Payで注文できなかった問題を解決することで、よりスムーズなチェックアウト体験を提供できるようになりました。

![修正された問題](../assets/fix.svg)<!-- PAY-5971 --> Apple Payが失敗した場合、[!DNL Payment Services]はお客様を注文レビューページにリダイレクトしなくなり、チェックアウトの不必要な中断を防ぐことができます。

## v2.10.3

_2025年2月24日_

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.4以降

![問題を修正](../assets/fix.svg)<!-- PAY-xxxx -->全体的な安定性とパフォーマンスが向上しました。

![問題を修正](../assets/fix.svg)<!-- PAY-xxxx -->一般的な改善と最適化。 v2.10.2のクリティカルなバグを修正しました。

## v2.10.2

_2025年2月21日_

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.4以降

![既知の問題](../assets/bug.svg)<!-- PAY-xxxx -->安定性とパフォーマンスに影響を与える可能性のある重大なバグが含まれています。 Adobeでは、このバージョン（v2.10.2）を使用するのではなく、v2.10.3にアップグレードすることをお勧めします。

## v2.10.1

_2025年2月5日_

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.4以降

![新規](../assets/new.svg)<!-- PAY-5813 --> Adobe Commerce 2.4.8およびPHP 8.4のサポートを追加しました。

## v2.10.0

_2024年12月13日_

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.4以降

![新規](../assets/new.svg)<!-- PAY-5702 --> [!DNL Payment Services]は、購入せずに保管するためのGraphQL エンドポイントをサポートするようになり、お客様は取引を完了することなく支払い方法を保存できるようになりました。

![新規](../assets/fix.svg)<!-- PAY-5789 --> [!DNL Payment Services]は、Google Pay[での](security.md#3ds)3D セキュア認証をサポートするようになり、支払い取引中の販売店とお客様のセキュリティを強化します。

![修正](../assets/fix.svg)<!-- PAY-5703 --> [!DNL Payment Services]では、[のお客様が&#x200B;**マイアカウント**](vaulting.md#vaulting-without-purchase)&#x200B;にカードを直接保存できるようになり、利便性が向上し、今後のチェックアウトが簡素化されます。`Vault without purchase functionality might not be 100% compatible with Adobe Commerce 2.4.4 due to a known issue with` [`GraphQL authorization mechanisms`](https://developer.adobe.com/commerce/webapi/graphql/usage/authorization-tokens/)。

![修正](../assets/fix.svg)<!-- PAY-5762 -->商品詳細ページ（PDP）から注文が開始されたときに、注文レビューページにクーポンコードが適用されない問題を修正しました。

![修正](../assets/fix.svg)<!-- PAY-5792 --> [!DNL Payment Services]様は、チェックアウトページ [に](vaulting.md) アクティブ化されたカードの説明と請求先住所を表示できるようになりました。これにより、顧客は保存された支払い方法をより詳細に把握できます。

![修正](../assets/fix.svg)<!-- PAY-5793 --> [!DNL Payment Services]を使用すると、チェックアウトページから直接、アークカードの請求先住所を保存して、正確で完全な支払い情報を確保できます。

## v2.9.0

_2024年11月7日_

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.4以降

![新規](../assets/new.svg)<!-- PAY-5629 --> [!DNL Payment Services]では、Apple Pay **用に** アップグレードされたSDK URLがサポートされるようになりました。Apple Payを使用するマーチャントの統合が改善されました。 この機能はmacOS 14以降と互換性があります。以前のバージョンのmacOSを実行しているデバイスには、この機能は表示されません。

![新規](../assets/new.svg)<!-- PAY-5630 --> **チェックアウト**、**商品**、**買い物かご**、**ミニカート**&#x200B;のページを更新して、**アップグレードされたApple PayのSDK URL**&#x200B;をサポートし、支払いオプションとしてApple Payを提供する販売者のユーザーエクスペリエンスを向上させました。

![新規](../assets/new.svg)<!-- PAY-5635 --> Appleの支払い先住所&#x200B;**に基づいて配送見積もり**&#x200B;を改善し、お客様が決済時に正確な送料を確認できるようにしました。

![修正](../assets/fix.svg)<!-- PAY-5661 --> チェックアウト **[!DNL Payment Services]時の様々な**&#x200B;の問題を修正し、加盟店と買い物客の支払いプロセスの信頼性を向上しました。

![修正](../assets/fix.svg)<!-- PAY-5692 -->Express チェックアウトに&#x200B;**スマートボタンを使用する際に**&#x200B;お客様の氏名&#x200B;**が注文に追加されない問題を修正しました**。

![修正](../assets/fix.svg)<!-- PAY-5712 -->合計金額が無料の場合、小計チェックアウトの支払いオプションを使用してチェックアウトを完了できない&#x200B;**問題を解決しました**。

## v2.8.1

_2024年9月13日_

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.4以降

![修正](../assets/fix.svg)<!-- PAY-5644 -->複数のスコープを[!DNL Payment Services]で使用する場合のSDK パラメーターのキャッシュに関する問題を修正しました。 SDK設定は、1つのキーの下ではなく、各スコープごとに個別にキャッシュされるようになりました。 これにより、各スコープのキャッシュが独立して無効化され、複数のスコープを管理する際の信頼性が向上します。

## v2.8.0

_2024年9月13日_

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.4以降

![新規](../assets/new.svg)<!-- PAY-5499 --> [!DNL Payment Services]は、Adobe Commerceで[&#x200B; トラッキング番号が入力されたときにPayPalにトラッキング番号を送信できるようになりました](track-shipment.md)。

![修正](../assets/fix.svg)<!-- PAY-5626 --> [!DNL Payment Services]は、お客様がCommerce チェックアウト ページにアクセスしたときに、加盟店レジストリへのリクエストプロセスを最適化しました。 以前は、各支払い方法（ホストフィールド、Google支払い、Apple支払い、スマートボタン）に対して個別のリクエストが行われていました。 これにより、通話数を削減し、チェックアウトプロセスにおけるパフォーマンスと効率性を向上できます。

![修正](../assets/fix.svg)<!-- PAY-5645 --> 買い物客がチェックアウトページでカスタム条件を作成することに同意していない場合、PayPal/Google支払いポップアップが開けなくなります。[!DNL Payment Services]

![修正](../assets/fix.svg)<!-- PAY-5648 -->  [!DNL Payment Services]は、PayPal ポータルでの税の行項目の分類に関する問題に対処しました。 注文の送料に税金が関連付けられている場合、その税金は送料の一部として含まれ、PayPal ポータルに表示される行項目の詳細にこのように表示されます。

## v2.7.0

_2024年8月2日_

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.4以降

![新規](../assets/new.svg)<!-- PAY-4844 --> [!DNL Payment Services]は、注文レベル [で](line-items.md)行項目データをサポートするようになりました。 この機能を使用すると、商品の詳細、数量、価格（消費税、割引、その他の関連情報を含む）など、注文のアイテムに関する詳細情報を確認できます。

![新規](../assets/new.svg)<!-- PAY-5380 --> [!DNL Payment Services]は、より簡単で直感的なオンボーディングプロセスを実現するために、マーチャント向けのAdmin[&#x200B; エクスペリエンスの](configure-admin.md#general-configuration)設定を改善します。 この機能を使用すると、販売者は[!DNL Payment Services] IDをリセットできます。

![新規](../assets/new.svg)<!-- PAY-5255 --> [!DNL Payment Services]には[支払い失敗の通知](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/point-of-purchase/checkout/checkout-payment-failed-emails)が含まれています。 この機能は、支払い失敗についてほぼリアルタイムでマーチャントに通知するので、買い物客に連絡して注文を保存し、問題解決を向上させる可能性があります。

![修正](../assets/fix.svg)<!-- PAY-5469 --> Safari **によって** Google支払いポップアップがブロックされる問題を修正しました。 買い物客は、SafariでGoogle Payの支払い取引を完了できるようになりました。

![修正](../assets/fix.svg)<!-- PAY-5492 -->販売者がカスタマイズされた条件をチェックアウトページに追加する際の問題を修正しました。 [&#x200B; エクスプレス チェックアウト &#x200B;](payments-options.md#standard-vs-advanced-payments-experience)中、買い物客は問題なくチェックアウトを完了するために、これらの利用条件に同意できるようになりました。

![修正](../assets/fix.svg)<!-- PAY-5532 --> **InstantPurchase**&#x200B;により、店舗内ピックアップ （ISPU）機能が改善されました。 買い物客が&#x200B;**InstantPurchase**&#x200B;で注文すると、**ISPU配達方法**&#x200B;が表示されなくなります。

![修正](../assets/fix.svg)<!-- PAY-5606 -->加盟店の国が&#x200B;**ドイツ**&#x200B;に設定されている場合に発生した&#x200B;**設定ページ**&#x200B;国セレクター内の問題を修正しました。

## v2.6.0

_2024年6月4日_

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.4以降

![新規](../assets/new.svg)<!-- PAY-4877 -->現在、[!DNL Payment Services]は[L2/L3の価格設定の機能](levels-card-payment-transactions.md#level-2-and-level-3)をサポートしています。 この機能は、IC++価格が有効になっている[!DNL Payment Services]のお客様のみが利用できます。 [!DNL Payment Services]のL2/L3処理データを使用する場合は、[!DNL Payment Services] アカウント マネージャーにお問い合わせください。

![修正](../assets/fix.svg)<!-- PAY-5455 -->[!DNL Payment Services]を使用すると、[&#x200B; ドメイン関連ファイル &#x200B;](https://developer.paypal.com/docs/checkout/apm/apple-pay/#register-your-live-domain)をダウンロードしてホストすることなく、拡張機能から直接Apple Payを有効にできます。

## v2.5.0

_2024年4月23日_

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.4以降

![修正](../assets/fix.svg)<!-- Issue PAY-5396 -->[!DNL Payment Services]では、Adobe Commerce バージョン 2.4.7以降の[&#x200B; パラメーター`--db-prefix`に対して](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/advanced#install-from-the-command-line)Adobe Commerce ガイドラインがサポートされるようになりました。

## v2.4.3

_2024年4月16日_

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.4以降

![修正](../assets/fix.svg)<!-- Issue PAY-5106 --> PayPalとAdobe Commerce間のチェックアウト時に注文金額の合計が誤って入力される問題を修正しました。 現在、注文を行う際に、加盟店は注文金額の合計が正しいことを確認できます。

## v2.4.2

_2024年4月11日_

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.4以降

![新規](../assets/new.svg)<!-- Issue xxx --> Adobe Commerce 2.4.7のサポートを追加しました。

## v2.4.1

_2024年4月4日_

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.4以降

![修正](../assets/fix.svg)<!-- PAY-5322 -->新しいAdobe Commerce リリースでのPCI互換性の問題を修正しました。 現在、[!DNL Payment Services]は支払いオプションとしてAdobe Commerceのチェックアウト要件に適応しています。

![Fix](../assets/fix.svg)<!-- PAY-5323 --> PayLaterとVenmoがAdobe Commerceに正しく表示されます。 管理者がPayLaterとVenmoの切り替えオプションを表示できないエラーを修正しました。

## v2.4.0

_2024年3月20日_

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.4以降

![新規](../assets/new.svg)<!-- PAY-4868 -->販売者は、Admin経由で[の他の支払いボタンと同様に、購入エクスペリエンス全体を通じて](payments-options.md)Google Payを正常に設定できます[!DNL Payment Services]。

![新規](../assets/new.svg)<!-- PAY-4381 --> [決済サービスでは、GraphQLを通じたGoogle Payをサポートしています](https://developer.adobe.com/commerce/webapi/graphql/payment-services/)販売者は、Google Payの決済方法でヘッドレスのCommerce体験を利用できます。

![新規](../assets/new.svg)<!-- PAY-4878 -->現在、[!DNL Payment Services]の基本的なチェックアウト機能は、Adobe CommerceとMagento Open Sourceのマーチャント向けにバンドルされています。[!DNL Payment Services]は、世界中の200の地域でビジネスを持つマーチャントをサポートできるようになりました。[!DNL Payment Services]の基本的なチェックアウトでは、セルフサービスのオンボーディングで、デビット/クレジット、PayPal、Venmo （利用可能な場合）、PayLater （利用可能な場合）のオプションが提供されます。

![修正](../assets/fix.svg)<!-- PAY-5291 -->一部のトランザクションの支払い確認の受信が遅れる可能性があります。 その場合、加盟店は注文の最新の支払い状況を取得できるようになります。 [決済サービスは、保留中のトランザクションを検出し、これらのトランザクションを積極的に監視し、保留中のステータスが取得されたときに更新することで、注文の支払いトランザクション &#x200B;](order-payment-status.md#payment-status-updates)の保留中ステータスを検出します。

## v2.3.4

_2024年3月1日_

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.4以降

![新規](../assets/new.svg)<!-- PAY-5244 -->非同期チェックアウトの互換性を修正しました。

![修正](../assets/fix.svg)<!-- PAY-5253 --> [!DNL Payment Services]に属していないボールトトークンを削除できないエラーを修正しました。

## v2.3.3

_2024年2月14日_

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.4以降

![新規](../assets/new.svg)<!-- PAY-5048 --> PHP 8.3のサポートを追加しました

![修正](../assets/fix.svg)<!-- PAY-5048 --> `is_deleted` フラグのエラーを修正しました。 拡張機能から`Rejected` ステータスが送信されたため、注文は失敗しません。

## v2.3.2

_2024年1月26日_

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.4以降

![修正](../assets/fix.svg)<!-- PAY-5183 -->REST/GraphQL パフォーマンスの問題を修正しました。 これで、APIを介して取得すると、クレジットカードのボタンがレンダリングされるようになりました。

## v2.3.1

_2023年12月7日_

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.4以降

![新規](../assets/new.svg)<!-- PAY-5047 -->次の場所から、クレジット/デビットカードのブランドまたは支払い方法の種類を利用できるようになりました。

- ストアフロントの顧客注文ページでは
- 買い物客に送信された注文確認メール
- Commerce Adminの[注文詳細ビュー](https://experienceleague.adobe.com/docs/commerce-admin/stores-sales/order-management/orders/order-processing.html#view-an-order)から。

## v2.3.0

_2023年12月1日_

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.4以降

![新規](../assets/new.svg)<!-- PAY-4381 --> [決済サービスでGraphQL統合がサポートされるようになりました](https://developer.adobe.com/commerce/webapi/graphql/payment-services/)。 GraphQLがPayPal支払いボタン、ホスティングフィールド、Apple Payをサポートするようになったことで、[!DNL Payment Services]はヘッドレス Commerce設定をサポートするようになりました。

## v2.2.1

_2023年9月27日_

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.4以降

![修正済みの問題](../assets/fix.svg)<!-- Issue PAY-4870 -->最新リリースで拡張機能バージョンを送信する際に、Storefrontで新しいヘッダー属性が正しく入力されない問題を修正しました。 以前は、Commerce Services コネクタの`1.3.0` リリースで、`User-Agent header`拡張機能から[!DNL Payment Services]を拡張できませんでした。

## v2.2.0

_2023年8月30日_

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.4以降

![新規](../assets/new.svg)<!-- PAY-4638 -->が[との統合をSignifyd](fraud-protection.md)に追加しました。これにより、自動不正利用防止サービスを提供できます。

![新規](../assets/new.svg)<!-- PAY-3981 --> [Apple PayをPayPal支払いボタン以外の別の支払いオプション &#x200B;](payments-options.md#apple-pay-button)に昇格し、買い物客が支払いオプションを見やすくしました。また、販売者がApple Payの配置とスタイルを制御できるようにしました。

![新規](../assets/new.svg)<!-- PAY-4002 -->支払いアイコンの追加などのスタイルの機能強化を含む、クレジットカードのチェックアウト項目のユーザーエクスペリエンスを改善して、買い物客の認知度を低下させ、コンバージョンを増加させました。

![新規](../assets/new.svg)<!-- PAY-4002 -->販売者が支払いオプションの順序を[並べ替え](configure-admin.md#paypal-payment-buttons)して特定の支払いオプションを優先できるようにする機能を追加しました。 この機能は、チェックアウト時の会話率の向上に役立ちます。

![新規](../assets/new.svg)<!-- PAY-4035 -->の販売者は、[管理者ホームページから入手できる新しい](reporting.md#transactions-report-view) トランザクション レポート [!DNL Payment Services]を使用して、ストアの健全性を効率的に監視し、トランザクションの問題を特定できるようになりました。 このレポートには、取引承認率とマイナスの取引傾向に関するデータも示されています。

## v2.1.0

_2023年6月9日_

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.4以降

![新規](../assets/new.svg)<!-- Issue xxx --> Adobe Commerce 2.4.7-beta1のサポートを追加しました。

![新規](../assets/new.svg)<!-- Issue xxx -->次の国と関連通貨[で](compatibility.md#standard-vs-advanced-payment-services-experience)の利用可能性が追加されました：オーストラリア、フランス、英国。

![新規](../assets/new.svg)<!-- Issue PAY-4296 -->管理者ユーザーが顧客の注文を作成および管理し、セールスメニューに[を表示できるように、管理者ロール &#x200B;](configure-admin.md#configure-roles)の[!DNL Payment Services]拡張リソースを追加しました。

![新規](../assets/new.svg)<!-- Issue PAY-4236 --> チェックアウト中にエラーが発生した注文に対して[自動無効化を追加しました](checkout.md#order-auto-voided-if-error)。

![新規](../assets/new.svg)<!-- Issue PAY-4183 --> チェックアウトページに「[&#x200B; クレジット/デビットカード支払いオプション」ボタン &#x200B;](payments-options.md#paypal-debit-or-credit-card-button)を表示する機能を作成しました。

## v2.0.0

_2023年3月10日_

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.4以降

![新規](../assets/new.svg)<!-- Issue PAY-4152 --> PHP 8.2およびAdobe Commerce 2.4.6のサポートを追加しました。PHP 7.xとの互換性はありません。

## v1.6.1

_2023年3月10日_

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.4以降

![修正](../assets/fix.svg)<!-- Issue PAY-4226 -->新しい[!DNL Payment Services]販売者が管理画面でチェックアウトを使用できない問題を修正しました。[!DNL Payment Services]は、以前はCommerceのお客様IDを使用していましたが、新規のお客様には存在しません。

![修正](../assets/fix.svg)<!-- Issue PAY-4205 --> [PayPal オプション &#x200B;](payments-options.md#paypal-payment-buttons)を使用して、チェックアウト時に、指定された配送先住所の状態をデフォルトの税金設定の状態に置き換える問題を修正しました。 これで、お客様は、注文を加盟店の税金設定でデフォルトとして設定された状態とは異なる状態に出荷できます。

![修正](../assets/fix.svg)<!-- Issue PAY-4202 --> [支払いアクション `Authorize and Capture`を使用して、お客様がカード保管を使用してストア &#x200B;](production.md#set-payment-services-as-payment-method)の購入を完了したり、保管された支払い方法を削除したりできない問題を修正しました。 以前は、顧客がボールト付きクレジットカードを使用または変更しようとすると、「Provider Vault IDが見つかりません」エラーが表示されていました。

## v1.6.0

_2023年2月17日_

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.0以降

![新規](../assets/new.svg)<!-- Issue PAY-3540 -->欧州連合（EU）と英国で取引するマーチャント向けに[PCI 3DS コンプライアンス機能を追加](security.md#3ds)。 この追加のセキュリティレイヤーは、購入者にクレジットカード発行元での認証を義務付けており、オンラインでの詐欺を防ぐのに役立ち、欧州連合（EU）のコンプライアンス規制の一部として必要とされています。

![新規](../assets/new.svg)<!-- Issue PAY-3609 -->管理者[で](vaulting.md#use-vaulting-in-the-admin) カードの保管を有効にする機能を追加しました。 これにより、管理画面で保管されている顧客の注文を、保管されている支払い方法を使用して作成できるようになります。

## v1.5.4

_2023年1月29日_

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.0以降

![修正済みの問題](../assets/fix.svg)<!-- Issue PAY-4110 -->購入者が製品ページ、ミニカート、カートの支払いボタンを使用して注文できない問題を修正しました。 バイヤーは注文を正常に完了できるようになりました。

## v1.5.3

_2023年1月25日_

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.0以降

![修正済みの問題](../assets/fix.svg)<!-- Issue PAY-4102 -->下位互換性のない既知の問題に対する修正をリリースしました。 このリリースでは、サービス ID拡張機能のバージョンが最新の安定バージョンにロックされ、新しい[!DNL Payment Services] インストールでCommerce サービスを再構成できるようになります。

## v1.5.2

_2022年12月22日_

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.0以降

![問題を修正](../assets/fix.svg)<!-- Issue PAY-3992 -->支払い方法が拒否された場合の[!DNL Payment Services]の請求書の処理を改善しました。

![修正済みの問題](../assets/fix.svg)<!-- Issue PAY-3999 -->[!DNL Payment Services]が、チェックアウトページに[Fire Checkoutの](https://commercemarketplace.adobe.com/swissup-firecheckout.html){target=_blank} カスタムテンプレートを使用して、加盟店のPayPal支払いボタンを正しく表示するようになりました。 以前は、ミニカートにボタンが断続的に表示されていました。

## v1.5.1

_2022年11月23日_

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.0以降

![新規](../assets/new.svg)<!-- Issue PAY-3923 -->[!DNL Payment Services]には、ユーザーエージェントヘッダーにバージョン番号が含まれるようになりました。これにより、リクエストは未使用のエンドポイントを追跡、フィルタリング、非推奨にできます。

![修正済みの問題](../assets/fix.svg)<!-- Issue PAY-3968 -->[!DNL Payment Services]は、支払いボタンを使用して製品ページから注文が行われたときに、注文データを正しく表示するようになりました。

## v1.5.0

_2022年11月18日_

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.0以降

![新規](../assets/new.svg)<!-- Issue PAY-3880 -->買い物客は、チェックアウト [中にクレジットカード情報を](vaulting.md)保管（保存）して、同じアカウント内の同じ店舗または別の店舗で後から購入する際に使用できるようになりました。

![新規](../assets/new.svg)<!-- Issue PAY-3950 -->販売者は、店舗の[即時Commerce機能](https://experienceleague.adobe.com/docs/commerce-admin/stores-sales/point-of-purchase/checkout-instant-purchase.html)を有効にして、買い物客がチェックアウトを迅速化できるようにしました（[有効なクレジットカード情報](vaulting.md)）。

## v1.4.1

_2022年10月14日_

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.0以降

![修正](../assets/fix.svg)<!-- Issue PAY-3766 -->お客様のお支払い方法が拒否された場合、表示されるエラーメッセージはより分かりやすいものになります。 お客様に支払い情報を再入力して、もう一度試すか、別の支払い方法を試すか、トランザクションが拒否された場合に銀行に連絡することをお勧めします。

## v1.4.0

_2022年9月30日_

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.0以降

![新規](../assets/new.svg)<!-- Issue PAY-784 -->[!DNL Payment Services]には、[複数のPayPal ビジネス アカウントを使用するように加盟店アカウントを設定する機能が追加されました](configure-admin.md#use-multiple-paypal-accounts)。 これにより、異なる通貨を使用して複数の国で店舗を運営したり、ビジネスの一部にAdobe Commerceを使用したりすることが可能になります。

![新規](../assets/new.svg)<!-- Issue PAY-3231 -->のマーチャントは、[web サイトまたは個々のストアビュー設定に[!UICONTROL Soft Descriptor]](configure-admin.md)を追加して、顧客トランザクション銀行取引明細書に表示し、ブランド、ストア、または製品ラインを明確にできます。

![新規](../assets/new.svg)<!-- Issue PAY-3707 --> [&#x200B; チェックアウト用のクレジットカードのフィールドとPayPal支払いボタン &#x200B;](configure-admin.md#paypal-payment-buttons)を[!DNL Payment Services]設定で有効または無効にします。

![修正済みの問題](../assets/fix.svg)<!-- Issue PAY-3546 -->顧客が&#x200B;**[!UICONTROL Edit cart]**&#x200B;をクリックすると、ページはカートページにリダイレクトされ、空のカートを表示する代わりに更新されたアイテムが表示されます。

## v1.3.1

_2022年9月6日_

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.0以降

![修正された問題](../assets/fix.svg)<!-- Issue PAY-3663 -->これで、加盟店の店舗がグローバル以外の通貨で承認された注文をキャプチャする際に、キャプチャプロセスが完了し、エラーは表示されなくなりました。

## v1.3.0

_2022年8月9日_

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.0以降

![新規](../assets/new.svg)<!-- Issue PAY-XX -->一般公開リリース – [!DNL Payment Services]は、[および [!DNL Adobe Commerce]  バージョン 2.4.0から2.4.5 [!DNL Magento Open Source] で](https://experienceleague.adobe.com/en/docs/commerce-operations/release/product-availability) サポートされるようになりました。

![修正済みの問題](../assets/fix.svg)<!-- Issue PAY-x --> Apple Payは、モバイルおよびデスクトップでSafari ブラウザーv15.5と互換性を持つようになりました。

## v1.2.0

_2022年6月29日_

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.0以降

![既知の問題](../assets/bug.svg)<!-- Issue PAY-x --> Apple Payは、モバイルおよびデスクトップのSafari ブラウザーv15.5と互換性がありません。 Safari バージョン 15.5を使用している場合、Apple Payでチェックアウトを完了できません。

![修正済みの問題](../assets/fix.svg)<!-- Issue PAY-3264 -->以前は、ログインユーザーがアカウントのデフォルトのアドレス以外の請求/配送先住所を選択した場合、チェックアウトに失敗しました。 これで、選択した請求/配送先住所が（デフォルトの保存先住所ではなく）送信され、チェックアウトが正常に完了しました。

![修正済みの問題](../assets/fix.svg)<!-- Issue PAY-3314 --> チェックアウト時にPayPal支払いボタンを無効にすると、エラーは表示されません。

![修正済みの問題](../assets/fix.svg)<!-- Issue PAY-3330 --> ゲストユーザーがダッシュを含む電話番号を入力すると、チェックアウト中に支払いが失敗しなくなりました。

![修正された問題](../assets/fix.svg)<!-- Issue PAY-3338 PAY-2502 --> Commerce サービスの資格情報が無効な場合、[!DNL Payment Services]は、管理者の[!DNL Payment Services] ホームから資格情報のエラーを表示して警告を表示するようになりました。

![既知の問題](../assets/bug.svg)<!-- Issue PAY-0 --> [!DNL Payment Services]は`commerce-data-export` v101.20以降と互換性がありません。これにより、[[!DNL Channel manager] 拡張機能](https://experienceleague.adobe.com/docs/commerce-channels/channel-manager/guide-overview.html)と互換性がなくなります。

## v1.1.0

_2022年3月31日_

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.0以降

![新規](../assets/new.svg)<!-- Issue PAY-2127 -->一般公開リリース – [!DNL Payment Services]は、[および [!DNL Adobe Commerce]  バージョン 2.4.0から2.4.4 [!DNL Magento Open Source] で](https://experienceleague.adobe.com/en/docs/commerce-operations/release/product-availability) サポートされるようになりました。

![新規](../assets/new.svg)<!-- Issue PAY-2682 --> [!DNL Payment Services]と[!DNL Adobe Commerce]の[!DNL Magento Open Source]拡張機能が、カナダのマーチャント向けに利用可能になりました。 加盟店は、[&#x200B; フランス語](compatibility.md##standard-vs-advanced-payment-services-experience)または[英語](compatibility.md#standard-vs-advanced-payment-services-experience)のいずれかで支払い設定を表示できます。

![新規](../assets/new.svg)<!-- Issue PAY-2681 --> [!DNL Payment Services]は、クレジットカードとPayPal トランザクションに[&#x200B; カナダ ドル （CAD） &#x200B;](compatibility.md#standard-vs-advanced-payment-services-experience)をサポートしています。

![新規](../assets/new.svg)<!-- Issue PAY-2680 -->のマーチャントは、英語またはフランス語の拡張機能を[&#x200B; オンボード  [!DNL Payment Services]](onboard.md)できます。

![新規](../assets/new.svg)<!-- Issue PAY-2678 -->の販売者は、[注文支払い状況](order-payment-status.md)と[支払い状況レポート &#x200B;](payouts.md)の両方をカナダドル （CAD）で表示できるようになりました。

![修正された問題](../assets/fix.svg)<!-- Issue PAY-2710 -->[!DNL Payment Services]は、[PHP 8.1](https://www.php.net/releases/8.1/en.php)と互換性を持つようになりました。

![問題を修正](../assets/fix.svg)<!-- Issue PAY-3017 -->複数のストアで適切なアラートを表示するためのサンドボックスモードのアラートを改善しました。

![修正済みの問題](../assets/fix.svg)<!-- Issue PAY-2742 --> Venmoなどの利用可能な支払い方法をストアビューレベルで有効または無効にできるようになりました。 以前は、web サイトごとに支払い方法を設定することしかできませんでした。

![修正された問題](../assets/fix.svg)<!-- Issue PAY-2277 -->個々のPayPal支払いボタンを選択して[有効または無効にできるようになりました](configure-admin.md#paypal-payment-buttons)。

![修正済みの問題](../assets/fix.svg)<!-- Issue PAY-2561 -->以前に削除した製品が&#x200B;_レビュー注文_ ページのカートに表示されない。

![既知の問題](../assets/bug.svg)<!-- Issue PAY-2842 --> サンドボックス環境で支払いを処理する場合、クレジットカード取引[のテストがPayPal](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/payments/payservices-cc-sandbox-failure.html)で失敗する可能性があります。

## v1.0.0

_2021年11月29日_

[!BADGE &#x200B; サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.0以降

![新規](../assets/new.svg)<!-- Issue PAY-2127 -->一般公開リリース – [[!DNL Payment Services]](https://commercemarketplace.adobe.com/magento-payment-services.html)は、[!DNL Adobe Commerce]および[!DNL Magento Open Source] バージョン 2.4.0 ～ 2.4.3-p1でサポートされるようになりました。

![新規](../assets/new.svg)<!-- Issue PAY-124 --> [!DNL Payment Services]および[!DNL Adobe Commerce]の[!DNL Magento Open Source]拡張機能は、[[!DNL Adobe Commerce]  クラウドインフラストラクチャ &#x200B;](install.md#adobe-commerce-on-cloud-infrastructure)または[&#x200B; オンプレミス &#x200B;](install.md#on-premises-and-other-configurations) インスタンスのいずれかにインストールできます。 これらの方法では、コマンドラインインターフェイスを使用する必要があります。

![新規](../assets/new.svg)<!-- Issue PAY-1986 --> [!DNL Payment Services]は、マーチャントがテストモードで拡張機能を評価できるようにする[&#x200B; サンドボックスアカウント &#x200B;](sandbox.md)をサポートしています。

![新規](../assets/new.svg)<!-- Issue PAY-666 -->のマーチャントは、[をサンドボックスまたは実稼動環境に切り替えるなど、基本的な支払い動作を使用して](configure-admin.md)決済サービス [`Authorize and Capture`](production.md#set-payment-services-as-payment-method)拡張機能を設定できます。

![新規](../assets/new.svg)<!-- Issue PAY-780 -->買い物客は[!DNL Payment Services]または[手動での注文作成](create-order.md)を通じてチェックアウトできます。

![新規](../assets/new.svg)<!-- Issue PAY-1856 -->注文支払い状況[および](order-payment-status.md)支払いレポート [を介した包括的なレポートが](payouts.md)で利用できるので、ストアの注文と関連する支払いを明確に把握できます。[!DNL Payment Services]

![新規](../assets/new.svg)<!-- Issue PAY-311 --> [!DNL Payment Services]は、あらゆる販売者に対応した、合計処理量に基づく柔軟な階層価格をサポートしています。

![新規](../assets/new.svg)<!-- Issue PAY-1443 --> [拡張機能のPayPal支払いボタンとクレジットカードのフィールドのルックアンドフィール &#x200B;](payments-options.md)を簡単に[!DNL Payment Services] カスタマイズできます。

![既知の問題](../assets/bug.svg)<!-- Issue PAY-2473 -->拡張機能のインストール中に[不正なComposer キー](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/payments/payservices-install.html)を使用すると、ユーザーは[正しい](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/prerequisites/authentication-keys)を使用して`MAGEID`認証できません。

![既知の問題](../assets/bug.svg)<!-- Issue PAY-2474 --> [!DNL Payment Services]件のレポート [はすぐに同期できません](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/payments/payservices-report-info-delayed.html)。

![既知の問題](../assets/bug.svg)<!-- Issue PAY-2475 --> [の](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/payments/payservices-paypal-acct.html)PayPal サンドボックスアカウント [!DNL Payment Services]は、オンボーディング中にそのアカウントを作成した場合、確認できません。
