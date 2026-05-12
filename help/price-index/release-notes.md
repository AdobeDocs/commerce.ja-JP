---
title: '[!DNL Catalog Adapter] リリースノート'
description: Adobe Commerceの [!DNL Catalog Adapter] の最新リリース情報。
feature: Services, Release Notes
recommendations: noCatalog
roles: Admin, Developer
exl-id: d4dd0288-8853-43fe-9103-1aead8d3b56e
TQID: https://experienceleague.adobe.com/btPlBYpdRdf-gMfqSv2px6iMfiI3FfXJSN40j61HXOU
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
source-git-commit: 33cd0e217447351b690646ec8d230f76060a74da
workflow-type: tm+mt
source-wordcount: 193
ht-degree: 0%

---

# [!DNL Catalog Adapter]拡張機能リリースノート

これらのリリースノートでは、[!DNL Catalog Adapter]拡張機能の最新バージョンについて説明しています。 現在のメジャーリリース版のサポートが提供されています。 古いバージョンのリリースノートは、参照用に提供されています。

アップデートには以下が含まれます。

![新機能](../assets/new.svg)
![修正](../assets/fix.svg)修正と機能強化
![ バグ ](../assets/bug.svg)既知の問題


>[!NOTE]
>
>[Catalog Adapter拡張機能](catalog-adapter.md)は、Adobe Commerce価格インデックス作成を無効にします。 インストール済みの場合は、composerを使用してシステムにインストールされているバージョンを確認できます。 場合によっては、システムのカタログアダプタ拡張機能をアップグレードして、Commerce Serviceのバージョンを更新せずに修正や新機能をピックアップする場合があります。

## 現在のメジャーバージョン

## 1.0.10 リリース

![修正](../assets/fix.svg) システムが正しい有効なSKUの代わりに連結されたSKUを検索に使用しようとしたため、読み込まれたバンドル製品または新しく作成されたバンドル製品の価格クエリで内部サーバーエラーが発生する可能性がある問題を修正しました。 バンドル製品の価格クエリで、適切なSKUが使用され、正しく解決されるようになりました。<!--MDEE-1040-->

## 1.0.9 リリース

![修正](../assets/fix.svg) PHP 8.4との互換性を追加しました。<!--MDEE-941-->

## 1.0.8 リリース

![修正](../assets/fix.svg)数値SKUを含む設定可能な製品バリエーションをウィッシュリストに追加する際に、例外ログでエラーが発生する問題を修正しました。<!--MDEE-876-->
