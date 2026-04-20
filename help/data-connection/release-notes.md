---
title: リリースノート
description: Adobe Commerceの [!DNL Data Connection] 拡張機能の最新のリリース情報。
feature: Personalization, Integration, Release Notes
exl-id: f3b92632-947d-40cd-89b7-24ed0680be51
source-git-commit: 14c4178338859d55a7391139033d51d1aa6f7678
workflow-type: tm+mt
source-wordcount: '1307'
ht-degree: 1%

---

# リリースノート

>[!IMPORTANT]
>
>Experience Platform コネクタの名前が[!DNL Data Connection]に変更されました。

これらのリリースノートには、[!DNL Data Connection]拡張機能の更新が含まれており、次のものが含まれています。

![新機能](../assets/new.svg) – 新機能
![修正](../assets/fix.svg) – 修正と改善
![ バグ ](../assets/bug.svg) – 既知の問題

[!DNL Data Connection]拡張機能で使用される拡張機能に関連する機能の変更と修正については、**サポートされているサービスの更新**&#x200B;を参照してください。

リリーススケジュールとサポートについて詳しくは、[今後のリリース ](https://experienceleague.adobe.com/en/docs/commerce-operations/release/planning/schedule)を参照してください。

[このモジュールをサポートするCommerceのバージョンについては、開発者向けドキュメントを参照してください](https://experienceleague.adobe.com/en/docs/commerce-operations/release/product-availability)。

## サポートされているサービス更新

これらのリリースノートでは、[!DNL Data Connection]拡張機能で使用される拡張機能に関連する機能変更と修正について説明します。

+++サポートされているサービス更新

_2025年8月7日_

![新規](../assets/new.svg) - 3.3.0 リリースでは、[ カスタム属性をプロファイル ](custom-identities.md)に追加できるようになりました。

_2024年8月2日_

![修正](../assets/fix.svg) – 注文合計に税金が含まれるように設定されている場合の支払い合計金額を修正しました。
![新規](../assets/new.svg) – 購入イベントを注文するための`taxAmount` フィールドを追加しました。
![新規](../assets/new.svg) - カスタムデータをイベントに追加する機能を追加しました。 [例](https://github.com/adobe/commerce-events/blob/main/examples/events/custom-event-override.md)については、次を参照してください。

_2024年1月24日_

![新規](../assets/new.svg) - `data-services-b2b`拡張機能を更新して、B2B マーチャントの`deleteRequisitionList`という新しい要件イベントを含めました。

_2023年11月16日_

![修正](../assets/fix.svg) – 複数の配送先住所を持つ注文を行うと、エラーメッセージが誤って表示される問題を修正しました。
![修正](../assets/fix.svg) - `productPageView` イベントで、`productListItems.priceTotal` イベントフィールドがストアビューで通貨を切り替えた後に価格を変換できなかった問題を修正しました。
![修正](../assets/fix.svg) – 販売者がストアビューを切り替えたときに通貨コードが更新されなかった`productListItems` イベントフィールドの問題を修正しました。

_2023年10月10日_

![新規](../assets/new.svg) – 新しい注文状況イベントが追加されました：[注文請求済み](events-backoffice.md#orderinvoiced)、[注文品目返品開始](events-backoffice.md#orderitemsreturninitiated)、[注文品返品完了](events-backoffice.md#orderitemreturncompleted)。
![修正](../assets/fix.svg) - キャッシュを更新した後、通貨設定の変更がイベントに反映されない問題を修正しました。
![修正](../assets/fix.svg) – 非同期注文の配置が有効になっている場合に注文確認メッセージが表示されないエラーを修正しました。
![新規](../assets/new.svg) - カテゴリ表示ページのシンプルな製品のデータを`addToRequisitionList` イベントに追加しました。
![修正](../assets/fix.svg) – 注文確認ページから商品が追加された際の`selectedOptions` イベントの`addToRequisitionList` データの問題を修正しました。
![新規](../assets/new.svg) - カテゴリ表示ページから商品が購買リストに追加されたときに、商品データを`addToRequisitionList` イベントに追加しました。
![新規](../assets/new.svg) – 構成可能な製品が製品ビューページから購買リストに追加されたときに`addToRequisitionList` イベントを追加しました。
![新規](../assets/new.svg) – 製品数量が購買リストから増加または減少した場合に、`addToRequisitionList`および`removeFromRequisitionList`件のイベントを追加しました。

_2023年6月10日_

![修正](../assets/fix.svg) - Commerceの注文識別子の接頭辞が原因で`orderId`がコンテキスト内で渡されなかった問題を修正しました。
![修正](../assets/fix.svg) - コンテンツセキュリティポリシー設定を更新しました。

_2023年3月30日_

![新規](../assets/new.svg) - B2B マーチャントの`data-services-b2b`購買リストイベント [を含む](events.md#b2b-events)という拡張機能を追加しました。
![新規](../assets/new.svg) - `uniqueIdentifier` フィールドを[検索](events.md#search-events) イベントに追加しました。 この新しいフィールドにより、マーチャントは検索リクエストと検索応答を相互参照できます。

_2022年10月12日_

![新規](../assets/new.svg) - 2つの[ ストアフロントイベント ](events.md)、`openCart`および`removeFromCart`をAdobe Commerce Storefront Events SDKおよびCollectorに追加しました。
![新規](../assets/new.svg) - [AEM ストアフロント ](overview.md#supported-architecture)のサポートを追加しました。

+++

## 3.5.0

_2026年3月17日_

[!BADGE 互換性]{type=Informative tooltip="互換性"} Adobe Commerce バージョン 2.4.4以降

![新規](../assets/new.svg) PHP 8.5のサポートを追加しました。

## 3.4.0

_2025年9月16日_

[!BADGE 互換性]{type=Informative tooltip="互換性"} Adobe Commerce バージョン 2.4.4以降

![新規](../assets/new.svg) [!DNL Data Connection]は、制限が有効になっている場合に、Cookie/ローカルストレージでのデータ収集と保存を防止することで、Cookie制限モードを完全に尊重するようになりました。

## 3.3.0

_2025年3月21日_

[!BADGE 互換性]{type=Informative tooltip="互換性"} Adobe Commerce バージョン 2.4.4以降

![新規](../assets/new.svg) PHP 8.4のサポートを追加しました。

## 3.2.1

_2025年1月17日_

[!BADGE 互換性]{type=Informative tooltip="互換性"} Adobe Commerce バージョン 2.4.4以降

![新規](../assets/new.svg) - [HIPAA対応の拡張機能](hipaa-readiness.md)を[!DNL Data Connection]に追加しました。これにより、マーチャントは[!DNL Commerce]件のバックオフィスイベント データをExperience Platformと共有し、HIPAA コンプライアンスを維持できます。
![修正](../assets/fix.svg) - [!DNL Data Connection]拡張機能が`eventForwarding` データを上書きし、すべての顧客に`HIPAA` フラグを設定していた問題を修正しました。 この拡張機能は、HIPAA顧客のフラグのみを設定します。

## 3.2.0

_2024年10月7日_

[!BADGE 互換性]{type=Informative tooltip="互換性"} Adobe Commerce バージョン 2.4.4以降

![新規](../assets/new.svg) - バックオフィス データに[ カスタム注文属性](custom-attributes.md)を作成する機能を追加しました。
![新規](../assets/new.svg) - [で設定され、Experience Platformに送信されたカスタム属性を表示するために、新しい](connect-data.md#data-customization) カスタム注文属性[!DNL Commerce] テーブルを追加しました。
![新規](../assets/new.svg) - プロファイルレコード [とデータを](connect-data.md#send-customer-profile-data)収集してExperience Platformに送信する機能を追加しました。

## 3.2.0-beta3

_2024年8月27日_

[!BADGE 互換性]{type=Informative tooltip="互換性"} Adobe Commerce バージョン 2.4.4以降

![新規](../assets/new.svg) - ベータ版に参加する場合は、`composer.json` ファイルのルートレベルが`"minimum-stability": "beta"`であることを確認してください。 また、`composer require "magento/customers-connector: ^1.2.0"`を追加して、お客様のCommerce インスタンスからSaaSに顧客プロファイルを送信します。
![新規](../assets/new.svg) – このリリースには、3.1.1、3.1.2、3.1.3、および3.1.4でリリースされたパッチが含まれています。

## 3.1.4

_2024年8月9日_

[!BADGE 互換性]{type=Informative tooltip="互換性"} Adobe Commerce バージョン 2.4.4以降

![修正](../assets/fix.svg) – 未使用の追加のデータエクスポーターとインデクサーを削除するために、`experience-platform-connector` メタパッケージを更新しました。

## 3.1.3

_2024年7月22日_

[!BADGE 互換性]{type=Informative tooltip="互換性"} Adobe Commerce バージョン 2.4.4以降

![修正](../assets/fix.svg) – 未使用のデータエクスポーターとインデクサーを削除するように`experience-platform-connector` メタパッケージを更新しました。

## 3.1.2

_2024年6月5日_

[!BADGE 互換性]{type=Informative tooltip="互換性"} Adobe Commerce バージョン 2.4.4以降

![修正](../assets/fix.svg) - [履歴の同期を開始する際に、間違った日付形式が使用されていた問題を修正しました](connect-data.md#specify-order-history-date-range)。
![修正](../assets/fix.svg) - Adobe Commerce 2.4.7で`startCheckout` イベントが送信されない問題を修正しました。

## 3.1.1

_2024年4月4日_

[!BADGE 互換性]{type=Informative tooltip="互換性"} Adobe Commerce バージョン 2.4.4以降

![新規](../assets/new.svg) – すべての[!DNL Data Connection]拡張機能に対するPHP 8.3のサポートを追加しました。
![新規](../assets/new.svg) - Adobe Experience Platform Mobile SDKとCommerceを[統合](mobile-sdk-epc.md)する方法に関する記事を追加しました。

## 3.2.0-beta2

_2024年3月4日_

[!BADGE 互換性]{type=Informative tooltip="互換性"} Adobe Commerce バージョン 2.4.4以降

![新規](../assets/new.svg) - ベータ版に参加する場合は、`composer.json` ファイルのルートレベルが`"minimum-stability": "beta"`であることを確認してください。 また、`composer require "magento/customers-connector: ^1.2.0"`を追加して、お客様のCommerce インスタンスからSaaSに顧客プロファイルを送信します。
![新規](../assets/new.svg) - カスタム属性[を](custom-attributes.md)追加する機能を追加しました。
![新規](../assets/new.svg) - プロファイルレコード [とデータを](connect-data.md#send-customer-profile-data)収集してExperience Platformに送信する機能を追加しました。

## 3.1.0

_2023年11月16日_

[!BADGE 互換性]{type=Informative tooltip="互換性"} Adobe Commerce バージョン 2.4.4以降

![新規](../assets/new.svg) - Experience Platform コネクタの名前が[!DNL Data Connection]に変更されました。
![修正](../assets/fix.svg) - Adobe IMSがアクセストークンを生成できない場合のエラー応答を記録する機能を追加しました。
![修正](../assets/fix.svg) – 過去の注文を同期しようとしたが、アカウント資格情報を指定していない場合に通知メッセージを追加しました。

## 3.0.0

_2023年10月10日_

[!BADGE 互換性]{type=Informative tooltip="互換性"} Adobe Commerce バージョン 2.4.4以降

これはメジャーバージョンのリリースです。 プロジェクトのルート composer.json ファイルを[編集](install.md#update)します。

![新規](../assets/new.svg) - [への一般提供は、過去の注文](connect-data.md#send-historical-order-data) データとステータスをExperience Platformに送信します。
![新規](../assets/new.svg) - [拡張機能を](connect-data.md#connect-commerce-data-to-adobe-experience-platform)構成[!DNL Data Connection]するときにOAuth 2.0のサポートを追加しました。
![新規](../assets/new.svg) - Adobe Commerce 2.4.3のサポートを終了しました。

## 2.3.0

_2023年6月27日_

[!BADGE  サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.3以降

![新規](../assets/new.svg) - Experience Platformへのストアフロントイベント [の送信を](connect-data.md#data-collection) オフにする機能を追加しました。
![修正](../assets/fix.svg) - コンテンツセキュリティポリシー設定を更新しました。
![修正](../assets/fix.svg) - Commerce 2.4.7 バージョンでのバックオフィスイベントのサポートを修正しました。
![新規](../assets/new.svg) - [!DNL Data Connection]拡張機能フォームに変更を保存する際に、キャッシュの無効化に関する通知メッセージを追加しました。

## 3.0.0-beta1 （内部のみ）

_2023年6月13日_

[!BADGE  サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.3以降

![新規](../assets/new.svg) - （Beta）過去の注文[ データとステータスを](connect-data.md#send-historical-order-data)Experience Platformに送信する機能を追加しました。

## 2.2.0

_2023年3月30日_

[!BADGE  サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.3以降

![新規](../assets/new.svg) - `commerce-data-export`および`saas-export`の依存関係を`experience-platform-connector`拡張にバンドルしました。 以前は、これらの依存関係を個別にインストールする必要がありました。 これらの依存関係とマーチャント設定により、[ バックオフィスイベント ](events-backoffice.md)のサーバーサイド処理が可能になります。
![新規](../assets/new.svg) - [`orderShipmentCompleted`](events-backoffice.md#ordershipmentcompleted)という新しいバックオフィスイベントを追加しました。

## 2.1.1

_2023年2月28日_

[!BADGE  サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.3以降

![新規](../assets/new.svg) – すべての[!DNL Data Connection]拡張機能に対するPHP 8.2のサポートを追加しました。

## 2.1.0

_2023年1月17日_

[!BADGE  サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.3以降

![新規](../assets/new.svg) - [[!DNL Data Connection] 拡張機能の管理者](connect-data.md)を更新して、独自のAEP Web SDK （合金）を指定できるようにしました。
エッジにプッシュされたデータのプライマリ IDを設定する際に、![修正](../assets/fix.svg)が`identityMap`ではなく`personID`を使用するように変更されました。

## 2.0.1

_2022年11月10日_

[!BADGE  サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.3以降

![修正](../assets/fix.svg) - Storefront Event CollectorとStorefront Event SDKが正常に読み込まれた後にのみ、Adobe Experience Platform コンテキストが設定されるようになりました。

## 2.0.0

_2022年10月12日_

[!BADGE  サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.3以降

![新規](../assets/new.svg) - Adobe Commerce インスタンスを[Experience Platformに](connect-data.md)接続する際に、独自のAEP Web SDKを指定できるようになりました。
![修正](../assets/fix.svg) - データストリーム IDがストアビューではなくweb サイトにスコープされるように、データストリーム スコープの要件を更新しました。

## 1.0.0

_2022年8月9日_

[!BADGE  サポートされている]{type=Informative tooltip="サポート対象"} Adobe Commerce バージョン 2.4.3以降

![新規](../assets/new.svg) – 一般公開リリース。
