---
title: '[!DNL Catalog Adapter] リリースノート'
description: Adobe Commerceの最新  [!DNL Catalog Adapter]  リリース情報です。
feature: Services, Release Notes
recommendations: noCatalog
roles: Admin, Developer
exl-id: d4dd0288-8853-43fe-9103-1aead8d3b56e
source-git-commit: 47419e7e19611dc4a045c195f259e2126ab77372
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 0%

---

# [!DNL Catalog Adapter] Extension リリースノート

これらのリリースノートでは、[!DNL Catalog Adapter] 拡張機能の最新バージョンについて説明します。 現在のメジャーリリースバージョンに対するサポートが提供されます。 古いバージョンのリリースノートが参照用に提供されています。

次のような更新があります。

![ 新機能 ](../assets/new.svg) 新機能
![ 修正 ](../assets/fix.svg) 修正点および改善点
![ バグ ](../assets/bug.svg) 既知の問題


>[!NOTE]
>
>[ カタログアダプタ拡張機能 ](catalog-adapter.md) により、Adobe Commerceの価格インデックス作成が無効になります。 インストール済みの場合は、composer を使用してシステムにインストールされているバージョンを確認できます。 場合によっては、Commerce Service のバージョンを更新せずに、システム上のカタログアダプタ拡張機能をアップグレードして、修正点または新しい機能を取得する必要があります。

## 現在のメジャーバージョン

## 1.0.10 リリース

![ 修正 ](../assets/fix.svg) インポートまたは新しく作成されたバンドル製品の価格クエリで、システムが正しい有効な SKU ではなく連結された SKU を参照に使用しようとすると、内部サーバーエラーが発生する可能性がある問題を修正しました。 バンドル製品の価格クエリで適切な SKU を使用し、正しく解決されるようになりました。<!--MDEE-1040-->

## 1.0.9 リリース

![ 修正 ](../assets/fix.svg)PHP 8.4 の互換性を追加しました。<!--MDEE-941-->

## 1.0.8 リリース

![ 修正 ](../assets/fix.svg) 数値 SKU を持つ設定可能な製品バリアントをウィッシュリストに追加する際に、例外ログでエラーが発生する問題を修正しました。<!--MDEE-876-->
