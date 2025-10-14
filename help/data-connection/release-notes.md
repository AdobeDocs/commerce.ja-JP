---
title: リリースノート
description: Adobe Commerceの拡張機能の最新  [!DNL Data Connection]  リリース情報です。
feature: Personalization, Integration, Release Notes
exl-id: f3b92632-947d-40cd-89b7-24ed0680be51
source-git-commit: 9c10aecb303dd09a85bdafa93d791d30611ec8b2
workflow-type: tm+mt
source-wordcount: '1290'
ht-degree: 1%

---

# リリースノート

>[!IMPORTANT]
>
>Experience Platform コネクタの名前は [!DNL Data Connection] に変更されました。

このリリースノートには、[!DNL Data Connection] 拡張機能のアップデートが含まれています。アップデートには次のものが含まれます。

![&#x200B; 新機能 &#x200B;](../assets/new.svg) – 新機能
![&#x200B; 修正 &#x200B;](../assets/fix.svg) – 修正点と改善点
![&#x200B; バグ &#x200B;](../assets/bug.svg) – 既知の問題

[!DNL Data Connection] 拡張機能で使用される拡張機能に関連する機能の変更と修正については、**サポートされるサービス更新** を参照してください。

リリーススケジュールとサポートについては、[&#x200B; 今後のリリース &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-operations/release/planning/schedule) を参照してください。

開発者向けドキュメントの [&#x200B; このモジュールをサポートするCommerceのバージョンについては &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-operations/release/product-availability) を参照してください。

## サポートされるサービスのアップデート

これらのリリースノートでは、[!DNL Data Connection] 拡張機能で使用される拡張機能に関連する機能の変更と修正について説明します。

+++サポートされるサービスのアップデート

_2025 年 8 月 7 日_

![&#x200B; 新規 &#x200B;](../assets/new.svg) - 3.3.0 リリースでは、[&#x200B; カスタム属性をプロファイル &#x200B;](custom-identities.md) に追加できるようになりました。

_2024 年 8 月 2 日_

![&#x200B; 修正 &#x200B;](../assets/fix.svg) – 注文合計が税金を含むように設定されている場合に、支払合計金額を修正しました。
![&#x200B; 新規 &#x200B;](../assets/new.svg) – 購入イベントを注文するための `taxAmount` フィールドを追加しました。
![&#x200B; 新規 &#x200B;](../assets/new.svg) - イベントにカスタムデータを追加する機能を追加しました。 [&#x200B; 例 &#x200B;](https://github.com/adobe/commerce-events/blob/main/examples/events/custom-event-override.md) については、次を参照してください。

_2024 年 1 月 24 日_

![&#x200B; 新規 &#x200B;](../assets/new.svg) - `data-services-b2b` 拡張機能が更新され、B2B マーチャント向けの `deleteRequisitionList` という新しい要求イベントが追加されました。

_2023 年 11 月 16 日_

![&#x200B; 修正 &#x200B;](../assets/fix.svg) – 複数の配送先住所を持つ注文を行った際に、エラーメッセージが正しく表示されない問題を修正しました。
![&#x200B; 修正 &#x200B;](../assets/fix.svg) - `productPageView` イベントで、ストアビューで通貨を切り替えた後、`productListItems.priceTotal` イベントフィールドで価格が変換されない問題を修正しました。
![&#x200B; 修正 &#x200B;](../assets/fix.svg) - `productListItems` イベント フィールドで、マーチャントがストアビューを切り替えた際に通貨コードが更新されなかった問題を修正しました。

_2023 年 10 月 10 日_

![&#x200B; 新規 &#x200B;](../assets/new.svg) – 新しい注文ステータスイベントとして、[&#x200B; 注文請求済み &#x200B;](events-backoffice.md#orderinvoiced)、[&#x200B; 注文品目返品開始 &#x200B;](events-backoffice.md#orderitemsreturninitiated)、および [&#x200B; 注文品目返品完了 &#x200B;](events-backoffice.md#orderitemreturncompleted) が追加されました。
![&#x200B; 修正 &#x200B;](../assets/fix.svg) - キャッシュを更新した後、通貨設定の変更がイベントに反映されない問題を修正しました。
![&#x200B; 修正 &#x200B;](../assets/fix.svg) – 非同期注文配置が有効な場合に、注文確認メッセージが表示されないエラーを修正しました。
![&#x200B; 新規 &#x200B;](../assets/new.svg) - カテゴリ表示ページ `addToRequisitionList` シンプルな製品のイベントにデータを追加しました。
![&#x200B; 修正 &#x200B;](../assets/fix.svg) – 注文確認ページから商品が追加された際に、`selectedOptions` イベントの `addToRequisitionList` データで発生していた問題を修正しました。
![&#x200B; 新規 &#x200B;](../assets/new.svg) - カテゴリ表示ページから購買依頼リストに製品 `addToRequisitionList` 追加されたときに、イベントに製品データが追加されました。
![&#x200B; 新規 &#x200B;](../assets/new.svg) – 「製品 `addToRequisitionList` 示」ページから構成可能な製品を購買依頼リストに追加した場合のイベントを追加しました。
![&#x200B; 新規 &#x200B;](../assets/new.svg) – 製品数量が購買依頼リストから増加または減少した場合の `addToRequisitionList` および `removeFromRequisitionList` のイベントが追加されました。

_2023 年 6 月 10 日_

![&#x200B; 修正 &#x200B;](../assets/fix.svg) - Commerce注文識別子のプレフィックスが原因で `orderId` がコンテキストで渡されなかった問題を修正しました。
![&#x200B; 修正 &#x200B;](../assets/fix.svg) - コンテンツセキュリティポリシー設定を更新しました。

_2023 年 3 月 30 日_

![&#x200B; 新規 &#x200B;](../assets/new.svg) - B2B マーチャント用の `data-services-b2b` 購入リストイベント [&#x200B; を含む &#x200B;](events.md#b2b-events) という拡張機能を追加しました。
![&#x200B; 新規 &#x200B;](../assets/new.svg) - `uniqueIdentifier` 検索 [&#x200B; イベントに「](events.md#search-events)」フィールドを追加しました。 この新しいフィールドを使用すると、マーチャントは、検索リクエストと検索応答を相互参照できます。

_2022 年 10 月 12 日_

![&#x200B; 新規 &#x200B;](../assets/new.svg) - Adobe Commerce Storefront イベントのSDKおよびコレクターに、[&#x200B; と &#x200B;](events.md) の 2 つの `openCart`storefront イベント `removeFromCart` を追加しました。
![&#x200B; 新規 &#x200B;](../assets/new.svg) - [AEM ストアフロント &#x200B;](overview.md#aem-support) のサポートを追加しました。

+++

## 3.4.0

_2025 年 9 月 16 日_

[!BADGE &#x200B; 互換性 &#x200B;]{type=Informative tooltip="互換性"} Adobe Commerce バージョン 2.4.4 以降

![&#x200B; 新規 &#x200B;](../assets/new.svg) [!DNL Data Connection] 制限が有効な場合に、cookie/ローカルストレージでのデータの収集と保存を防ぎ、cookie 制限モードに完全に従うようになりました。

## 3.3.0

_2025 年 3 月 21 日_

[!BADGE &#x200B; 互換性 &#x200B;]{type=Informative tooltip="互換性"} Adobe Commerce バージョン 2.4.4 以降

![&#x200B; 新規 &#x200B;](../assets/new.svg) PHP 8.4 のサポートを追加しました。

## 3.2.1

_2025 年 1 月 17 日_

[!BADGE &#x200B; 互換性 &#x200B;]{type=Informative tooltip="互換性"} Adobe Commerce バージョン 2.4.4 以降

![&#x200B; 新規 &#x200B;](../assets/new.svg) - [HIPAA 対応の拡張機能 &#x200B;](hipaa-readiness.md) を [!DNL Data Connection] に追加しました。これにより、マーチャントはバックオフィスイベントデータをExperience Platformと共有し、HIPAA への準拠 [!DNL Commerce] 維持できるようになりました。
![&#x200B; 修正 &#x200B;](../assets/fix.svg) - [!DNL Data Connection] 拡張機能がデータを上書きし、すべてのお客様 `eventForwarding` 対して `HIPAA` フラグを設定していた問題を修正しました。 現在は、拡張機能は HIPAA のお客様向けのフラグのみを設定します。

## 3.2.0

_2024 年 10 月 7 日_

[!BADGE &#x200B; 互換性 &#x200B;]{type=Informative tooltip="互換性"} Adobe Commerce バージョン 2.4.4 以降

![&#x200B; 新規 &#x200B;](../assets/new.svg) - バックオフィスデータに [&#x200B; カスタムオーダー属性 &#x200B;](custom-attributes.md) を作成する機能を追加しました。
![&#x200B; 新規 &#x200B;](../assets/new.svg) – 新しい [&#x200B; カスタム注文属性 &#x200B;](connect-data.md#data-customization) テーブルが追加され、[!DNL Commerce] で設定され、Experience Platformに送信されたカスタム属性を確認できるようになりました。
![&#x200B; 新規 &#x200B;](../assets/new.svg) - プロファイルレコードとデータを [&#x200B; 収集してExperience Platformに送信 &#x200B;](connect-data.md#send-customer-profile-data) する機能が追加されました。

## 3.2.0-beta3

_2024 年 8 月 27 日_

[!BADGE &#x200B; 互換性 &#x200B;]{type=Informative tooltip="互換性"} Adobe Commerce バージョン 2.4.4 以降

![&#x200B; 新規 &#x200B;](../assets/new.svg) - ベータ版に参加している場合は、`composer.json` ファイルのルートレベルに次のものが含まれていることを確認してください：` "minimum-stability": "beta"`。 また、`composer require "magento/customers-connector: ^1.2.0"` を追加して、Commerce インスタンスから SaaS に顧客プロファイルを送信します。
![&#x200B; 新規 &#x200B;](../assets/new.svg) – このリリースには、3.1.1、3.1.2、3.1.3、および 3.1.4 でリリースされたパッチが含まれています。

## 3.1.4

_2024 年 8 月 9 日_

[!BADGE &#x200B; 互換性 &#x200B;]{type=Informative tooltip="互換性"} Adobe Commerce バージョン 2.4.4 以降

![&#x200B; 修正 &#x200B;](../assets/fix.svg) – 未使用のデータエクスポーターとインデクサーを追加で削除する `experience-platform-connector` メタパッケージを更新しました。

## 3.1.3

_2024 年 7 月 22 日_

[!BADGE &#x200B; 互換性 &#x200B;]{type=Informative tooltip="互換性"} Adobe Commerce バージョン 2.4.4 以降

![&#x200B; 修正 &#x200B;](../assets/fix.svg) – 未使用のデータエクスポーターとインデクサーを削除するように `experience-platform-connector` メタパッケージを更新しました。

## 3.1.2

_2024 年 6 月 5 日_

[!BADGE &#x200B; 互換性 &#x200B;]{type=Informative tooltip="互換性"} Adobe Commerce バージョン 2.4.4 以降

![&#x200B; 修正 &#x200B;](../assets/fix.svg) - [&#x200B; 履歴同期 &#x200B;](connect-data.md#specify-order-history-date-range) を開始する際に、間違った日付形式が使用されていた問題を修正しました。
![&#x200B; 修正 &#x200B;](../assets/fix.svg) - Adobe Commerce 2.4.7 で `startCheckout` イベントが送信されない問題を修正しました。

## 3.1.1

_2024 年 4 月 4 日_

[!BADGE &#x200B; 互換性 &#x200B;]{type=Informative tooltip="互換性"} Adobe Commerce バージョン 2.4.4 以降

![&#x200B; 新規 &#x200B;](../assets/new.svg) – すべての [!DNL Data Connection] 拡張機能で PHP 8.3 のサポートを追加しました。
![&#x200B; 新規 &#x200B;](../assets/new.svg) - Adobe Experience Platform Mobile SDKとCommerceを [&#x200B; 統合 &#x200B;](mobile-sdk-epc.md) する方法に関する記事を追加しました。

## 3.2.0-beta2

_2024 年 3 月 4 日_

[!BADGE &#x200B; 互換性 &#x200B;]{type=Informative tooltip="互換性"} Adobe Commerce バージョン 2.4.4 以降

![&#x200B; 新規 &#x200B;](../assets/new.svg) - ベータ版に参加している場合は、`composer.json` ファイルのルートレベルに次のものが含まれていることを確認してください：` "minimum-stability": "beta"`。 また、`composer require "magento/customers-connector: ^1.2.0"` を追加して、Commerce インスタンスから SaaS に顧客プロファイルを送信します。
![&#x200B; 新規 &#x200B;](../assets/new.svg) - [&#x200B; カスタム属性を追加 &#x200B;](custom-attributes.md) 機能を追加しました。
![&#x200B; 新規 &#x200B;](../assets/new.svg) - プロファイルレコードとデータを [&#x200B; 収集してExperience Platformに送信 &#x200B;](connect-data.md#send-customer-profile-data) する機能が追加されました。

## 3.1.0

_2023 年 11 月 16 日_

[!BADGE &#x200B; 互換性 &#x200B;]{type=Informative tooltip="互換性"} Adobe Commerce バージョン 2.4.4 以降

![&#x200B; 新規 &#x200B;](../assets/new.svg) - Experience Platform コネクタの名前が [!DNL Data Connection] に変更されました。
![&#x200B; 修正 &#x200B;](../assets/fix.svg) - Adobe IMSがアクセストークンを生成できない場合にエラー応答をログに記録できるようになりました。
![&#x200B; 修正 &#x200B;](../assets/fix.svg) – 注文履歴を同期しようとしたが、アカウント資格情報を指定していない場合に表示される通知メッセージを追加しました。

## 3.0.0

_2023 年 10 月 10 日_

[!BADGE &#x200B; 互換性 &#x200B;]{type=Informative tooltip="互換性"} Adobe Commerce バージョン 2.4.4 以降

これはメジャーバージョンリリースです。 [&#x200B; 編集 &#x200B;](install.md#update-the-data-connection) プロジェクトのルートの composer.json ファイル。

![&#x200B; 新規 &#x200B;](../assets/new.svg) - Experience Platformに注文履歴 [&#x200B; データおよびステータスを &#x200B;](connect-data.md#send-historical-order-data) 送信する一般提供
![&#x200B; 新規 &#x200B;](../assets/new.svg) - [&#x200B; 拡張機能を &#x200B;](connect-data.md#connect-commerce-data-to-adobe-experience-platform) 設定 [!DNL Data Connection] する際に、OAuth 2.0 のサポートを追加しました。
![&#x200B; 新規 &#x200B;](../assets/new.svg) - Adobe Commerce 2.4.3 のサポートを終了しました。

## 2.3.0

_2023 年 6 月 27 日_

[!BADGE &#x200B; サポート対象 &#x200B;]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.3 以降

![&#x200B; 新規 &#x200B;](../assets/new.svg) - Experience Platformへの [&#x200B; ストアフロントイベントの送信をオフにする &#x200B;](connect-data.md#data-collection) 機能が追加されました。
![&#x200B; 修正 &#x200B;](../assets/fix.svg) - コンテンツセキュリティポリシー設定を更新しました。
![&#x200B; 修正 &#x200B;](../assets/fix.svg) - Commerce 2.4.7 バージョンのバックオフィスイベントのサポートを修正しました。
![&#x200B; 新規 &#x200B;](../assets/new.svg) - [!DNL Data Connection] 拡張機能フォームに対する変更を保存する際の、キャッシュの無効化に関する通知メッセージを追加しました。

## 3.0.0-beta1 （内部のみ）

_2023 年 6 月 13 日_

[!BADGE &#x200B; サポート対象 &#x200B;]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.3 以降

![&#x200B; 新規 &#x200B;](../assets/new.svg) - （Beta）Experience Platformに注文履歴 [&#x200B; データおよびステータスを送信 &#x200B;](connect-data.md#beta-send-historical-order-data) る機能が追加されました。

## 2.2.0

_2023 年 3 月 30 日_

[!BADGE &#x200B; サポート対象 &#x200B;]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.3 以降

![&#x200B; 新規 &#x200B;](../assets/new.svg) - `commerce-data-export` 拡張機能に `saas-export` および `experience-platform-connector` の依存関係がバンドルされました。 以前は、これらの依存関係を個別にインストールする必要がありました。 これらの依存関係とマーチャント設定により、[&#x200B; バックオフィスイベント &#x200B;](events-backoffice.md) のサーバーサイド処理が可能になります。
![&#x200B; 新規 &#x200B;](../assets/new.svg) - [`orderShipmentCompleted`](events-backoffice.md#ordershipmentcompleted) という新しいバックオフィスイベントを追加しました。

## 2.1.1

_2023 年 2 月 28 日_

[!BADGE &#x200B; サポート対象 &#x200B;]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.3 以降

![&#x200B; 新規 &#x200B;](../assets/new.svg) – すべての [!DNL Data Connection] 拡張機能で PHP 8.2 のサポートを追加しました。

## 2.1.0

_2023 年 1 月 17 日_

[!BADGE &#x200B; サポート対象 &#x200B;]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.3 以降

![&#x200B; 新規 &#x200B;](../assets/new.svg) - [[!DNL Data Connection] extension Admin](connect-data.md) を更新して、独自のAEP web SDK（alloy）を指定できるようになりました。
![&#x200B; 修正 &#x200B;](../assets/fix.svg) エッジにプッシュされたデータのプライマリ ID を設定する際に、`identityMap` の代わりに `personID` を使用するように変更しました。

## 2.0.1

_2022 年 11 月 10 日_

[!BADGE &#x200B; サポート対象 &#x200B;]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.3 以降

![&#x200B; 修正 &#x200B;](../assets/fix.svg) - Storefront イベントコレクターおよび Storefront イベントSDKが正常に読み込まれた後にのみ、Adobe Experience Platform コンテキストが設定されるようになりました。

## 2.0.0

_2022 年 10 月 12 日_

[!BADGE &#x200B; サポート対象 &#x200B;]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.3 以降

![&#x200B; 新規 &#x200B;](../assets/new.svg) - Adobe Commerce インスタンスをExperience Platformに [&#x200B; 接続 &#x200B;](connect-data.md) する際に、独自のAEP web SDKを指定する機能が追加されました。
![&#x200B; 修正 &#x200B;](../assets/fix.svg) - データストリーム ID を storereview ではなく web サイトにスコープする必要があるので、データストリーム範囲の要件を更新しました。

## 1.0.0

_2022 年 8 月 9 日_

[!BADGE &#x200B; サポート対象 &#x200B;]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.3 以降

![&#x200B; 新規 &#x200B;](../assets/new.svg) – 一般提供リリース。
