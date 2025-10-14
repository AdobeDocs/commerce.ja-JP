---
title: Commerce サービスコネクタ
description: 実稼動およびサンドボックス API キーを使用して、Adobe CommerceまたはMagento Open Source インスタンスをサービスに統合する方法について説明します。
feature: Services, Saas
role: Admin, User
exl-id: 1aa6ba8b-be39-496e-b83d-a4a7db9f5dd8
badgePaas: label="PaaS のみ" type="Informative" url="https://experienceleague.adobe.com/ja/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce on Cloud プロジェクト（Adobeが管理する PaaS インフラストラクチャ）およびオンプレミスプロジェクトにのみ適用されます。"
source-git-commit: d7cf4898d5f44ab73017eb0a16b10856f0c4fc75
workflow-type: tm+mt
source-wordcount: '1486'
ht-degree: 0%

---

# [!DNL Commerce Services Connector]

Adobe CommerceとMagento Open Sourceの一部の機能は [!DNL Commerce Services] を利用し、SaaS （software as a service）としてデプロイされます。 これらのサービスを使用するには、実稼動およびサンドボックス API キーを使用して [!DNL Commerce] インスタンスを接続し、[configuration](#saas-configuration) でデータ領域を指定する必要があります。 接続はインスタンスごとに 1 回だけ設定する必要があります。

## 利用可能なサービス {#availableservices}

[!DNL Commerce] からアクセスできる [!DNL Commerce Services Connector] の機能は次のとおりです。

| サービス | 対象 |
| ---|--- |
| [[!DNL Product Recommendations]](/help/product-recommendations/overview.md) powered by Adobe Sensei | Adobe Commerce |
| [[!DNL Live Search]](/help/live-search/overview.md) powered by Adobe Sensei | Adobe Commerce |
| [[!DNL Payment Services]](/help/payment-services/guide-overview.md) | Adobe CommerceとMagento Open Source |
| [[!DNL Catalog Service]](/help/catalog-service/overview.md) | Adobe Commerce |
| [[!DNL Data Connection]](/help/data-connection/overview.md) | Adobe Commerce |

## アーキテクチャ

大まかに言えば、[!DNL Commerce Services Connector] は次のコア要素で構成されています。

![Commerce サービスコネクタのアーキテクチャ &#x200B;](assets/saas-config-sync-workflow.png)

次のセクションでは、これらの各要素について詳しく説明します。

## 資格情報 {#apikey}

実稼働およびサンドボックスの API キーは、[!DNL Commerce] ライセンス所有者 [&#x200B; の &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-cloud-service/start/onboarding) アカウントから生成されます。 Commerce アカウントは、一意の [!DNL Commerce] ID （MageID）で識別されます。 加盟店の組織のライセンス所有者は、アカウントが正常に動作している限り、製品レコメンデーションやライブ検索などのサービスの API キーを生成できます。

キーは、ライセンス所有者の代わりにプロジェクトや環境を管理するシステムインテグレーターまたは開発チームと、「必要な情報」ベースで共有できます。 ライセンス所有者から [!DNL Shared Access] を付与された開発者は、マーチャントの組織がアカウントの [!DNL Switch Accounts] ドロップダウンに存在する場合でも、自分の代わりにキーを生成することはできません。

さらに、ソリューションインテグレーターは [!DNL Commerce Services] も使用できます。 ソリューションインテグレーターの場合は、[!DNL Commerce] パートナー契約の署名者が API キーを生成する必要があります。

>[!NOTE]
>キー識別子 *実稼動* と *サンドボックス* は、お使いの環境を参照しません。 同じ API キーのセットを、ローカル環境、開発環境、ステージング環境、実稼動環境など、各環境に対して使用します。
>
>ライセンスオーナーは通常、Adobe Commerce アカウントのプライマリ連絡先であり、クラウドインフラストラクチャプロジェクトにおけるAdobe Commerceのプロジェクトオーナーと同じでないことがあります。

### 実稼動およびサンドボックス API キーの生成 {#genapikey}

1. [!DNL Commerce] アカウント（[https://account.magento.com](https://account.magento.com/customer/account/login){:target="_blank"}）にログインします。

1. 「**Magento**」タブで、サイドバーの **API ポータル** を選択します。

1. _環境_ メニューから、「**実稼動**」または「**サンドボックス**」を選択します。

   >[!NOTE]
   >
   >*実稼動環境* および *サンドボックス* とは、データがAdobe SaaS バックエンドシステムに保存されるデータスペース環境を指します。 キーを使用するコマース環境ではありません。

1. _API キー_ セクションに名前を入力し、**新規追加** をクリックして、新しいキーをダウンロードするためのダイアログを開きます。

   ![&#x200B; 秘密鍵のダウンロード &#x200B;](assets/download-api-private-key.png)

   >[!WARNING]
   >
   > このダイアログでは、キーのコピーまたはダウンロードが必要になる唯一の機会を提供します。

1. 「**ダウンロード**」をクリックし、「**キャンセル**」をクリックします。

1. 各環境（実稼動環境とサンドボックス）で上記の手順を繰り返します。

   **API キー** セクションに API （公開）キーが表示されるようになりました。 ライセンスに関連付けられたいずれかの環境またはインストールで [SaaS プロジェクトを選択または作成 &#x200B;](#createsaasenv) する場合、4 つのキー（実稼動鍵とサンドボックス鍵の両方、公開鍵と秘密鍵）がすべて必要です。

## SaaS 設定 {#saasenv}

[!DNL Commerce] インスタンスは、データを適切な場所に送信できるように、SaaS プロジェクトと SaaS データ領域を使用して設定する必要が [!DNL Commerce Services] ります。 SaaS プロジェクトは、すべての SaaS データ スペースをグループ化します。 SaaS データ スペースは、[!DNL Commerce Services] ーザーが作業できるようにするデータの収集および保存に使用されます。 このデータの一部は [!DNL Commerce] インスタンスから書き出され、一部はストアフロントの買い物客の行動から収集される場合があります。 そのデータは、セキュリティで保護されたクラウドストレージに保持されます。

[!DNL Product Recommendations] えば、SaaS データ スペースには、カタログと行動データが含まれています。 [!DNL Commerce] 設定で [&#x200B; 選択 &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-admin/config/services/saas) することにより、[!DNL Commerce] インスタンスを SaaS データ空間にポイントできます。

>[!WARNING]
>
> **実稼動 SaaS データ領域** は、データの競合を避けるために、実稼動 [!DNL Commerce] インストールでのみ使用します。 そうしないと、テストデータで実稼動サイトデータが汚染され、デプロイメントの遅延が発生するリスクがあります。 例えば、実稼動製品のデータが、ステージング URL などのステージングデータと誤って上書きされる可能性があります。
> &#x200B;> これが発生した場合は、[&#x200B; サポートリクエストを送信 &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-knowledge-base/kb/overview) して、データのクリーンアップをリクエストします。

管理パネルに LiveSearch 設定フィールドが見つからない場合は、正しい SaaS API キーを入力したことを確認します。  実稼動データ領域を設定する際には実稼動 SaaS キーを追加し、ステージングデータ領域を設定する際にはステージングキーを追加していることを確認してください。 誤ったキーを設定すると、LiveSearch などの SaaS サービスはAdobe Commerce環境で使用できなくなります。

### SaaS データ領域のプロビジョニング

すべてのAdobe Commerce マーチャントは、SaaS プロジェクトごとに 1 つの実稼動データスペースと 2 つのテストデータスペースにアクセスできます。

同じデータスペースを複数の環境で同時に使用しない限り、非実稼動環境でテストデータスペースを使用できます。 別の環境でテストデータ領域を使用するには、その環境でデータ領域を選択および設定する前に、データクリーンアップを実行します。

複数のステージング環境を使用する Adobe Commerce Cloud Pro プロジェクトの場合は、[&#x200B; サポートリクエストを送信 &#x200B;](https://experienceleague.adobe.com/home?lang=ja&support-tab=home#support) することで、ステージング環境ごとに追加のテストデータスペースをリクエストできます。 ただし、ステージング環境が 1 つのみで、追加のテストデータスペースが必要な場合は、次のオプションがあります。

- 追加のステージング環境をリクエストする場合は、カスタマーサクセスチームまたは担当のカスタマーサクセスマネージャーにお問い合わせください。

- [&#x200B; サポートリクエストを送信 &#x200B;](https://experienceleague.adobe.com/home?lang=ja&support-tab=home#support) して追加のテストデータスペースをリクエストし、追加のデータスペースに対するビジネス上の正当性を示します。 このリクエストは承認される場合があります。

Adobe支払いサービスを利用しているMagento Open Sourceのお客様は、追加のデータスペースをリクエストする場合もあります。 テストデータスペースをリクエストするには、[&#x200B; サポートリクエスト &#x200B;](https://experienceleague.adobe.com/home?lang=ja&support-tab=home#support) を送信する前に、支払いチームに追加のデータスペースに関する事前承認を問い合わせてください。

複数のクラウドプロジェクトまたはオンプレミス（実稼働/実稼働）インストールを所有しているお客様は、[&#x200B; サポートリクエストを送信 &#x200B;](https://experienceleague.adobe.com/home?lang=ja&support-tab=home#support) することで、各プロジェクトまたはインスタンスに対して追加の実稼働およびテスト用データスペースをリクエストすることもできます。

### SaaS プロジェクトの選択または作成 {#createsaasenv}

SaaS プロジェクトを選択または作成するには、ストアの [!DNL Commerce] ライセンス所有者に [!DNL Commerce] API キーをリクエストします。

>[!NOTE]
>
> **[!UICONTROL Commerce Services Connector]** の設定に [!DNL Commerce] のセクションが表示されない場合は、目的の [!DNL Commerce] サービス [[!DNL Commerce]  に &#x200B;](#availableservices) モジュールをインストールする必要があります。

1. _管理者_ サイドバーで、**システム**/サービス/**Commerce サービスコネクタ** に移動します。

   **[!UICONTROL Commerce Services Connector]** の設定に [!DNL Commerce] のセクションが表示されない場合は、目的の [!DNL Commerce] サービス [[!DNL Commerce]  に &#x200B;](#availableservices) モジュールをインストールします。 また、`magento/module-services-id` パッケージがインストールされていることを確認します。

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

1. **ストアの現在の設定に使用する** データスペース [!DNL Commerce] を選択します。

>[!NOTE]
>
>Commerce サービスと統合するための個別のインスタンスがある場合は、[&#x200B; サポートチケットを送信 &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#submit-ticket) して、追加のインスタンスごとに新しい SaaS プロジェクトをリクエストします。 サポートが SaaS プロジェクトを作成したら、同じ API キーを使用してインスタンスのCommerce Services 統合を設定し、データ空間用の新しい SaaS プロジェクトを選択します。

>[!WARNING]
>
> マイアカウントの API ポータルセクションで新しいキーを生成した場合、直ちに管理設定の API キーを更新します。 新しいキーを生成し、管理者でそれらを更新しない場合、SaaS 拡張機能は機能しなくなり、貴重なデータが失われます。

SaaS プロジェクトまたはデータ領域の名前を変更するには、どちらかの横にある **名前の変更** をクリックします。 名前を変更しても、サービスには影響しません。名前は、プロジェクトとデータ スペースを識別および区別するのに役立つラベルにすぎないからです。

## IMS 組織（オプション） {#organizationid}

Adobe Commerce インスタンスをAdobe Experience Platformに接続するには、Adobe IDを使用してAdobe アカウントにログインします。 ログインすると、Adobe アカウントに関連付けられた IMS 組織がこのセクションに表示されます。

## SaaS データのエクスポート

[!DNL Commerce] インスタンスが [!DNL Commerce Services] に正常に接続されると、SaaS データ書き出しプロセスによって、Commerce データが [!DNL Commerce] サーバーから [!DNL Commerce SaaS Services] に書き出され、接続されたCommerce Services に同期できるようになります。 管理者では、[&#x200B; データ管理ダッシュボード &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-admin/systems/data-transfer/data-dashboard) を使用して、同期ステータスを確認できます。 詳細については、「[SaaS データ書き出しガイド &#x200B;](../data-export/overview.md)」を参照してください。
