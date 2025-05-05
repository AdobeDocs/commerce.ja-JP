---
title: '[!DNL Store Fulfillment by Walmart Commerce Technologies] リリースノート'
description: すべてのリリースについて詳しくは、リリースノ  [!DNL Store Fulfillment by Walmart Commerce Technologies]  トを参照してください。
role: Admin, User, Leader
feature: Shipping/Delivery, Release Notes
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '488'
ht-degree: 0%

---

# リリースノート

このリリースノートは、[!DNL Store Fulfillment Services by Walmart Commerce Technologies] の初期リリースを説明するもので、次のものが含まれます。

![ 新機能 ](../assets/new.svg) 新機能
![ 修正された問題 ](../assets/fix.svg) 修正および改善
![ 既知の問題 ](../assets/bug.svg)

リリーススケジュールとサポートについては、[ 今後のリリース ](https://experienceleague.adobe.com/docs/commerce-operations/release/planning/schedule.html?lang=ja) を参照してください。

この拡張機能をサポートするAdobe Commerceのバージョンについては、[ 製品の可用性 ](https://experienceleague.adobe.com/docs/commerce-operations/release/product-availability.html?lang=ja) を参照してください。

## v1.5.0

*2023 年 8 月 3 日*

[!BADGE &#x200B; サポート対象 &#x200B;]{type=Informative tooltip="サポート"}[Adobe Commerce 2.4.4 ～ 2.4.6](https://experienceleague.adobe.com/docs/commerce-operations/release/product-availability.html?lang=ja) （2.4.6-p1、2.4.5-p3、および 2.4.4-p4 セキュリティパッチリリースを含む）

このリリースには、次のアップデートが含まれています。

![ 新規 ](../assets/fix.svg) [Adobe Commerce セキュリティパッチリリース ](https://experienceleague.adobe.com/docs/commerce-operations/release/notes/security-patches/overview.html?lang=ja)2.4.6-p1、2.4.5-p3 および 2.4.4-p4 をサポートするように拡張機能を更新しました。

![ 新規 ](../assets/new.svg)<!-- WMTP-918 --> 販売メール用の [ 非同期送信 ](sales-emails.md) 設定オプションのサポートを追加しました。 バージョン 1.5.0 にアップグレードしたマーチャントは、メールを直ちに送信（デフォルト）するか、非同期で送信するかを選択できます。

![ 新規 ](../assets/new.svg)<!-- WMTP-916--> [ ソース設定 ](merchant-store-configuration.md) が更新され、国際電話番号形式がサポートされるようになりました。

![ 新規 ](../assets/new.svg) 払戻金額が残額または請求額を超えないようにするロジックが追加されました。

![ 新規 ](../assets/new.svg)<!-- WMTP-882 --> オブジェクト `google.map.LatLng`JSON リテラルに置き換えて、旧バージョンの [!DNL Google Maps] との互換性をサポートしました。

![ 問題を修正 ](../assets/fix.svg)<!-- WMTP- --> 属性カテゴリの競合を防ぐために、`[!DNL Available for Store Pickup]` および `[!DNL Available for Home Delivery]` の製品属性を作成するスクリプトを更新しました。

![ 修正された問題 ](../assets/fix.svg)<!-- WMTP-915 --> 一部のエンティティの読み込みと保存時に無限ループが発生する互換性の問題を修正しました。

![ 修正された問題 ](../assets/fix.svg)<!-- WMTP-921 --> 製品詳細ページ（PDP）から買い物かごに項目 [!DNL Ship to Store] 追加した際に、見積もり検証がトリガーされない問題を修正しました。

![ 問題を修正 ](../assets/fix.svg)<!-- WMTP- 932 --> 宅配が受け付けられない項目に対して、顧客が宅配方法を選択できたチェックアウトの問題を修正しました。

![ 修正された問題 ](../assets/fix.svg) インストールの更新：

- &#x200B;<!-- WMTP-880--> [!DNL Store Fulfillment] 拡張機能のインストール時に誤った web サイトコードが返される問題を修正しました。

- &#x200B;<!-- WMTP-878--> SKU 整数で、インストール中にデータタイプを文字列タイプにキャストする必要がある問題を修正しました。

![ 修正された問題 ](../assets/fix.svg)<!-- WMTP-915--> チェックインエラーコードが見つからないために発生したエラーを修正しました。

![ 問題を修正 ](../assets/fix.svg)<!-- WMTP-932 --> 分注操作中の部分却下に関連するバグを修正しました。

![ 新規 ](../assets/new.svg)<!-- WMTP-953 --> Cancel API エンドポイントを更新して、ステータスパラメーターをオプションのオブジェクトとして使用するようになりました。

![ 新規 ](../assets/new.svg)<!-- WMTP-960 -->Dispend API エンドポイントのログの詳細を改善しました。

## v1.4.0

*2023 年 4 月 13 日*

[!BADGE &#x200B; サポート対象 &#x200B;]{type=Informative tooltip="サポート"}

![ 新規 ](../assets/fix.svg) [!DNL Store Fulfillment] は [2.4.4 ～ 2 [!DNL Adobe Commerce] 4.6 と互換性がある ](https://experienceleague.adobe.com/docs/commerce-operations/release/product-availability.html?lang=ja) ようになりました。


## v1.3.0

*2023 年 2 月 27 日*

[!BADGE &#x200B; サポート対象 &#x200B;]{type=Informative tooltip="サポート"}

このリリースには、次のアップデートが含まれています。

![ 新規 ](../assets/fix.svg)<!-- WMTP-795 --> システム構成の既定のスコープ設定を Web サイトからグローバルに変更することにより、特定のサイトのストア フルフィルメント ソリューションを無効にする機能が追加されました。

## v1.2.0

*2022 年 9 月 27 日*

[!BADGE &#x200B; サポート対象 &#x200B;]{type=Informative tooltip="サポート"}

このリリースには、次のアップデートが含まれています。

![ 新規 ](../assets/fix.svg) [!DNL Store Fulfillment] は [2.4.4 ～ 2 [!DNL Adobe Commerce] 4.5 と互換性がある ](https://experienceleague.adobe.com/docs/commerce-operations/release/product-availability.html?lang=ja) ようになりました。


## v1.1.0

*2022 年 7 月 15 日*

[!BADGE &#x200B; サポート対象 &#x200B;]{type=Informative tooltip="サポート"}

安定性：一般提供（GA）

![ 新規 ](../assets/fix.svg)<!-- WMTP-731 --> デフォルトの車種とモデル選択を追加し、ストアアシストアプリの [ チェックインエクスペリエンス設定 ](check-in-experience-setup.md) を簡略化しました。 以前のバージョンでは、マーチャントは車種とモデルの選択を手動で設定する必要がありました。

## v1.0.0

*2022 年 3 月 4 日*

[!BADGE &#x200B; サポート対象 &#x200B;]{type=Informative tooltip="サポート"}

安定性：一般提供（GA）

## ストアシストアプリ

ストアシストアプリの新しいリリースについて詳しくは、[Apple App Storeまたは ](https://apps.apple.com/us/app/store-assist-by-walmart/id1609281539){target="_blank"}3&rbrace;Google Play ストア [&#128279;](https://play.google.com/store/apps/details?id=com.walmart.faas.storeassist){target="_blank"} のアプリ情報を参照してください。
