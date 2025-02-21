---
title: ストアフルフィルメントサービスのオンボーディングの概要
description: オンボーディングフロー、システム要件、境界、制限に [!DNL Live Search] いて説明します。
role: Admin, Leader
level: Intermediate
feature: Shipping/Delivery, Install
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 0%

---

# ストアフルフィルメントのオンボーディングの概要

[!DNL Store Fulfillment for Adobe Commerce by Walmart Commerce Technologies] の基本を学ぶには、次のコンポーネントを設定、設定および有効にします。

- **ストアフルフィルメント拡張機能** – このサードパーティ製拡張機能をAdobe Commerce インスタンスにインストールして設定します。 インストール後、管理者からストアフルフィルメントソリューションを設定および管理して、Commerce ストアフロントの [!DNL buys online, pickup in store] （BOPI）シナリオをサポートできます。

  管理ビューの ![[!DNL Store Fulfillment Service] 設定 ](assets/store-fulfillment-admin-home.png)

- **ストアフルフィルメントアカウント** – 有効化プロセス中に、アカウントマネージャーがストアフルフィルメントアカウントを作成し、アカウント情報と資格情報を提供します。 これらの資格情報は、Adobe Commerceとストアフルフィルメントソリューションの間の接続を有効にするために必要です。

- **ストアアシストアプリ** - モバイルデバイスからの BOPI 注文を管理するためのエンドツーエンドのストアフルフィルメントワークフローを店員に提供します。 Store Associates は、iOSおよびAndroid™ デバイス向けのウォルマート [!DNL Store Assist] をダウンロードしてインストールできます。 アプリのオンボーディングプロセスは、ウォルマート Commerce テクノロジーズ クライアントセンターによって別のプロセスとして管理されます。 ただし [ 一部のアプリ設定 ](user-setup.md) は、Adobe Commerce管理者が行います。

  | ストアアシストアプリ – 概要ビュー | Store Assist App — モジュール表示 |
  |-------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------|
  | モバイルデバイスの ![[!DNL Store Assist App Getting Started] ビュー ](assets/store-assist-get-started-small.png) | モバイルデバイスで ![[!DNL Store Assist App Orders view] 動 ](assets/store-assist-orders-small.png) |

## プロビジョニング手順

- **新規登録[!DNL Store Fulfillment for Adobe Commerce by Walmart Commerce Technologies]**- [business.adobe.com](https://business.adobe.com/resources/store-fulfillment.html) の新規登録フォームに入力するか、Adobe Commerce担当営業または販売店にお問い合わせください。

- **Store Fulfillment のプロビジョニングリクエストの開始** - アカウントマネージャーから提供される取り込みフォームに入力して、プロビジョニングプロセスの開始に必要な情報を指定します。

- **ストアフルフィルメントアカウントの資格情報を取得する** – ストアフルフィルメントアカウントが作成されると、ストアフルフィルメントソリューションをAdobe Commerceと統合するために必要な資格情報を受け取ります。

- **[ソースコードをダウンロードして、拡張機能をインスト  [!DNL Store Fulfillment]  ルする](install.md)**

## オンボーディング手順

1. [Adobe Commerceのストアフルフィルメント拡張機能をインストールします ](install.md)。

1. 管理者で、[ ソリューションを有効にする ](enable-general.md) をクリックします。

1. [Adobe Commerce管理者からストアフルフィルメント拡張機能を設定します ](service-config-settings-overview.md)。

1. [ 提供されたストアフルフィルメントの資格情報を使用して  [!DNL Store Fulfillment]  サービスに接続します ](connect-set-up-service.md)。

1. [ ストアアシストアプリのユーザーと役割を作成します ](user-setup.md)。

1. [Walmart&#39;s [!DNL Store Assist]  アプリをお好みのデバイスにダウンロードしてください。 このアプリは、Apple アプリ（iOS）とGoogle Play（Android™）の両方のストアで利用 ](app-setup.md) きます。

正常にインストール、設定、オンボーディングを完了し、[!DNL Store Assist] アプリにアクセスできるようになったら、[ 注文の作成とテストを開始 ](test-and-deploy.md) できます。
