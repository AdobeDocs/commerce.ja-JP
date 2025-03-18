---
title: Adobe Commerce as a Cloud Serviceの概要
description: Adobe Commerce as a Cloud Serviceの使用を開始する方法について説明します。
role: Admin, Developer, User
source-git-commit: 19c49b2b9d630898353addd778e062d3208505c1
workflow-type: tm+mt
source-wordcount: '595'
ht-degree: 0%

---


# はじめに

Adobe Commerce as a Cloud Serviceでは、ほとんどの設定が標準で提供されています。 いくつかの基本的な設定プロセスを完了すると、ストアはすぐに立ち上がって実行されます。 このガイドでは、インスタンスの作成と操作について説明します。

以下のタブをクリックして、次のユーザータイプに関するワークフローの概要を確認してください。

* 管理者
* 商人
* 開発者

>[!BEGINTABS]

>[!TAB  管理者とマーチャントワークフロー ]

次の図は、管理者とマーチャントがAdobe Commerce as a Cloud Service インスタンスにアクセスして管理する方法の概要を示しています。 管理者ワークフローについて詳しくは、[Adobe Admin Console ガイド ](https://helpx.adobe.com/enterprise/admin-guide.html) を参照してください。

![Adobe Commerce as a Cloud Serviceのマーチャントフロー図 ](./assets/merchant-flow.svg){zoomable="yes"}

>[!TAB  開発者ワークフロー ]

次の図は、App Builderを使用してAdobe Commerce as a Cloud Serviceの統合を開発する方法の概要を示しています。 詳しくは、[API ドキュメント ](https://developer.adobe.com/commerce/services/cloud/) を参照してください。

![Adobe Commerce as a Cloud Service開発者のフロー図 ](./assets/developer-flow.svg){zoomable="yes"}

>[!ENDTABS]

## インスタンスの作成

Adobe Commerce as a Cloud Service インスタンスは、信用ベースのシステムを使用します。 複数のインスタンスを作成できますが、各インスタンスには相対的なクレジット量が必要です。 最初に付与されるクレジットの量は、サブスクリプションによって異なります。

1. [Adobe Experience Cloud](https://experience-stage.adobe.com/) アカウントにログインします。

1. 「[!UICONTROL Quick access]」で「[!UICONTROL **Commerce**]」をクリックして [!UICONTROL Commerce Cloud Manager] を開きます。

   [!UICONTROL Commerce Cloud Manager] に、お客様のAdobe IMS組織で使用可能なAdobe Commerce as a Cloud Service インスタンスのリストが表示されます。

1. 画面の右上隅にある「[!UICONTROL **インスタンスを追加**]」をクリックします。

   ![ インスタンスを作成 ](./assets/create-instance.png){width="50%" align="center" zoomable="yes"}

1. 「[!UICONTROL **Commerceas a Cloud Service**]」を選択します。

1. インスタンスの **名前** と **説明** を入力します。

1. インスタンスをホストする地域を選択します。

   >[!NOTE]
   >
   >インスタンスを作成すると、地域を変更できなくなります。

1. インスタンスの [!UICONTROL **環境タイプ**] を選択します。 次のいずれかのオプションを選択できます。

   * [!UICONTROL **サンドボックス**] - デザインおよびテスト目的に最適です。 サンドボックス環境を使用して、Adobe Commerce as a Cloud Serviceのジャーニーを開始する必要があります。
   * [!UICONTROL **実稼動**] - ライブストアおよびお客様向けのサイト用。

   >[!NOTE]
   >
   >サンドボックスインスタンスは、現在、北米リージョンに制限されています。

1. _（オプション）_ テストや学習の目的でサンプルの商品データを含める場合は、{ テストデータ **]ドロップダウンから[!UICONTROL ** 2 **]Adobe ストア } を選択します。[!UICONTROL **

   このオプションはスキップできますが、その場合、ストアフロントに製品はありません。 ストアフロントの完全なエクスペリエンスを表示するには、[ カタログを読み込む ](#import-your-catalog) 必要があります。

1. [!UICONTROL **インスタンスを追加**] をクリックします。

## インスタンスへのアクセス

インスタンスを作成したら、[!UICONTROL Commerce Cloud Manager] からアクセスできます。

1. [Adobe Experience Cloud](https://experience.adobe.com/) アカウントにログインします。

1. 「[!UICONTROL Quick access]」で「[!UICONTROL **Commerce**]」をクリックして [!UICONTROL Commerce Cloud Manager] を開きます。

   [!UICONTROL Commerce Cloud Manager] に、Adobe IMS組織で使用可能なインスタンスのリストが表示されます。

1. インスタンスの [!UICONTROL Commerce Admin] を開くには、インスタンス名をクリックします。

>[!TIP]
>
>REST およびGraphQL エンドポイント、管理 URL など、インスタンスに関する情報を表示するには、インスタンス名の横にある情報アイコンをクリックします。

## カタログの読み込み

デフォルトでは、Adobe Commerce as a Cloud Service インスタンスには商品データは含まれていません。 独自のカタログを読み込む前に、テストや学習のためにインスタンスを作成する際に、サンプルの製品データを含めるオプションがあります。

カタログをAdobe Commerce as a Cloud Serviceに読み込むには、次の 2 つの方法があります。

* [**Commerce管理者**](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/import/data-import) – 数回クリックするだけでカタログデータを読み込むことができる、使いやすいインターフェイスです。
* [**JSON API の読み込み**](https://developer.adobe.com/commerce/webapi/rest/modules/import/#import-json-api) - カタログデータをプログラムで読み込むことができる REST API。

<!-- TODO

- Add guidance about how to choose which method to use
- Add guidance for new vs existing customers (cross-reference OR and _include file for migration content)

-->

## ストアフロントの設定

インスタンスを作成したので、Edge Delivery Servicesを使用したCommerce Storefront の [ 設定 ](storefront.md) を続行する準備が整いました。
