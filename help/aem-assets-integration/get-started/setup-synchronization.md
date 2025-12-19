---
title: 統合の設定
description: Adobe Commerce プロジェクトとExperience Manager Assets プロジェクトを接続して、これら 2 つのシステム間のアセット同期を有効にする方法を説明します。
feature: CMS, Media
exl-id: 3533d010-926f-4d78-935c-98a9b7040d27
source-git-commit: d426c7878f7a66fe1047673be7c5bf65ae1949a7
workflow-type: tm+mt
source-wordcount: '786'
ht-degree: 0%

---

# 統合の設定

CommerceをAEM Assets インスタンスに接続し、アセット同期の一致する方法を選択することで、統合を設定します。

AEM Assets プロジェクトを特定した後、Adobe CommerceとAEM Assetsの間でアセットを同期するための一致ルールを選択します。

* **[!UICONTROL Match by product SKU]** - アセットが正しい商品に関連付けられるようにするために、アセットメタデータの SKU を [1&rbrace;Commerce商品 SKU&rbrace; と一致させるデフォルトのルール。](https://experienceleague.adobe.com/ja/docs/commerce-operations/implementation-playbook/glossary#sku)

* **[!UICONTROL Custom match]** - カスタム・マッチング・ロジックを必要とするより複雑なシナリオや特定のビジネス要件の照合ルール。 カスタムマッチングを実装するには、アセットと商品のマッチング方法を定義するカスタムコードをAdobe Developer App Builderで開発する必要があります。 詳細は近日公開予定です…

初期設定では、デフォルトの *製品 SKU で一致* ルールを使用します。

## 前提条件

* [AEM Assets プロジェクトの設定](configure-aem.md)

* [!BADGE PaaS のみ &#x200B;]{type=Informative tooltip="クラウドプロジェクト上のAdobe Commerceにのみ適用されます（Adobeが管理する PaaS インフラストラクチャ）。"}[Adobe Commerce パッケージをインストール &#x200B;](configure-commerce.md) して、拡張機能を追加し、その拡張機能を使用するために必要な資格情報と接続を生成します。

* [Dynamic Media Open API を有効にする &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/assets/dynamicmedia/dynamic-media-open-apis/dynamic-media-open-apis-overview#enable-dynamic-media-open-apis) トピックに記載されている手順に従います。 サポートチームには、次の情報を含めます。

   * **[!UICONTROL AEM Program ID]**
   * **[!UICONTROL Adobe Commerce URL]**
   * **[!UICONTROL AEM Environment ID]**,
   * Commerceに接続するAEM Assets オーサリング環境の **[!UICONTROL IMS Org ID]** ール。

## 接続の設定

1. [AEM Assets オーサリング環境 &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/sites/authoring/quick-start) プロジェクトおよび環境 ID を取得します。

   1. AEM Cloud Managerを開き、「**[!UICONTROL Assets]**」を選択します。

   1. 次の URL からプロジェクト ID と環境 ID をコピーして保存します。<br>`https://author-p[Program ID]-e[EnvironmentID].adobeaemcloud.com/`

1. Commerce Admin から、AEM Assets Integration configuration を開きます。

   1. **[!UICONTROL Store]**/設定/**[!UICONTROL ADOBE SERVICES]**/**[!UICONTROL AEM Assets Integration]** に移動します。

      ![AEM Assets統合：統合の有効化 &#x200B;](../assets/aem-assets-view.png){width="600" zoomable="yes"}

>[!INFO]
>
> AEM Assets統合では、グローバル（デフォルト）スコープでの設定のみがサポートされます。 Web サイトレベルの設定はサポートされていません。 Web サイトレベルで統合を設定しようとすると、システムは web サイトレベルの設定を無視して、代わりにグローバル設定値を使用します。

1. AEM Assets環境 **[!UICONTROL Program ID]** と **[!UICONTROL Environment ID]** を入力します。

   *[!UICONTROL Use system value]* から選択内容を削除して、設定値を編集します。

1. **[!UICONTROL Asset Selector IMS Client ID]** を入力します。

   アセットセレクターについて詳しくは、「[&#x200B; 手動によるアセットの選択 &#x200B;](../synchronize/asset-selector-integration.md)」を参照してください。

1. [!BADGE PaaS のみ &#x200B;]{type=Informative tooltip="クラウドプロジェクト上のAdobe Commerceにのみ適用されます（Adobeが管理する PaaS インフラストラクチャ）。"} Commerceとアセット照合サービスの間でリクエストを認証する [[!UICONTROL Commerce integration]](configure-commerce.md#add-the-integration-to-the-commerce-environment) を選択します。

1. **[!UICONTROL Commerce integration]** を `assets-integration` に設定して、AEM Assetsで使用するCommerce統合を選択します。

1. **[!UICONTROL Synchronization enabled]** を `Yes` に設定して、CommerceがAEM Assetsからの受信アップデートを受け入れるようにします。

   統合を有効にすると、アセットの一致条件を指定するために、追加の設定オプションを使用できます。

1. **[!UICONTROL Asset matching rule]** ドロップダウンから、アセット同期用のアセット一致ルールの 1 つを選択します。

   * **[!UICONTROL Match by SKU]** デフォルトの自動照合 [&#x200B; の &#x200B;](../synchronize/default-match.md) を選択します。
   * **[!UICONTROL Custom match]** カスタム自動照合 [&#x200B; の &#x200B;](../synchronize/custom-match.md) を選択します（[Adobe Developer App Builder](https://experienceleague.adobe.com/ja/docs/commerce-learn/tutorials/adobe-developer-app-builder/introduction-to-app-builder) が必要です）。

1. Commerce製品 SKU に対して定義された [0&rbrace;AEM Assets メタデータフィールド名を「](configure-aem.md#configure-metadata)」フィールドに追加します（デフォルトでは **[!UICONTROL Match by product SKU attribute name]**）。`commerce:skus`

1. 「**[!UICONTROL Save Config]**」を選択すると、更新を適用し、アセットの同期を開始します。

   設定の更新は初期同期プロセスをトリガーし、CommerceがAEM Assetsから受信する更新を受け入れるようにします。 同期に要する時間は、アセットの量と特定の設定によって異なります。 この統合では、自動化されたプロセスを活用して、同期に要する時間を最小限に抑えます。

### 同期SLA

統合により、次の同期パフォーマンスレベルが保証されます。

* `< 5 minutes for 99% of updates`

* `< 30 minutes for 99.9% of updates`

これにより、製品ページに常に最新の画像を表示でき、ストアフロントのコンテンツを正確で視覚的に魅力的に保つことができます。

### ビジュアライゼーション所有者の設定

**ビジュアライゼーション所有者** 設定は、統合で製品画像を提供するシステムを決定します。

* Adobe Commerce - Commerceでホストされる画像を使用します。
* AEM Assets - AEMから同期された画像を使用します。

管理者には、その所有者で使用可能な画像が表示されますが、残りの画像はグレー表示され、「**非表示** ラベルで表示されます。

画像の表示動作について詳しくは、[&#x200B; 画像の詳細を設定 &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-admin/catalog/products/digital-assets/product-image#set-image-details){target=_blank} トピックを参照してください。

>[!TIP]
>
> CommerceからAEM Assetsへの移行時に、**ビジュアライゼーションオーナー** をCommerceに設定して、画像リンクが壊れないようにします。 すべての商品がAEM Assetsと正常に同期されたら、AEM Assets オーナーに切り替えて移行を完了します。 これにより、プロセス全体を通じて画像の継続的な可用性が確保されます。

1. **[!UICONTROL Store]**/設定/**[!UICONTROL ADOBE SERVICES]**/**[!UICONTROL AEM Assets Integration]** に移動します。

   ![AEM Assets統合ビジュアライゼーションオーナー機能 &#x200B;](../assets/visualization-owner-detail.png){width="400" zoomable="yes"}

1. **ビジュアライゼーション所有者** ソースを選択して画像を表示します。

1. 「**[!UICONTROL Save Config]**」をクリックして更新を適用し、アセットの同期を開始します。

### オプション。 カスタムドメイン URL の設定

AEM Assets as a Cloud Service プロジェクトが [&#x200B; カスタムドメイン名 &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/custom-domain-names/add-custom-domain-name){target=_blank} で設定されている場合は、Commerce ストア設定にドメイン名を追加して、CommerceのAEM Assets統合で使用できるようにする必要があります。

1. **[!UICONTROL Store]**/設定/**[!UICONTROL ADOBE SERVICES]**/**[!UICONTROL AEM Assets Integration]** に移動します。

   ![AEM Assets統合：統合の有効化 &#x200B;](../assets/aem-assets-view.png){width="700" zoomable="yes"}

1. **カスタムドメイン URL** を **[!UICONTROL Asset Custom Domain]** フィールドに追加します。

1. 「**[!UICONTROL Save Config]**」をクリックして更新を適用し、アセットの同期を開始します。

## 次の手順

* **Commerce ストアフロントの設定** - Edge Delivery Servicesを使用したCommerce ストアフロントでAEM Assetsを使用するには、[Adobe Commerce ストアフロントのドキュメントの &#x200B;](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/aem-assets-configuration/?lang=ja)AEM Assetsの統合 *のトピックで説明されているストアフロント設定を行ってください*。

* Adobe CommerceとAEM Assets統合の間に [&#x200B; 一致ルール &#x200B;](../synchronize/default-match.md) を設定します。

* [Commerce アセットの管理 &#x200B;](../manage-assets.md).
