---
title: 統合の設定
description: Adobe Commerce プロジェクトとExperience Manager Assets プロジェクトを接続して、これら 2 つのシステム間のアセット同期を有効にする方法を説明します。
feature: CMS, Media
source-git-commit: b6e190e883087a942630f0a27781654cd2c68781
workflow-type: tm+mt
source-wordcount: '546'
ht-degree: 0%

---


# 統合の設定

CommerceをAEM Assets インスタンスに接続し、アセット同期の一致する方法を選択することで、統合を設定します。

AEM Assets プロジェクトを特定した後、Adobe CommerceとAEM Assetsの間でアセットを同期するための一致ルールを選択します。

* **[!UICONTROL Match by product SKU]** - アセットが正しい商品に関連付けられるようにするために、アセットメタデータの SKU を [&#128279;](https://experienceleague.adobe.com/ja/docs/commerce-operations/implementation-playbook/glossary#sku)1&rbrace;Commerce商品 SKU&rbrace; と一致させるデフォルトのルール。

* **[!UICONTROL Custom match]** - カスタム・マッチング・ロジックを必要とするより複雑なシナリオや特定のビジネス要件の照合ルール。 カスタムマッチングを実装するには、アセットと商品のマッチング方法を定義するカスタムコードをAdobe Developer App Builderで開発する必要があります。 詳細は近日公開予定です…

初期設定では、デフォルトの *製品 SKU で一致* ルールを使用します。

## 前提条件

* [AEM Assets パッケージのインストール](configure-aem.md)

* [!BADGE PaaS のみ &#x200B;]{type=Informative tooltip="クラウドプロジェクト上のAdobe Commerceにのみ適用されます（Adobeが管理する PaaS インフラストラクチャ）。"}[Adobe Commerce パッケージをインストール ](configure-commerce.md) して、拡張機能を追加し、その拡張機能を使用するために必要な資格情報と接続を生成します。

* [Dynamic Media Open API を有効にする ](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/assets/dynamicmedia/dynamic-media-open-apis/dynamic-media-open-apis-overview#enable-dynamic-media-open-apis) トピックに記載されている手順に従います。 サポートチームには、次の情報を含めます。

   * **[!UICONTROL AEM Program ID]**
   * **[!UICONTROL Adobe Commerce URL]**
   * **[!UICONTROL AEM Environment ID]**,
   * Commerceに接続するAEM Assets オーサリング環境の **[!UICONTROL IMS Org ID]** ール。

## 接続の設定

1. [AEM Assets オーサリング環境 ](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/sites/authoring/quick-start) プロジェクトおよび環境 ID を取得します。

   1. AEM Cloud Managerを開き、「**[!UICONTROL Assets]**」を選択します。

   1. 次の URL からプロジェクト ID と環境 ID をコピーして保存します。<br>`https://author-p[Program ID]-e[EnvironmentID].adobeaemcloud.com/`

1. Commerce Admin から、AEM Assets Integration configuration を開きます。

   1. **[!UICONTROL Store]**/設定/**[!UICONTROL ADOBE SERVICES]**/**[!UICONTROL AEM Assets Integration]** に移動します。

      ![AEM Assets統合：統合の有効化 ](../assets/aem-assets-integration-enable-config.png){width="600" zoomable="yes"}

1. AEM Assets環境 **[!UICONTROL Program ID]** と **[!UICONTROL Environment ID]** を入力します。

   *[!UICONTROL Use system value]* から選択内容を削除して、設定値を編集します。

1. **[!UICONTROL Asset Selector IMS Client ID]** を入力します。

   アセットセレクターについて詳しくは、「[ 手動によるアセットの選択 ](../synchronize/asset-selector-integration.md)」を参照してください。

1. [!BADGE PaaS のみ &#x200B;]{type=Informative tooltip="クラウドプロジェクト上のAdobe Commerceにのみ適用されます（Adobeが管理する PaaS インフラストラクチャ）。"} Commerceとアセット照合サービスの間でリクエストを認証する [[!UICONTROL Commerce integration]](configure-commerce.md#add-the-integration-to-the-commerce-environment) を選択します。

1. **[!UICONTROL Integration enabled]** を `Yes` に設定して、CommerceがAEM Assetsからの受信アップデートを受け入れるようにします。

   統合を有効にすると、アセットの一致条件を指定するために、追加の設定オプションを使用できます。

1. **[!UICONTROL Asset matching rule]** ドロップダウンから、アセット同期用のアセット一致ルールの 1 つを選択します。

   * [ デフォルトの自動照合 ](../synchronize/default-match.md) の **[!UICONTROL Match by SKU]** を選択します。
   * [ カスタム自動照合 ](../synchronize/custom-match.md) の **[!UICONTROL Custom match]** を選択します（[Adobe Developer App Builder](https://experienceleague.adobe.com/ja/docs/commerce-learn/tutorials/adobe-developer-app-builder/introduction-to-app-builder) が必要です）。

1. Commerce製品 SKU に対して定義された [&#128279;](configure-aem.md#configure-metadata)0&rbrace;AEM Assets メタデータフィールド名を「**[!UICONTROL Match by product SKU attribute name]**」フィールドに追加します（デフォルトでは `commerce:skus`）。

1. 「**[!UICONTROL Save Config]**」を選択すると、更新を適用し、アセットの同期を開始します。

   設定の更新は初期同期プロセスをトリガーし、CommerceがAEM Assetsから受信する更新を受け入れるようにします。 同期に要する時間は、アセットの量と特定の設定によって異なります。 この統合では、自動化されたプロセスを活用して、同期に要する時間を最小限に抑えます。

### 同期SLA

統合により、次の同期パフォーマンスレベルが保証されます。

* `< 5 minutes for 99% of updates`

* `< 30 minutes for 99.9% of updates`

これにより、製品ページに常に最新の画像を表示でき、ストアフロントのコンテンツを正確で視覚的に魅力的に保つことができます。

### オプション。 カスタムドメイン URL の設定

AEM Assets as a Cloud Service プロジェクトが [ カスタムドメイン名 ](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/custom-domain-names/add-custom-domain-name){target=_blank} で設定されている場合は、Commerce ストア設定にドメイン名を追加して、CommerceのAEM Assets統合で使用できるようにする必要があります。

1. **[!UICONTROL Store]**/設定/**[!UICONTROL ADOBE SERVICES]**/**[!UICONTROL AEM Assets Integration]** に移動します。

   ![AEM Assets統合：統合の有効化 ](../assets/aem-assets-view.png){width="600" zoomable="yes"}

1. **カスタムドメイン URL** を **[!UICONTROL Asset Custom Domain]** フィールドに追加します。

1. 「**[!UICONTROL Save Config]**」をクリックして更新を適用し、アセットの同期を開始します。

## 次の手順

[製品ビジュアルでのCommerce アセットの管理](../manage-assets.md)
