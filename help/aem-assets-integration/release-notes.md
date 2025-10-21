---
title: AEM Assets統合リリースノート
description: すべてのAEM Assets統合リリースについては、リリースノートを参照してください。
feature: CMS, Media, Release Notes
exl-id: 0d639565-812f-481a-afd6-6e6fa54ed70e
source-git-commit: 141f2291d1ead324a159053145e92ee7d4237a7d
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 0%

---

# AEM Assets統合リリースノート

このリリースノートでは、AEM Assets統合の初回リリースについて説明します。リリースノートには次のものが含まれます。

![&#x200B; 新機能 &#x200B;](../assets/new.svg) 新機能
![&#x200B; 修正された問題 &#x200B;](../assets/fix.svg) 修正および改善
![&#x200B; 既知の問題 &#x200B;](../assets/bug.svg)

通常の機能リリースバージョン以外でリリースされた機能の変更と修正については、_ホストサービスのアップデート_ の節を参照してください。

今後のリリース、製品のサポート、AEM Assets Integration 拡張機能をサポートしているAdobe Commerce バージョンについて詳しくは、Adobe Commerce[&#x200B; リリーススケジュール &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-operations/release/planning/schedule) および [&#x200B; 製品の提供 &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-operations/release/product-availability) に関するトピックを参照してください。

## ホステッド サービスの更新

これらのリリースノートでは、ホステッド サービスの通常の機能リリースの外部で発生した機能の変更と修正について説明します。

+++ホステッド サービスの更新

_2025 年 9 月 11 日_

![&#x200B; 新しい問題 &#x200B;](../assets/new.svg) [&#x200B; カスタム自動マッチング &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce/aem-assets-integration/synchronize/custom-match){target=_blank} エンドポイントを新しい `asset_matches` 属性で更新しました。

_2025 年 2 月 11 日_

![&#x200B; 新しい問題 &#x200B;](../assets/new.svg) マーチャントは、製品とカテゴリの画像を同期できるようになりました。

+++

## v1.2.4

_2025 年 10 月 17 日_

[!BADGE &#x200B; サポート対象 &#x200B;]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.5 以降のリリース。

![&#x200B; 問題を修正 &#x200B;](../assets/fix.svg)<!-- Issue ACAP-1155 --> カスタム属性の全体的な安定性が向上しました。 非同期 API を使用する場合に、カスタム属性が正しく更新されるようになりました。

## v1.2.3

_2025 年 10 月 2 日_

[!BADGE &#x200B; サポート対象 &#x200B;]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.5 以降のリリース。

![&#x200B; 修正された問題 &#x200B;](../assets/fix.svg)<!-- Issue ACAP-1135 --> 製品属性の更新に関する問題を修正しました。 製品属性が期待どおりに更新され、更新が失敗すると、200 応答ではなく適切なエラーが返されるようになりました。

## v1.2.2

_2025 年 9 月 18 日_

[!BADGE &#x200B; サポート対象 &#x200B;]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.5 以降のリリース。

![&#x200B; 問題を修正 &#x200B;](../assets/fix.svg)<!-- Issue ACAP-1110 --> ミニ買い物かご、買い物かごおよびチェックアウトページでの全体的な画像の安定性が向上しました。 これらのページ上の画像が正しく読み込まれるようになりました。

## v1.2.0

_2025 年 8 月 7 日_

[!BADGE &#x200B; サポート対象 &#x200B;]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.5 以降のリリース。

![&#x200B; 新しい問題 &#x200B;](../assets/new.svg)<!-- Issue ACAP-1018 --> マーチャントは、管理者からAssets統合を設定する際に、[&#x200B; ビジュアライゼーションの所有者 &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce/aem-assets-integration/get-started/setup-synchronization){target=_blank} を選択することで、画像アセットとメディアアセットのソースを選択できるようになりました。

![&#x200B; 新しい問題 &#x200B;](../assets/new.svg)<!-- Issue ACAP-1078 --> [&#x200B; カスタム自動マッチング &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce/aem-assets-integration/synchronize/custom-match){target=_blank} エンドポイントを新しい `asset_matches` 属性で更新しました。 この変更により、独自のマッチングロジックを実装して、特定の `productSku` に関連付けられたすべてのアセットを返すことができます。

## v1.1.2

_2025 年 6 月 11 日_

[!BADGE &#x200B; サポート対象 &#x200B;]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.5 以降のリリース。

![&#x200B; 新規問題 &#x200B;](../assets/new.svg)<!-- Issue ACAP-1041 --> Adobe Commerce 2.4.8 および PHP 8.4 がサポートされるようになりました。

## v1.1.0

_2025 年 4 月 23 日_

[!BADGE &#x200B; サポート対象 &#x200B;]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.5 以降のリリース。

![&#x200B; 新しい問題 &#x200B;](../assets/new.svg)<!-- Issue ACAP-955 -->AEMの配信 URL の代わりに [&#x200B; カスタムドメイン URL](https://experienceleague.adobe.com/ja/docs/commerce/aem-assets-integration/get-started/setup-synchronization#optional-configure-the-custom-domain-url) を使用できるようになりました。 マーチャントがAEM ダッシュボードに **カスタムドメイン名** を設定した場合は、Commerceにこの **カスタムドメイン URL** を追加する必要があります。

![&#x200B; 問題を修正 &#x200B;](../assets/fix.svg)<!-- Issue ACAP-987 -->AEM Assets同期プロセスの全体的なログを改善しました。

## v1.0.22

_2025 年 3 月 12 日_

[!BADGE &#x200B; サポート対象 &#x200B;]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.5 以降のリリース。

![&#x200B; 新しい問題 &#x200B;](../assets/new.svg)<!-- Issue ACAP-xx -->AEM Assets セレクターで、[Assets セレクター IMS クライアント ID](https://experienceleague.adobe.com/ja/docs/commerce/aem-assets-integration/get-started/setup-synchronization) が必要になり、製品カテゴリおよびページビルダー生成コンテンツでAssets画像をマッピングできるようになりました。

## v1.0.20

_2025 年 2 月 11 日_

[!BADGE &#x200B; サポート対象 &#x200B;]{type=Informative tooltip="サポート"} Adobe Commerce バージョン 2.4.5 以降のリリース。

![&#x200B; 新規 &#x200B;](../assets/new.svg)<!-- Issue ACAP-xx --> 一般提供リリース。
