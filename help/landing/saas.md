---
title: Commerce サービスコネクタ
description: 実稼動およびサンドボックス API キーを使用して、Adobe CommerceまたはMagento Open Source インスタンスをサービスに統合する方法について説明します。
feature: Services, Saas
role: Admin, User
exl-id: 1aa6ba8b-be39-496e-b83d-a4a7db9f5dd8
badgePaas: label="PaaS のみ" type="Informative" url="https://experienceleague.adobe.com/ja/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce on Cloud プロジェクト（Adobeが管理する PaaS インフラストラクチャ）およびオンプレミスプロジェクトにのみ適用されます。"
source-git-commit: be1c739f3821a5f1e846b3026088e3a3ff45a60f
workflow-type: tm+mt
source-wordcount: '1420'
ht-degree: 0%

---

# [!DNL Commerce Services Connector]

Adobe CommerceとMagento Open Sourceの一部の機能は [!DNL Commerce Services] を利用し、SaaS （software as a service）としてデプロイされます。 これらのサービスを使用するには、実稼動およびサンドボックス API キーを使用して [!DNL Commerce] インスタンスを接続し、[configuration](#saas-configuration) でデータ領域を指定する必要があります。 接続はインスタンスごとに 1 回だけ設定する必要があります。

## 利用可能なサービス {#availableservices}

[!DNL Commerce Services Connector] からアクセスできる [!DNL Commerce] の機能は次のとおりです。

| サービス | 対象 |
| ---|--- |
| [[!DNL Product Recommendations]](/help/product-recommendations/overview.md) powered by Adobe Sensei | Adobe Commerce |
| [[!DNL Live Search]](/help/live-search/overview.md) powered by Adobe Sensei | Adobe Commerce |
| [[!DNL Payment Services]](/help/payment-services/overview.md) | Adobe CommerceとMagento Open Source |
| [[!DNL Site-Wide Analysis Tool]](https://experienceleague.adobe.com/ja/docs/commerce-operations/tools/site-wide-analysis-tool/intro) | Adobe Commerce |
| [[!DNL Catalog Service]](/help/catalog-service/overview.md) | Adobe Commerce |
| [[!DNL Data Connection]](/help/data-connection/overview.md) | Adobe Commerce |

## アーキテクチャ

大まかに言えば、[!DNL Commerce Services Connector] は次のコア要素で構成されています。

![Commerce サービス コネクタのアーキテクチャ](assets/saas-config-sync-workflow.png)

次のセクションでは、これらの各要素について詳しく説明します。

## 資格 情報 {#apikey}

実稼働およびサンドボックスの API キーは、[ ライセンス所有者 ](https://experienceleague.adobe.com/ja/docs/commerce-cloud-service/start/onboarding) の [!DNL Commerce] アカウントから生成されます。 Commerce アカウントは、一意の [!DNL Commerce] ID （MageID）で識別されます。 加盟店の組織のライセンス所有者は、アカウントが正常に動作している限り、製品レコメンデーションやライブ検索などのサービスの API キーを生成できます。

キーは、ライセンス所有者の代わりにプロジェクトや環境を管理するシステムインテグレーターまたは開発チームと、「必要な情報」ベースで共有できます。 ライセンス版所有者によって [!DNL Shared Access] を付与された開発者は、マーチャントの組織がアカウントの [!DNL Switch Accounts] ドロップダウンに存在する場合均等、自分の代わりにキーを生成することはできません。

さらに、ソリューションインテグレーターは [!DNL Commerce Services]を使用する権利もあります。 ソリューション インテグレーターの場合は、 [!DNL Commerce] パートナー コントラクトの署名者が API キーを生成する必要があります。

>[!NOTE]
>キー識別子 *実稼動* および *サンドボックス* は、環境 を参照しません。 各環境 (ローカル、開発環境、ステージング環境、実稼働環境など) に同じ API キーのセットを使用します。
>
>ライセンス版 所有者は通常、Adobe Systems Commerce アカウントの主要連絡先であり、クラウドインフラストラクチャープロジェクトの Adobe Systems Commerce のプロジェクト所有者と常に同じであるとは限りません。

### 実稼動およびサンドボックス API キーの生成 {#genapikey}

1. [!DNL Commerce] アカウント（[https://account.magento.com](https://account.magento.com/customer/account/login){:target="_blank"}）にログインします。

1. 「**Magento**」タブで、サイドバーの **API ポータル** を選択します。

1. _環境_ メニューから、「**実稼動**」または「**サンドボックス**」を選択します。

   >[!NOTE]
   >
   >*実稼動環境* および *サンドボックス* とは、データがAdobe SaaS バックエンドシステムに保存されるデータスペース環境を指します。 キーを使用するコマース環境ではありません。

1. _API キー_ セクションに名前を入力し、**新規追加** をクリックして、新しいキーをダウンロードするためのダイアログを開きます。

   ![秘密鍵無償体験版で試してみる](assets/download-api-private-key.png)

   >[!WARNING]
   >
   > このダイアログには、キーをコピーまたはダウンロードするする必要がある機会のみが表示されます。

1. 「 **無償体験版で試してみる** をクリックし、「 **キャンセル**」をクリックします。

1. 各環境(実稼働およびサンドボックス)について上記の手順を繰り返します。

   **API キー**&#x200B;セクションに API(公開)キーが表示されるようになりました。ライセンス版に関連付けられている環境またはインストールのいずれかで [SaaS プロジェクトを選択または作成する](#createsaasenv) 場合は、4 つのキーすべて (運用キーとサンドボックス キーの両方、公開+秘密キー) が必要になります。

## SaaS 設定 {#saasenv}

[!DNL Commerce] インスタンスは、 [!DNL Commerce Services] 適切な場所にデータを送信できるように、SaaS プロジェクトと SaaS データスペースを使用して構成する必要があります。 SaaS プロジェクトは、すべての SaaS データスペースをグループ化します。 SaaSデータスペースは、 [!DNL Commerce Services] が機能することを可能にするデータを収集およびストアするために使用されます。 このデータの一部は [!DNL Commerce] インスタンスからエクスポートされ、一部はストアフロントでの買い物客動作から収集される場合があります。 その後、そのデータはクラウドストレージを保護するために保持されます。

[!DNL Product Recommendations]の場合、SaaSデータスペースにはカタログデータと行動データが含まれています。[!DNL Commerce]構成で[!DNL Commerce]インスタンスを SaaS データ スペースに[選択](https://experienceleague.adobe.com/ja/docs/commerce-admin/config/services/saas)することでポイントできます。

>[!WARNING]
>
> **実稼動 SaaS データ領域** は、データの競合を避けるために、実稼動 [!DNL Commerce] インストールでのみ使用します。 そうしないと、テストデータで実稼動サイトデータが汚染され、デプロイメントの遅延が発生するリスクがあります。 例えば、実稼動製品のデータが、ステージング URL などのステージングデータと誤って上書きされる可能性があります。
> これが発生した場合は、[ サポートリクエストを送信 ](https://experienceleague.adobe.com/ja/docs/commerce-knowledge-base/kb/overview) して、データのクリーンアップをリクエストします。

### SaaS データ領域のプロビジョニング

すべてのAdobe Commerce マーチャントは、SaaS プロジェクトごとに 1 つの実稼動データスペースと 2 つのテストデータスペースにアクセスできます。

同じデータスペースを複数の環境で同時に使用しない限り、非実稼動環境でテストデータスペースを使用できます。 別の環境でテストデータ領域を使用するには、その環境でデータ領域を選択および設定する前に、データクリーンアップを実行します。

複数のステージング環境を使用する Adobe Commerce Cloud Pro プロジェクトの場合は、[ サポートリクエストを送信 ](https://experienceleague.adobe.com/home?lang=ja&support-tab=home#support) することで、ステージング環境ごとに追加のテストデータスペースをリクエストできます。 ただし、ステージング環境が 1 つのみで、追加のテストデータスペースが必要な場合は、次のオプションがあります。
- 追加のステージング環境をリクエストする場合は、カスタマーサクセスチームまたは担当のカスタマーサクセスマネージャーにお問い合わせください。
- [ サポートリクエストを送信 ](https://experienceleague.adobe.com/home?lang=ja&support-tab=home#support) して追加のテストデータスペースをリクエストし、追加のデータスペースに対するビジネス上の正当性を示します。 このリクエストは承認される場合があります。

Adobe支払いサービスを利用しているMagento Open Sourceのお客様は、追加のデータスペースをリクエストする場合もあります。 テストデータスペースをリクエストするには、[ サポートリクエスト ](https://experienceleague.adobe.com/home?lang=ja&support-tab=home#support) を送信する前に、支払いチームに追加のデータスペースに関する事前承認を問い合わせてください。

複数のクラウドプロジェクトまたはオンプレミス（実稼働/実稼働）インストールを所有しているお客様は、[ サポートリクエストを送信 ](https://experienceleague.adobe.com/home?lang=ja&support-tab=home#support) することで、各プロジェクトまたはインスタンスに対して追加の実稼働およびテスト用データスペースをリクエストすることもできます。

### SaaS プロジェクトの選択または作成 {#createsaasenv}

SaaS プロジェクトを選択または作成するには、ストアの [!DNL Commerce] ライセンス所有者に [!DNL Commerce] API キーをリクエストします。

>[!NOTE]
>
> [!DNL Commerce] の設定に **[!UICONTROL Commerce Services Connector]** のセクションが表示されない場合は、目的の [[!DNL Commerce]  サービス ](#availableservices) に [!DNL Commerce] モジュールをインストールする必要があります。

1. _管理者_ サイドバーで、**システム**/サービス/**Commerce サービスコネクタ** に移動します。

   [!DNL Commerce] の設定に **[!UICONTROL Commerce Services Connector]** のセクションが表示されない場合は、目的の [[!DNL Commerce]  サービス ](#availableservices) に [!DNL Commerce] モジュールをインストールします。 また、`magento/module-services-id` パッケージがインストールされていることを確認します。

1. _[!UICONTROL Sandbox API Keys]_&#x200B;セクションと&#x200B;_[!UICONTROL Production API Keys]_ セクションに、キー値を貼り付けます。

   - 秘密鍵は、鍵の先頭に `----BEGIN PRIVATE KEY---`、鍵の末尾に `----END PRIVATE KEY----` を含める必要があります。
   - 実際のキーのコピーがない場合は、アカウント所有者に問い合わせて、値を設定に接続します。

   >[!WARNING]
   >
   > データベースのバックアップまたはスナップショットに対してクエリを実行し、その値を設定に貼り付けることでキー値を追加した場合、追加の暗号化レイヤーが適用され、キーは機能しません。

1. **保存** をクリックします。

キーに関連付けられている SaaS プロジェクトは、[**SaaS Identifier**] セクションの [**プロジェクト**] フィールドに表示されます。

1. SaaS プロジェクトが存在しない場合は、[**プロジェクトの作成**] をクリックします。 次に、**プロジェクト** フィールドに、SaaS プロジェクトの名前を入力します。

>[!NOTE]
>
>混乱を避けるために、*Live Search*、*Product Recommendations*、*Data Connection* など、特定のCommerce サービスをプロジェクトの名前として使用しないでください。  ライセンスが複数の SaaS プロジェクト用にプロビジョニングされていない限り、複数のサービスに同じ SaaS プロジェクトを使用できます。

1. [!DNL Commerce] ストアの現在の設定に使用する **データスペース** を選択します。

>[!NOTE]
>
>Commerce サービスと統合するための個別のインスタンスがある場合は、[ サポートチケットを送信 ](https://experienceleague.adobe.com/ja/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#submit-ticket) して、追加のインスタンスごとに新しい SaaS プロジェクトをリクエストします。 サポートが SaaS プロジェクトを作成したら、同じ API キーを使用してインスタンスのCommerce Services 統合を設定し、データ空間用の新しい SaaS プロジェクトを選択します。

>[!WARNING]
>
> マイアカウントの API ポータルセクションで新しいキーを生成した場合、直ちに管理設定の API キーを更新します。 新しいキーを生成し、管理者でそれらを更新しない場合、SaaS 拡張機能は機能しなくなり、貴重なデータが失われます。

SaaS プロジェクトまたはデータ領域の名前を変更するには、どちらかの横にある **名前の変更** をクリックします。 名前を変更しても、サービスには影響しません。名前は、プロジェクトとデータ スペースを識別および区別するのに役立つラベルにすぎないからです。

## IMS 組織 (オプション) {#organizationid}

Adobe Commerce インスタンスをAdobe Experience Platformに接続するには、Adobe IDを使用してAdobe アカウントにログインします。 サインインすると、Adobe Systemsアカウントに関連付けられている IMS 組織がこのセクションに表示されます。

## SaaS データのエクスポート

[!DNL Commerce] インスタンスが [!DNL Commerce Services] に正常に接続されると、SaaS データ書き出しプロセスによって、Commerce データが [!DNL Commerce] サーバーから [!DNL Commerce SaaS Services] に書き出され、接続されたCommerce Services に同期できるようになります。 管理者では、[ データ管理ダッシュボード ](https://experienceleague.adobe.com/ja/docs/commerce-admin/systems/data-transfer/data-dashboard) を使用して、同期ステータスを確認できます。 詳細については、「[SaaS データ書き出しガイド ](../data-export/overview.md)」を参照してください。
