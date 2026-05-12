---
title: Commerce Services Connector
description: 実稼動およびサンドボックス API キーを使用して、Adobe CommerceまたはMagento Open Source インスタンスをサービスに統合する方法を説明します。
feature: Services, Saas
role: Admin, User
exl-id: 1aa6ba8b-be39-496e-b83d-a4a7db9f5dd8
badgePaas: label="PaaSのみ" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce on Cloud プロジェクト（Adobeで管理されるPaaS インフラストラクチャ）とオンプレミス プロジェクトにのみ適用されます。"
TQID: https://experienceleague.adobe.com/pWbJSCrV9CcdJXNTkuXyCxh73eUA7nYt1okexwtK7II
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: bd989d82-1e15-4534-88db-f1f51dd77ffa
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
subfeature_v2:
  - id: f8ddfd3b-6194-46e8-a176-0e918039be56
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2:
  - id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377
  - id: c4147b6e-073b-4d3c-9ab1-d60f2f4434ef
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: 33cd0e217447351b690646ec8d230f76060a74da
workflow-type: tm+mt
source-wordcount: 1662
ht-degree: 0%

---

# [!DNL Commerce Services Connector]

Adobe CommerceとMagento Open Sourceの一部の機能は[!DNL Commerce Services]によって提供され、SaaS （Software as a Service）としてデプロイされます。 これらのサービスを使用するには、実稼動用およびサンドボックス API キーを使用して[!DNL Commerce] インスタンスを接続し、[設定](#saas-configuration)でデータ領域を指定する必要があります。 各インスタンスに対して1回だけ接続を設定する必要があります。

これらのAPI キーを生成できるのは、[!DNL Commerce] ライセンス所有者のみです。 ライセンス所有者でない場合は、ストアのCommerce ライセンスを所有しているユーザーまたはチームにキーをリクエストしてください。

## 利用可能なサービス {#availableservices}

次に、[!DNL Commerce Services Connector]を通じてアクセスできる[!DNL Commerce]機能を示します。

| サービス | 対象 |
| --- | --- |
| Adobe AIによる[[!DNL Product Recommendations]](/help/product-recommendations/overview.md) | Adobe Commerce |
| Adobe AIによる[[!DNL Live Search]](/help/live-search/overview.md) | Adobe Commerce |
| [[!DNL Payment Services]](/help/payment-services/guide-overview.md) | Adobe CommerceとMagento Open Source |
| [[!DNL Catalog Service]](/help/catalog-service/overview.md) | Adobe Commerce |
| [[!DNL Data Connection]](/help/data-connection/overview.md) | Adobe Commerce |

## デザイン

上位レベルでは、[!DNL Commerce Services Connector]は次のコア要素で構成されています。

![Commerce Services Connector Architecture](assets/saas-config-sync-workflow.png)

次の節では、これらの各要素について詳しく説明します。

## 資格情報 {#apikey}

実稼動用およびサンドボックス API キーは、[&#x200B; ライセンス所有者](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/start/onboarding)の[!DNL Commerce] アカウントから生成されます。 Commerce アカウントは、一意の[!DNL Commerce] ID （MageID）によって識別されます。 加盟店の組織のライセンス所有者は、アカウントが良好な状態であれば、商品レコメンデーションやライブサーチなどのサービス用のAPI キーを生成できます。

キーは、ライセンス所有者に代わってプロジェクトや環境を管理するシステムインテグレーターまたは開発チームと「知っておく必要がある」方法で共有できます。 ライセンス所有者から[!DNL Shared Access]を付与された開発者は、アカウントの[!DNL Switch Accounts] ドロップダウンに加盟店の組織が存在する場合でも、ライセンス所有者に代わってキーを生成することはできません。

さらに、ソリューションインテグレーターは[!DNL Commerce Services]を使用する権利があります。 ソリューション インテグレーターの場合、[!DNL Commerce]のパートナー契約の署名者はAPI キーを生成する必要があります。

キー識別子&#x200B;*実稼動環境*&#x200B;および&#x200B;*サンドボックス*&#x200B;は、[!DNL Commerce Services]がデータを保存するSaaS データスペース環境を参照します（Adobe Commerce環境には含まれません）。 ローカル、開発、ステージング、実稼動のAdobe Commerce環境で同じAPI キーのセットを使用できます。重要なのは、設定したデータ領域に対して正しいキーペアを貼り付けることです。

通常、ライセンスオーナーは、Adobe Commerce アカウントのプライマリ担当者であり、Adobe Commerce オンクラウドインフラストラクチャプロジェクトのプロジェクトオーナーと必ずしも同じではありません。

### 実稼動およびサンドボックス API キーの生成 {#genapikey}

1. [https://account.magento.com](https://account.magento.com/customer/account/login){:target="_blank"}で[!DNL Commerce] アカウントにログインします。

1. 「**Magento**」タブで、サイドバーの「**API Portal**」を選択します。

1. _環境_ メニューから、**実稼動**&#x200B;または&#x200B;**サンドボックス**&#x200B;を選択します。

1. _API キー_ セクションに名前を入力し、**新規を追加**&#x200B;をクリックしてダイアログを開き、新しいキーをダウンロードします。

   ![秘密鍵をダウンロード &#x200B;](assets/download-api-private-key.png)

   >[!WARNING]
   >
   > 秘密鍵のコピーまたはダウンロードは1回のみです。 安全な保管：

1. 「**ダウンロード**」をクリックして秘密鍵を保存し、ダイアログを閉じます。

1. 各環境（実稼動環境とサンドボックス）に対して、上記の手順を繰り返します。

   「**API キー**」セクションに、API （公開）キーが表示されるようになりました。 ライセンスに関連する環境またはインストールのいずれかで[SaaS プロジェクト &#x200B;](#createsaasenv)を選択または作成する場合は、4つのキー（実稼動用キーとサンドボックスキーの両方、パブリック+プライベート）がすべて必要です。

## SaaS設定 {#saasenv}

[!DNL Commerce Services]が適切な場所にデータを送信できるように、[!DNL Commerce] インスタンスをSaaS プロジェクトとSaaS データスペースで設定する必要があります。 SaaS プロジェクトは、あらゆるSaaS データ空間をグループ化します。 SaaS データ スペースは、[!DNL Commerce Services]が作業できるようにデータを収集および保存するために使用されます。 このデータの一部は[!DNL Commerce] インスタンスからエクスポートされ、一部はストアフロントの買い物客の行動から収集される可能性があります。 そのデータは、クラウドストレージのセキュリティを確保するために保持されます。

[!DNL Product Recommendations]と[!DNL Live Search]の場合、SaaS データ スペースにはカタログと行動データが含まれます。 [!DNL Commerce]設定で[&#128279;](https://experienceleague.adobe.com/en/docs/commerce-admin/config/services/saas)を選択すると、[!DNL Commerce] インスタンスをSaaS データ領域にポイントできます。

>[!WARNING]
>
> 実稼動[!DNL Commerce]のインストールでのみ&#x200B;**実稼動SaaS データ領域**&#x200B;を使用します。 実稼動以外の環境で使用すると、テストとライブデータ（ステージング URLやテストカタログデータなど）を混在させることができます。 このような場合は、[&#x200B; サポートリクエスト &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/overview)を送信してデータクリーンアップをリクエストしてください。

管理者にライブサーチ設定フィールドが見つからない場合は、選択したデータスペースに対して正しいAPI キーペアを入力したことを確認します（実稼動データスペースでは実稼動キーを使用し、テストデータスペースではサンドボックスキーを使用します）。 誤ったキーを設定した場合、ライブサーチなどのSaaS サービスは、そのAdobe Commerce環境では使用できません。

### API キーの削除 {#delapikey}

>[!WARNING]
>
>まだアクティブに使用されているキーを削除すると、接続されたサービスが直ちに中断されます。

API キーを削除する前に、置き換えキーを生成して安全に保存します。 新しいキーを使用するためにすべての統合を更新し、依存サービスが期待どおりに機能していることを確認します。

管理パネルに&#x200B;**[!DNL Live Search]**&#x200B;設定フィールドが表示されない場合は、その環境に正しいSaaS API キーを入力したことを確認してください。 実稼動データ領域には実稼動SaaS キーを、ステージング データ領域にはステージング キーを使用します。 誤ったキーが設定されている場合、Adobe Commerce環境ではSaaS サービス（**[!DNL Live Search]**&#x200B;を含む）を利用できません。

削除するAPI キーで、**[!UICONTROL Delete]**&#x200B;をクリックします。 確認メッセージが表示されたら、キーを完全に削除する操作を確認します。

### SaaS データ空間のプロビジョニング

Adobe Commerceをご利用のお客様は、SaaS プロジェクトごとに、1つの本番データスペースと2つのテストデータスペースにアクセスできます。

実稼動以外の環境では、テストデータスペースを使用できますが、複数の環境で同じデータスペースを同時に使用することは避けてください。 テストデータスペースを別の環境に移動する場合は、新しい環境で選択して設定する前にデータクリーンアップを実行します。

複数のステージング環境を持つAdobe Commerce Cloud Pro プロジェクトの場合は、[&#x200B; サポートリクエストを送信](https://experienceleague.adobe.com/home?support-tab=home#support)することにより、ステージング環境ごとに追加のテストデータスペースをリクエストできます。 ただし、ステージング環境が1つしかなく、追加のテストデータスペースが必要な場合は、次のオプションを使用できます。

- カスタマーサクセスチームまたは専任のカスタマーサクセスマネージャーに連絡して、追加のステージング環境をリクエストしてください。

- [追加のテストデータ領域をリクエストし、追加のデータ領域のビジネス上の理由を示すには、サポートリクエスト &#x200B;](https://experienceleague.adobe.com/home?support-tab=home#support)を送信します。 この要求は承認済みです。

Adobe Payment Servicesをご利用のMagento Open Sourceのお客様は、追加のデータスペースをリクエストすることもできます。 テストデータスペースをリクエストするには、[&#x200B; サポートリクエスト &#x200B;](https://experienceleague.adobe.com/home?support-tab=home#support)を送信する前に、支払いチームに追加データスペースの事前承認を依頼してください。

複数のクラウドプロジェクトまたはオンプレミス（ライブ/実稼動）のインストールを所有しているお客様は、[&#x200B; サポートリクエスト &#x200B;](https://experienceleague.adobe.com/home?support-tab=home#support)を送信することで、各プロジェクトまたはインスタンスの追加の実稼動およびテストデータスペースをリクエストすることもできます。

### SaaS プロジェクトの選択または作成 {#createsaasenv}

SaaS プロジェクトを選択または作成するには、ストアの[!DNL Commerce] ライセンス所有者から[!DNL Commerce] API キーをリクエストします。

1. _管理者_ サイドバーで、**システム**/サービス/**Commerce Services Connector**&#x200B;に移動します。

   **[!UICONTROL Commerce Services Connector]** セクションが表示されない場合は、目的の[[!DNL Commerce]  サービス &#x200B;](#availableservices)の[!DNL Commerce] モジュールをインストールし、`magento/module-services-id` パッケージがインストールされていることを確認します。

1. _[!UICONTROL Sandbox API Keys]_&#x200B;および&#x200B;_[!UICONTROL Production API Keys]_ セクションにキー値を貼り付けます。

   - 秘密鍵には、キーの先頭に`-----BEGIN PRIVATE KEY-----`、キーの末尾に`-----END PRIVATE KEY-----`を含める必要があります。
   - 実際のキーのコピーがない場合は、ライセンス所有者に確認し、値を設定に接続します。

   データベースのバックアップまたはスナップショットからコピーしたキー値を貼り付けないでください。 設定が保存されると、暗号化の追加レイヤーが適用され、キーは機能しません。

1. **保存**&#x200B;をクリックします。

   キーに関連付けられているSaaS プロジェクトはすべて、**SaaS識別子** セクションの&#x200B;**プロジェクト** フィールドに表示されます。

1. SaaS プロジェクトが存在しない場合は、**プロジェクトを作成**&#x200B;をクリックします。 次に、**プロジェクト** フィールドに、SaaS プロジェクトの名前を入力します。

   混乱を避けるために、特定のCommerce サービスをプロジェクトの名前として使用しないでください（例：*Live Search*、*Product Recommendations*、*Data Connection*）。 ライセンスが複数のSaaS プロジェクト用にプロビジョニングされていない限り、同じSaaS プロジェクトを複数のサービスに使用できます。

1. [!DNL Commerce] ストアの現在の設定に使用する&#x200B;**データ領域**&#x200B;を選択します。

   Commerce サービスと統合する個別のインスタンスがある場合、[&#x200B; サポートチケットを送信](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#submit-ticket)して、追加のインスタンスごとに新しいSaaS プロジェクトをリクエストします。 サポートがSaaS プロジェクトを作成したら、同じAPI キー&#x200B;**を使用してインスタンス**&#x200B;のCommerce Services Connectorを設定し、新しいSaaS プロジェクトとデータスペースを選択します。

>[!WARNING]
>
> API ポータルで新しいキーを生成した場合は、管理者設定でAPI キーをすぐに更新します。 管理者が古いキーを引き続き使用している場合、SaaS拡張機能が動作しなくなり、データ収集が中断されます。

SaaS プロジェクトまたはデータスペースの名前を変更するには、いずれかの横にある&#x200B;**名前を変更**&#x200B;をクリックします。 名前を変更してもサービスには影響しません。名前は、プロジェクトとデータ空間を識別して区別するのに役立つラベルにすぎません。

## IMS組織（オプション） {#organizationid}

Adobe Commerce インスタンスをAdobe Experience Platformに接続するには、Adobe IDを使用してAdobe アカウントにログインします。 ログインすると、Adobe アカウントに関連付けられているIMS組織がこのセクションに表示されます。

## SaaS データ書き出し

[!DNL Commerce] インスタンスが[!DNL Commerce Services]に正常に接続すると、SaaS データ書き出しプロセスによって[!DNL Commerce] サーバーから[!DNL Commerce SaaS Services]にCommerce データが書き出され、接続されているCommerce サービスに同期できるようになります。 管理者では、[&#x200B; データ管理ダッシュボード &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard)を使用して同期ステータスを確認できます。 詳しくは、[SaaS データ書き出しガイド &#x200B;](../data-export/overview.md)を参照してください。
