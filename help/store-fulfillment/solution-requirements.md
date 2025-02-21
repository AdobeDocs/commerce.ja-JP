---
title: ストアフルフィルメントの要件
description: ' [!DNL Store Fulfillment solution] のプロビジョニングとオンボーディングの要件'
role: Leader, Admin, Developer
level: Intermediate
feature: Shipping/Delivery, Install
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 0%

---

# Adobe Commerceのストアフルフィルメントの要件

以下のセクションでは、Adobe Commerceのストアフルフィルメントソリューションをインストールおよび有効にするための技術的およびビジネス要件について詳しく説明します。

## プラットフォームとソフトウェアのバージョン要件

[!DNL Store Fulfillment] のソリューションは、Adobe Commerceのお客様が次のプラットフォームで利用できます。

- クラウドインフラストラクチャー上のAdobe Commerce（ECE）
- Adobe Commerce オンプレミス（EE）

インストールまたはアップグレードの前に、リリースノートとAdobe Commerceのシステム要件を確認して、インストールまたはアップグレードの要件に影響を与える可能性のあるバージョンの互換性、アップデート、変更点に関する最新情報を入手してください。

- [Store Fulfillment リリースノート](release-notes.md)

- [Adobe Commerceのリリースノート ](https://experienceleague.adobe.com/docs/commerce-operations/release/versions.html) （*Adobe Commerce リリース情報*）。

- [Adobe Commerceの必要システム構成 ](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/system-requirements.html) （*Adobe Commerce インストールガイド*）。


## ストアアシストアプリの要件

店舗の集荷注文を管理するエンドツーエンドのプロセスは、モバイルデバイスにインストールされたストアアシストアプリを介して管理されます。 これらのデバイスは、小売業者または店舗従業員が個人のスマートフォンを使用して提供するもので、次の要件を満たす必要があります。

**オペレーティングシステムの最小要件**

- ANDROID6
- iOS12

**ハードウェアの最小要件**

- 1 GB RAM
- 600 MB の空きディスク容量

## ビジネス要件

ストアフルフィルメントソリューションを実装するには、ビジネスが次の最小条件を満たす必要があります。

- 米国に拠点を置く企業のみ

- B2C （Business to Consumer）小売業者、CPG （Consumer Packaged Goods）消費者に直接販売するメーカー（D2C）、または消費者または中小企業に直接販売するディストリビューター

- 1 つ以上の物理ストアまたは倉庫

- Inventory management for Adobe Commerce（MSI）による商品インベントリの管理

- 業者在庫のシンジケート機能

- ストアフルフィルメントソリューションをサポートするすべての場所で Wi-Fi を利用できます：最小インターネット速度 3 Mbps

- 店舗および倉庫の担当者は、勤務時間の間、個人または販売者から提供されたiOSまたはAndroidのモバイルデバイスにアクセスできます

- ストアフルフィルメントソリューションを使用して管理される製品には、SKU または UPC 製品コードのいずれかを含む製品属性が必要です
