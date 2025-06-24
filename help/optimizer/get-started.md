---
title: 基本を学ぶ
description: ' [!DNL Adobe Commerce Optimizer] の使用を開始する方法について説明します。'
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="SaaS のみ" type="Positive" url="https://experienceleague.adobe.com/ja/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud ServiceおよびAdobe Commerce Optimizer プロジェクトにのみ適用されます（Adobeで管理される SaaS インフラストラクチャ）。"
source-git-commit: f49a86b8793e2d91413acfbc0b922cb94db67362
workflow-type: tm+mt
source-wordcount: '753'
ht-degree: 0%

---

# はじめに

この記事では、[!DNL Adobe Commerce Optimizer] の最新情報を取得する方法について説明します。 このガイドではマーチャンダイザーと管理者の役割に重点を置いていますが、開発者が実行する簡単な大まかなタスクも含まれています。 開発者固有のコンテンツについて詳しくは、[ 開発者ドキュメント ](https://developer-stage.adobe.com/commerce/services/composable-catalog/) を参照してください。

## あなたの役割は何ですか。

[!DNL Adobe Commerce Optimizer] の正常な設定には、通常、次のチームメンバーが関与します。

- 管理者
- 開発者
- マーチャンダイザー

各チームメンバーには、次の表に示すように、独自の役割と責務があります。

| 役割 | タスク |
|---|---|
| 管理者 | Admin Consoleを使用して、管理者、ユーザーグループ、ユーザーおよび開発者を作成し&#x200B;ます。 |
|  | Commerce Cloud Manager で新しい [!DNL Adobe Commerce Optimizer] インスタンスを作成し&#x200B;す。 |
|  | ポリシーとカタログ表示を設定します。 |
| 開発者 | Developer Consoleを使用してプロジェクトを作成し、デベロッパー API アクセスを許可し、必要なアプリケーションとカスタマイズをインストールします。 |
|  | API Mesh とApp Builderを使用して、バックオフィスシステム（買い物かご、チェックアウト）に&#x200B;接続します。 |
|  | マーチャンダイジングサービスデータ取り込み API を使用して、既存のコマースソリューションからカタログデータを取り込む&#x200B; |
|  | ストアフロントの設定 |
| マーチャンダイザー | 製品の検出を設定&#x200B;します。 |
|  | 製品レコメンデーションを設定します。 |

各役割は、[!DNL Adobe Commerce Optimizer] 環境のオンボーディングと立ち上げの成功に不可欠な役割を果たします。 次の図は、組織の各役割の開始から終了までの高レベルのワークフローを示しています。

![ ワークフローの概要 ](./assets/high-level-workflow.png){zoomable="yes"}

### 管理者

管理者は、インスタンスの設定、ユーザー、グループおよび組織の使用権限の管理を担当します。

- **[Adobe Admin Consoleへのアクセス ](https://helpx.adobe.com/jp/enterprise/admin-guide.html)** - Adobeの使用権限を組織全体で管理します。 自分または組織の製品管理者またはシステム管理者が [!DNL Adobe Commerce Optimizer] 製品にユーザーを追加する方法については、[ ユーザー管理 ](./user-management.md) を参照してください。

- **インスタンスを作成** - インスタンス [!DNL Adobe Commerce Optimizer]、クレジットベースのシステムを使用します。 複数のサンドボックスインスタンスと実稼動インスタンスを作成できます。各インスタンスには、対応する 1 つのクレジットが必要です。 最初に付与されるクレジットの量は、サブスクリプションによって異なります。 [学習を増やす](#create-an-instance)。

- **インスタンスへのアクセス** - インスタンスを作成したら、[!UICONTROL Commerce Cloud Manager] からアクセスできます。 [学習を増やす](#access-an-instance)。

- **カタログビューとポリシーの設定** - [ カタログビューとポリシーを定義 ](./setup/catalog-view.md) する方法について説明します。 カタログには製品データが含まれているだけでなく、ビジネス構造を定義するのにも役立ちます。

### 開発者

開発者は、プロジェクトと資格情報の作成、拡張機能のインストール、カタログデータの取り込み、一般的な Platform アーキテクチャタスクの実行を行います。 開発者固有のコンテンツについて詳しくは、[ 開発者ドキュメント ](https://developer-stage.adobe.com/commerce/services/composable-catalog/) を参照してください。

- **Developer Consoleへのアクセス** - [Developer Console](https://developer.adobe.com/developer-console/docs/guides/getting-started) にアクセスして [!DNL Adobe Commerce Optimizer] 用プロジェクトを作成し、アクセストークンを生成し、必要なアプリケーションとカスタマイズをインストールします。

- **カタログデータの取り込み** - カタログデータを [!DNL Adobe Commerce Optimizer] に読み込む方法については、[Data ingestion API](https://developer-stage.adobe.com/commerce/services/composable-catalog/data-ingestion/using-the-api/) ドキュメントを参照してください。

  取り込まれたカタログデータが [ データ同期 ](./setup/data-sync.md) ページに表示されます。

- **ストアフロントの設定** - ストアフロントを設定する前に、まずインスタンスを作成する必要があります。これは、通常、組織の [ 管理者 ](#administrator) が実行するタスクです。 インスタンスを作成したら、Edge Delivery Servicesを使用したCommerce ストアフロントの [ 設定 ](./storefront.md) を続行する準備が整います。

### マーチャンダイザー

マーチャンダイザーは、買い物客データと分析を使用して、ストアフロントでの製品の配置、価格、プロモーションに関する戦略的な決定を行うと同時に、製品の検出とレコメンデーションを通じてショッピングエクスペリエンスを最適化します。

- **製品検出とレコメンデーションの設定** – 製品検出とレコメンデーションを通じて、買い物客に [ パーソナライズされたエクスペリエンスの作成 ](./merchandising/overview.md) を行う方法を説明します。

## インスタンスの作成

1. [Adobe Experience Cloud](https://experience.adobe.com/) アカウントにログインします。

1. 「[!UICONTROL Quick access]」で「[!UICONTROL **Commerce**]」をクリックして [!UICONTROL Commerce Cloud Manager] を開きます。

   [!UICONTROL Commerce Cloud Manager] には、Adobe IMS組織で使用可能な [!DNL Adobe Commerce] インスタンスのリストが表示されます。これには、[!DNL Adobe Commerce Optimizer] 用と [!DNL Adobe Commerce as a Cloud Service] 用にプロビジョニングされた両方のインスタンスが含まれます。

1. 画面の右上隅にある「[!UICONTROL **インスタンスを追加**]」をクリックします。

   ![ インスタンスを作成 ](./assets/create-aco-instance.png){width="100%" align="center" zoomable="yes"}

1. 「[!UICONTROL **Commerce Optimizer**]」を選択します。

1. インスタンスの **名前** と **説明** を入力します。

1. インスタンスをホストする地域を選択します。

   >[!NOTE]
   >
   >インスタンスを作成した後は、領域を変更できません。

1. インスタンスに対して、次のいずれかの [!UICONTROL **環境タイプ**] を選択します。

   - [!UICONTROL **サンドボックス**] - デザインおよびテスト目的に最適です。 サンドボックス環境を使用して、[!DNL Adobe Commerce Optimizer] ジャーニーを開始する必要があります。
   - [!UICONTROL **実稼動**] - ライブストアおよびお客様向けのサイト用。

   >[!NOTE]
   >
   >サンドボックスインスタンスは、現在、北米リージョンに制限されています。

1. [!UICONTROL **インスタンスを追加**] をクリックします。

   これで、Cloud Managerで新しいインスタンスを使用できるようになります。

1. GraphQLおよびカタログサービスエンドポイント、Adobe Commerce Optimizer アプリケーションにアクセスするための URL、インスタンス ID （テナント ID）など、インスタンスの詳細を表示するには、インスタンス名の横にある「情報」アイコンをクリックします。

   ![ インスタンスを作成 ](./assets/aco-instance-details.png){width="100%" align="center" zoomable="yes"}

## インスタンスへのアクセス

1. [Adobe Experience Cloud](https://experience.adobe.com/) アカウントにログインします。

1. 「[!UICONTROL Quick access]」で「[!UICONTROL **Commerce**]」をクリックして [!UICONTROL Commerce Cloud Manager] を開きます。

   [!UICONTROL Commerce Cloud Manager] に、Adobe IMS組織で使用可能なインスタンスのリストが表示されます。

1. インスタンスに関連付けられている [!UICONTROL Commerce Optimizer] アプリケーションを開くには、インスタンス名をクリックします。


