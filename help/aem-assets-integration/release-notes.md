---
title: AEM Assets統合リリースノート
description: すべてのAEM Assets統合リリースについては、リリースノートを参照してください。
feature: CMS, Media, Release Notes
exl-id: 0d639565-812f-481a-afd6-6e6fa54ed70e
source-git-commit: 65b63a192f0690ce25d40723a6a9404cfcebc2ea
workflow-type: tm+mt
source-wordcount: '725'
ht-degree: 0%

---

# AEM Assets統合リリースノート

このリリースノートでは、AEM Assets統合の初回リリースについて説明します。リリースノートには次のものが含まれます。

![ 新機能 ](../assets/new.svg) 新機能
![ 修正された問題 ](../assets/fix.svg) 修正および改善
![ 既知の問題 ](../assets/bug.svg)

通常の機能リリースバージョン以外でリリースされた機能の変更と修正については、_ホストサービスのアップデート_ の節を参照してください。

今後のリリース、製品のサポート、AEM Assets Integration 拡張機能をサポートしているAdobe Commerce バージョンについて詳しくは、Adobe Commerce[ リリーススケジュール ](https://experienceleague.adobe.com/en/docs/commerce-operations/release/planning/schedule) および [ 製品の提供 ](https://experienceleague.adobe.com/en/docs/commerce-operations/release/product-availability) に関するトピックを参照してください。

## ホステッド サービスの更新

これらのリリースノートでは、ホステッド サービスの通常の機能リリースの外部で発生した機能の変更と修正について説明します。

+++ホステッド サービスの更新

_2025 年 9 月 11 日_

![ 新しい問題 ](../assets/new.svg) [ カスタム自動マッチング ](https://experienceleague.adobe.com/en/docs/commerce/aem-assets-integration/synchronize/custom-match){target=_blank} エンドポイントを新しい `asset_matches` 属性で更新しました。

_2025 年 2 月 11 日_

![ 新しい問題 ](../assets/new.svg) マーチャントは、製品とカテゴリの画像を同期できるようになりました。

+++

## v1.2.10

_2026 年 1 月 12 日_

[!BADGE  サポート対象 ]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.5 以降のリリース。

![ 修正された問題 ](../assets/fix.svg)<!-- Issue ACAP-1178 --> 製品に画像があり、AEM Assets統合が有効になっている場合に、製品のカスタム属性が REST API を介して更新できなかった問題を修正しました。 現在は、製品のカスタム属性は REST API を介して正しく更新されます。

![ 問題 ](../assets/fix.svg)<!-- Issue ACAP-1172 --> 製品の編集ページの管理 UI で、非表示の製品画像が非表示として表示されない問題を修正しました。 これで、画像の表示ステータスが正しく表示されるようになりました。

![ 問題を修正 ](../assets/fix.svg)<!-- Issue ACAP-1170 --> シリアル化解除エラーが原因で、AEM Assets内の商品画像がAdobe Commerceに同期されない問題を修正しました。 これで、すべての画像属性（`image`、`small_image` および `swatch_image`）が正しく同期されます。

## v1.2.7

_2025 年 11 月 6 日_

[!BADGE  サポート対象 ]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.5 以降のリリース。

![ 問題を修正 ](../assets/fix.svg)<!-- Issue ACAP-1169 -->**ミニカート**、**カート**、**チェックアウト** ページでAEM Assets統合を有効にした後、製品のサムネール画像が一貫して表示されない問題を修正しました。 現在は、製品画像は、ページを更新した後も、すべてのページで一貫してレンダリングされます。

## v1.2.6

_2025 年 10 月 24 日_

[!BADGE  サポート対象 ]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.5 以降のリリース。

![ 修正された問題 ](../assets/fix.svg)<!-- Issue ACAP-1163 --> 連続した一括製品更新リクエストにより、ステータストラッキングフラグがスタックしていて、後続の更新が正しく処理されない可能性がある問題を解決しました。 エラーが発生した場合でも、ステータスをリセットできるようになりました。

## v1.2.5

_2025 年 10 月 22 日_

[!BADGE  サポート対象 ]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.5 以降のリリース。

![ 問題を修正 ](../assets/fix.svg)<!-- Issue ACAP-1161 -->Adobe Commerce管理で既存の画像マッピングの場所を更新すると、PHP タイプのエラーが発生する問題を修正しました。

## v1.2.4

_2025 年 10 月 17 日_

[!BADGE  サポート対象 ]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.5 以降のリリース。

![ 問題を修正 ](../assets/fix.svg)<!-- Issue ACAP-1155 --> カスタム属性の全体的な安定性が向上しました。 非同期 API を使用する場合に、カスタム属性が正しく更新されるようになりました。

![ 修正された問題 ](../assets/fix.svg)<!-- Issue ACAP-1074 --> ベースリンク URL が定義されている場合、[ 製品とアセットの同期 ](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/site-store/store-urls#configure-the-base-url){target=_blank} が失敗しなくなりました。

## v1.2.3

_2025 年 10 月 2 日_

[!BADGE  サポート対象 ]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.5 以降のリリース。

![ 修正された問題 ](../assets/fix.svg)<!-- Issue ACAP-1135 --> 製品属性の更新に関する問題を修正しました。 製品属性が期待どおりに更新され、更新が失敗すると、200 応答ではなく適切なエラーが返されるようになりました。

## v1.2.2

_2025 年 9 月 18 日_

[!BADGE  サポート対象 ]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.5 以降のリリース。

![ 問題を修正 ](../assets/fix.svg)<!-- Issue ACAP-1110 --> ミニ買い物かご、買い物かごおよびチェックアウトページでの全体的な画像の安定性が向上しました。 これらのページ上の画像が正しく読み込まれるようになりました。

## v1.2.0

_2025 年 8 月 7 日_

[!BADGE  サポート対象 ]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.5 以降のリリース。

![ 新しい問題 ](../assets/new.svg)<!-- Issue ACAP-1018 --> マーチャントは、管理者からAssets統合を設定する際に、[ ビジュアライゼーションの所有者 ](https://experienceleague.adobe.com/en/docs/commerce/aem-assets-integration/get-started/setup-synchronization){target=_blank} を選択することで、画像アセットとメディアアセットのソースを選択できるようになりました。

![ 新しい問題 ](../assets/new.svg)<!-- Issue ACAP-1078 --> [ カスタム自動マッチング ](https://experienceleague.adobe.com/en/docs/commerce/aem-assets-integration/synchronize/custom-match){target=_blank} エンドポイントを新しい `asset_matches` 属性で更新しました。 この変更により、独自のマッチングロジックを実装して、特定の `productSku` に関連付けられたすべてのアセットを返すことができます。

## v1.1.2

_2025 年 6 月 11 日_

[!BADGE  サポート対象 ]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.5 以降のリリース。

![ 新規問題 ](../assets/new.svg)<!-- Issue ACAP-1041 --> Adobe Commerce 2.4.8 および PHP 8.4 がサポートされるようになりました。

## v1.1.0

_2025 年 4 月 23 日_

[!BADGE  サポート対象 ]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.5 以降のリリース。

![ 新しい問題 ](../assets/new.svg)<!-- Issue ACAP-955 -->AEMの配信 URL の代わりに [ カスタムドメイン URL](https://experienceleague.adobe.com/en/docs/commerce/aem-assets-integration/get-started/setup-synchronization#optional-configure-the-custom-domain-url) を使用できるようになりました。 マーチャントがAEM ダッシュボードに **カスタムドメイン名** を設定した場合は、Commerceにこの **カスタムドメイン URL** を追加する必要があります。

![ 問題を修正 ](../assets/fix.svg)<!-- Issue ACAP-987 -->AEM Assets同期プロセスの全体的なログを改善しました。

## v1.0.22

_2025 年 3 月 12 日_

[!BADGE  サポート対象 ]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.5 以降のリリース。

![ 新しい問題 ](../assets/new.svg)<!-- Issue ACAP-xx -->AEM Assets セレクターで、[Assets セレクター IMS クライアント ID](https://experienceleague.adobe.com/en/docs/commerce/aem-assets-integration/get-started/setup-synchronization) が必要になり、製品カテゴリおよびページビルダー生成コンテンツでAssets画像をマッピングできるようになりました。

## v1.0.20

_2025 年 2 月 11 日_

[!BADGE  サポート対象 ]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.5 以降のリリース。

![ 新規 ](../assets/new.svg)<!-- Issue ACAP-xx --> 一般提供リリース。
