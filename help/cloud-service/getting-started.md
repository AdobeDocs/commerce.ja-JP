---
title: 入門  [!DNL Adobe Commerce as a Cloud Service]
description: ' [!DNL Adobe Commerce as a Cloud Service] の使用を開始する方法について説明します。'
role: Admin, Developer, User
exl-id: 58d98b9e-b41d-44db-9666-c924a5b005b3
badgeSaas: label="SaaS のみ" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud ServiceおよびAdobe Commerce Optimizer プロジェクトにのみ適用されます（Adobeで管理される SaaS インフラストラクチャ）。"
source-git-commit: 061b976872fae614cf1fb3db5aaabd9ffdc5e0f9
workflow-type: tm+mt
source-wordcount: '1264'
ht-degree: 0%

---

# はじめに

[!DNL Adobe Commerce as a Cloud Service] は、ほとんどの設定を標準で提供しています。 いくつかの基本的な設定プロセスを完了すると、ストアはすぐに立ち上がって実行されます。 このガイドでは、インスタンスの作成と操作について説明します。 また、このガイドは、チームが [!DNL Adobe Commerce as a Cloud Service] への適切なアクセス権と、開始に必要なツールを確実に持つことで、組織を成功に向けて設定する際にも役立ちます。

[!DNL Adobe Commerce as a Cloud Service] は、デジタルコマースエクスペリエンスを配信するための柔軟性、拡張性、効率を提供するクラウドネイティブなコマースプラットフォームです。 この SaaS 製品は、完全に管理されたバージョンなしのプラットフォームであり、手動の介入を必要とせずにシームレスなアップグレードを実現します。

## 主要コンポーネント

[!DNL Adobe Commerce as a Cloud Service] は、次のコンポーネントで構成されます。

* **[Adobe Experience Cloud](https://experience.adobe.com/)** - [!DNL Adobe Commerce]experience.adobe.com[ にあるすべての ](https://experience.adobe.com/) 製品への主要なエントリポイント
   * [!UICONTROL **クイックアクセス**] の下の [!UICONTROL **0&rbrace;Commerce&rbrace; をクリックして、Commerce Cloud Manager を開きます**]
* **[Commerce Cloud Manager](https://experience.adobe.com/#/commerce/cloud-service)** - インスタンスの作成と管理、API URL へのアクセスおよびCommerce管理者
* **[Adobe Admin Console](https://adminconsole.adobe.com/)** - ユーザーとロールを管理します
* **Commerce管理者** – 商品、注文、顧客およびストア設定を管理します
* **[Edge Delivery Servicesを活用したストアフロント](./storefront.md)** - コンポーザブルで高性能なシステムを使用して、マーチャントやデベロッパー向けに優れたスピード、SEO、ユーザーエクスペリエンスを提供する、顧客向けのストアフロントを作成およびカスタマイズします
* **[Adobe Developer App Builder](https://developer.adobe.com/app-builder/)** - [integration starter kit](https://developer.adobe.com/commerce/extensibility/starter-kit/integration/) や [API メッシュ ](https://developer.adobe.com/graphql-mesh-gateway/) などの拡張ツールと共に、App Builderを使用してカスタム統合を構築します

## 設定と管理

[!DNL Adobe Commerce as a Cloud Service] の設定プロセスの一環として、システム管理者、マーチャント、開発者は、クラウドリソースのプロビジョニングや、ユーザーを責任に基づいて適切な役割に割り当てるなど、組織のアクセスやリソースを設定します。

### 設定と管理のワークフロー

組み合わせたグループとして、システム管理者、マーチャントおよび開発者は、Commerce インスタンスを起動して実行するために次の基本的な手順に従う必要があります。

1. **すべてのユーザー**: [ インスタンスを作成 ](#create-an-instance)
1. **システム管理者**:[ ユーザーの追加と役割の割り当て ](user-management.md#add-users-and-admins)
1. **マーチャント**:[Commerce管理にアクセス ](#access-an-instance) て [ カタログを読み込みます ](#import-your-catalog)
1. **開発者**:[ ストアフロントを設定 ](storefront.md) し、[ 開発者プラットフォーム ](overview.md#developer-platform) を参照してください

#### AEM Assetsと製品ビジュアルのワークフロー

[!DNL Adobe Experience Manager Assets] または [!DNL Product Visuals powered by AEM Assets] を [!DNL Adobe Commerce as a Cloud Service] と統合するには、次の手順が必要です。

1. **システム管理者**:[ 「AEM Assetsと Product Visuals」製品プロファイルにユーザーを追加 ](user-management.md#add-a-user-to-aem-assets-or-product-visuals)
1. **開発者**:[AEM Assetsと製品ビジュアルの統合 ](../aem-assets-integration/overview.md)
1. **マーチャント**:[AEM Assetsと製品のビジュアルにアクセス ](./user-management.md#access-the-experience-manager-interface)

### 役割ベースの設定と管理タスク

以下のタブを選択して、対応する役割のワークフローのグラフィックの概要を確認します。

>[!BEGINTABS]

>[!TAB  システム管理者とマーチャントワークフロー ]

次の図は、システム管理者とマーチャントが [!DNL Adobe Commerce as a Cloud Service] インスタンスにアクセスして管理する方法の概要を示しています。 管理者ワークフローについて詳しくは、[Adobe Admin Console ガイド ](https://helpx.adobe.com/enterprise/admin-guide.html) を参照してください。

商 ![[!DNL Adobe Commerce as a Cloud Service] フロー図 ](./assets/merchant-flow.svg){zoomable="yes"}

>[!TAB  開発者ワークフロー ]

次の図は、App Builderを使用して、開発者向けの統合を作成する方法の概要 [!DNL Adobe Commerce as a Cloud Service] 示しています。 詳しくは、[API ドキュメント ](https://developer.adobe.com/commerce/webapi/rest/) を参照してください。

開発者 ![[!DNL Adobe Commerce as a Cloud Service] フロー図 ](./assets/developer-flow.svg){zoomable="yes"}

>[!ENDTABS]

役割を選択してリソースを検索し、設定プロセスを開始します。

>[!BEGINTABS]

>[!TAB  システム管理者 ]

あなたは、システム管理者として、組織の設定とユーザーアクセスの管理を担当します。

| タスク | 説明 | Resource |
|------|-------------|----------|
| プラットフォームについて | Adobe Commerce as a Cloud Serviceのアーキテクチャとメリットについて説明します | [ 概要 ](overview.md) |
| 機能の比較 | Cloud Serviceと他のAdobe Commerce製品の違いを理解する | [ 機能の比較 ](feature-comparison.md) |
| インスタンスの作成 | サンドボックスと実稼動環境のプロビジョニング | [ インスタンスの作成 ](#create-an-instance) |
| User Management の設定 | ユーザーの追加、役割の割り当ておよび権限の管理 | [ ユーザー管理 ](user-management.md) |
| AEM Assetsと製品ビジュアルの設定（オプション） | ユーザーの追加、役割の割り当ておよび権限の管理 | [ ユーザー管理 ](user-management.md#add-a-user-to-aem-assets-or-product-visuals) |

>[!TAB  商人 ]

マーチャントは、製品、注文、ストアフロントコンテンツの管理に専念します。

| タスク | 説明 | Resource |
|------|-------------|----------|
| インスタンスへのアクセス | Commerce管理者にログインしてストアを管理する | [ インスタンスへのアクセス ](#access-an-instance) |
| ユースケースの調査 | 実用的なビジネスシナリオとワークフローについて学ぶ | [ ユースケース ](./use-cases.md) |
| Import catalog | 製品データをプラットフォームに読み込む方法を説明します | [ カタログを読み込む ](#import-your-catalog) |
| AEM Assetsと製品ビジュアルへのアクセス（オプション） | Experience Manager にアクセスして、AEM Assetsと製品ビジュアルの使用を開始する | [Experience Manger インターフェイスへのアクセス ](./user-management.md#access-the-experience-manager-interface) |


>[!TAB  開発者 ]

開発者は、カスタム統合を構築し、プラットフォーム機能を拡張する方法を知っている必要があります。

| タスク | 説明 | Resource |
|------|-------------|----------|
| アーキテクチャについて | プラットフォームの拡張性と API について説明します | [ 概要 – 開発者プラットフォーム ](overview.md#developer-platform) |
| 開発環境の設定 | 開発およびテスト用のサンドボックスインスタンスを作成 | [ インスタンスの作成 ](#create-an-instance) |
| ストアフロントを構築 | Commerce ストアフロントのセットアップおよびカスタマイズ方法について説明します | [ ストアフロントの設定 ](./storefront.md) |
| ストアフロントの設定 | ストアフロントの設定方法について学ぶ | [ ストアフロントの設定 ](./storefront.md) |
| 統合オプションの調査 | App Builder、API メッシュ、およびアクセス権のあるその他の拡張ツールについて説明します | [ 概要 – 開発者プラットフォーム ](overview.md#developer-platform) |
| AEM Assetsと製品ビジュアルの統合（オプション） | AEM Assetsと製品ビジュアルをAdobe Commerceと統合する方法を学ぶ | [AEM Assetsの統合 ](../aem-assets-integration/overview.md) |

>[!ENDTABS]

### 次の手順

役割固有の設定タスクを完了した後：

* **システム管理者**: [ 共有責任 ](shared-responsibility.md) ガイドラインの確認
* **マーチャント**：一般的なビジネスシナリオについて [ ユースケース ](use-cases.md) を調べます
* **Developers**: [Adobe Commerce開発者向けドキュメントをご覧ください ](https://developer.adobe.com/commerce/docs)

## Adobe Commerce as a Cloud Serviceの基本

次の節では、Commerce インスタンスを起動して実行するために必要な基本的なプロセスについて説明します。

### インスタンスの作成

>[!NOTE]
>
>インスタンスを作成する前に、組織の製品管理者またはシステム管理者が、[!DNL Adobe Commerce as a Cloud Service] 製品のユーザーとしてユーザーを追加する必要があります。 詳しくは、[ ユーザーと管理者の追加 ](./user-management.md#add-users-and-admins) を参照してください。

[!DNL Adobe Commerce as a Cloud Service] インスタンスでは、クレジットベースのシステムを使用します。 複数のインスタンスを作成できますが、各インスタンスには使用可能なクレジットが必要です。 最初に付与されるクレジットの数は、サブスクリプションによって異なります。

1. [Adobe Experience Cloud](https://experience.adobe.com/) アカウントにログインします。

1. 「[!UICONTROL Quick access]」で「[!UICONTROL **Commerce**]」をクリックして [!UICONTROL Commerce Cloud Manager] を開きます。

   [!UICONTROL Commerce Cloud Manager] に、Adobe IMS組織で使用可能な [!DNL Adobe Commerce as a Cloud Service] インスタンスのリストが表示されます。

1. 画面の右上隅にある「[!UICONTROL **インスタンスを追加**]」をクリックします。

   ![ インスタンスを作成 ](./assets/create-instance.png){width="50%" align="center" zoomable="yes"}

1. 「[!UICONTROL **Commerceas a Cloud Service**]」を選択します。

1. インスタンスの **名前** と **説明** を入力します。

1. インスタンスの [!UICONTROL **環境タイプ**] を選択します。 次のいずれかのオプションを選択できます。

   * [!UICONTROL **サンドボックス**] - デザインおよびテスト目的に最適です。 サンドボックス環境を使用して、[!DNL Adobe Commerce as a Cloud Service] ジャーニーを開始する必要があります。
   * [!UICONTROL **実稼動**] - ライブストアおよびお客様向けのサイト用。

   >[!NOTE]
   >
   >* サンドボックスインスタンスは、北米リージョンに制限されています。
   >* サンプルデータをインストールするオプションは現在使用できません。

1. インスタンスをホストする地域を選択します。

   >[!NOTE]
   >
   >インスタンスを作成すると、地域を変更できなくなります。

1. [!UICONTROL **インスタンスを追加**] をクリックします。

### インスタンスへのアクセス

インスタンスを作成したら、[!UICONTROL Commerce Cloud Manager] からアクセスできます。

1. [Adobe Experience Cloud](https://experience.adobe.com/) アカウントにログインします。

1. 「[!UICONTROL Quick access]」で「[!UICONTROL **Commerce**]」をクリックして [!UICONTROL Commerce Cloud Manager] を開きます。

   [!UICONTROL Commerce Cloud Manager] に、Adobe IMS組織で使用可能なインスタンスのリストが表示されます。

1. インスタンスの [!UICONTROL Commerce Admin] を開くには、インスタンス名をクリックします。

>[!TIP]
>
>REST およびGraphQL エンドポイント、管理 URL など、インスタンスに関する情報を表示するには、インスタンス名の横にある情報アイコンをクリックします。

管理者とエンドポイントのベース URL は、次のパターンを使用して、地域と環境によって異なります。

* Admin
   * 北米の実稼動管理者：`https://na1.admin.commerce.adobe.com`
   * 北米サンドボックス管理者：`https://na1-sandbox.admin.commerce.adobe.com`
   * ヨーロッパ実稼動管理者：`https://eu1.admin.commerce.adobe.com`
* REST とGraphQL
   * 北米生産GraphQL:`https://na1.api.commerce.adobe.com`
   * 北米サンドボックスGraphQL:`https://na1-sandbox.api.commerce.adobe.com`
   * ヨーロッパの実稼動GraphQL: `https://eu1.api.commerce.adobe.com`

### カタログの読み込み

デフォルトでは、[!DNL Adobe Commerce as a Cloud Service] インスタンスには製品データは含まれていません。 独自のカタログを読み込む前に、テストや学習のためにインスタンスを作成する際に、サンプルの製品データを含めるオプションがあります。

カタログを [!DNL Adobe Commerce as a Cloud Service] に読み込む方法は 2 つあります。

* [**Commerce管理者**](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/import/data-import) – 数回クリックするだけでカタログデータを読み込むことができる、使いやすいインターフェイスです。
* [**JSON API の読み込み**](https://developer.adobe.com/commerce/webapi/rest/modules/import/#import-json-api) - カタログデータをプログラムで読み込むことができる REST API。

### ストアフロントの設定

インスタンスを作成したので、Edge Delivery Servicesを使用して [ ストアフロントを設定 ](storefront.md) する準備が整いました。

## その他のリソース

* [リリースノート](release-notes.md)
* [移行ガイド](migration/overview.md)
* [Commerce ストアフロントのドキュメント ](https://experienceleague.adobe.com/developer/commerce/storefront/)
