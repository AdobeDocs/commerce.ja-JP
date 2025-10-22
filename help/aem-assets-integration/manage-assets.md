---
title: アセットの管理
description: CommerceのAEM Assets統合を使用すると、ストアフロントのメディアアセットを管理できます。
feature: CMS, Media
exl-id: 40ca36e0-d617-4814-852d-bc60ff53b2b3
source-git-commit: 5dd290a4e10bdbd1f6c96b67ab6c9ba1598705dc
workflow-type: tm+mt
source-wordcount: '866'
ht-degree: 0%

---

# Commerce Media アセットの管理

<!--In ACAP-844, this topic was linked to from the Commerce Admin products images and videos when the Assets integration is enabled. If the URL to the topic changes, be sure to add a redirect.-->

CommerceのAEM Assets統合を有効にすると、次のメディアタイプを管理できます。

* 製品画像
* コンテンツ画像
* 製品ビデオ
* カテゴリ画像

## 製品画像

この統合を有効にすると、画像管理がデジタルアセット管理システム（DAM）内で一元化されます。 Adobe Commerceは、主要なエンゲージメントチャネルとして機能し、承認された高品質の画像のみをストアフロント全体で使用するようにします。 この設定により、ブランドの一貫性が向上し、手動の作業が最小限に抑えられ、コンテンツの更新が効率化されます。マーチャントはAdobe Commerce内で画像を手動でアップロードまたは管理する必要がなくなります。

### Adobe Commerceでの商品画像の表示

商品画像は、事前設定されたマッチングルールに基づいてAEM Assetsから自動的に取り込まれます。

1. _管理者_ サイドバーで、**[!UICONTROL Catalog]**/**[!UICONTROL Products]** に移動します。

1. 商品を選択します。

1. 「**画像とビデオ** セクションを開きます。

   ![&#x200B; 製品画像 &#x200B;](assets/product-image.png){width="600" zoomable="yes"}

   >[!NOTE]
   >
   > 画像管理が DAM に一元化されているので、統合が有効になり、これが **読み取り専用** セクションになることを示すメッセージが表示されます。

### AEM Assetsでの商品画像の管理

商品関連の画像を管理するには、すべての変更を **0&rbrace;AEM Assets&rbrace; で直接行う必要があります。**&#x200B;このプロセスは完全に自動化されており、手動の操作を必要とせずに、変更内容がAdobe Commerceに確実に同期されます。

### 同期 SLA

このトピックについて詳しくは、[&#x200B; 同期SLA](get-started/setup-synchronization.md#synchronization-sla) を参照してください。

## コンテンツ画像

Adobe Commerceは、Adobe Experience Manager（CMS）ツールセットを使用していないマーチャント向けに **ページビルダーを** コンテンツ管理システム（AEM）として提供します。 コンテンツの作成を強化するために、[AEM アセットセレクター &#x200B;](synchronize/asset-selector-integration.md) を活用し、マーケターが **DAM** から直接、画像にシームレスにアクセスして埋め込めるようにします。 これにより、承認された高品質の画像のみがコンテンツの作成に使用されるので、Adobe Commerceに冗長なストレージを保存する必要がなくなります。

### ページビルダーでのAEM アセットセレクターの使用

[!BADGE PaaS のみ &#x200B;]{type=Informative tooltip="クラウドプロジェクト上のAdobe Commerceにのみ適用されます（Adobeが管理する PaaS インフラストラクチャ）。"}**AEM アセットセレクター** を使用して画像を埋め込むには：

1. **ページビルダー** を使用して、`content enrichment` をサポートする **0&rbrace;Adobe Commerce管理者 &rbrace; の任意のセクションに移動します。**

1. [&#x200B; ページビルダー &#x200B;](https://developer.adobe.com/commerce/frontend-core/page-builder/){target=_blank} を開きます。

   **AEM Asset** という新しいメディアタイプが使用できるようになります。

1. AEM Asset メディアタイプをコンテンツブロックにドラッグ&amp;ドロップします。

1. プロンプトが表示されたら、DAM にアクセスするための資格情報を入力します。

1. DAM から画像を選択して、コンテンツに直接挿入します。

選択された画像への関連付けは、**Dynamic Media** を指すダイレクト URL としてAdobe Commerceに保存され、以下を保証します。

* 画像ファイルは、Adobe Commerceに保存する必要はありません。

* マーケターは、DAM 内の承認済みアセットでのみ作業します。

* コンテンツは、すべての顧客タッチポイントにわたって一貫性を保ち、最新の状態を保ちます。

>[!TIP]
>
> [DA.live （ドキュメントオーサリング） &#x200B;](https://experienceleague.adobe.com/developer/commerce/storefront/merchants/storefront-builder/?lang=ja#dalive-document-authoring){target=_blank} では、データをエンリッチメントするためのアセットセレクターも提供しています。

## 製品ビデオ

Adobe Commerceは、デジタルアセットの主要なエンゲージメントチャネルとして機能します。 AEM Assets統合を有効にすると、ビデオ管理が **DAM** 内で一元化され、コマースストアフロント間での一貫性、コンプライアンス、最適化された配信が確保されます。

### 製品ビデオの管理

1. _管理者_ サイドバーで、**[!UICONTROL Catalog]**/**[!UICONTROL Products]** に移動します。

1. 商品を選択します。

1. 「**画像とビデオ** セクションを開きます。

   ![&#x200B; 製品画像 &#x200B;](assets/product-image.png){width="600" zoomable="yes"}

   >[!NOTE]
   >
   > ビデオがAEM Assetsでコントロールされるので、このセクションを **読み取り専用** にする統合が有効であることを示すメッセージが表示されます。

### AEM Assetsでのビデオの関連付け

1. AEM Assetsで、商品に関連付けるビデオに移動します。

1. ビデオをAdobe Commerceの 1 つ以上の商品にリンクします。

1. 統合により関連付けが自動的に同期され、Dynamic Media ビデオプレーヤーがストアフロントに直接表示されます。 これにより、マーチャントがビデオ再生設定を管理する必要がなくなります。

### API ファーストのビデオのサポートのみ

現在、統合は API を介してビデオをサポートしており、パートナーはプログラムでビデオを取得できます。

>[!WARNING]
>
> デフォルトでは、ビデオは既存のAdobe Commerce ストアフロントソリューションにまだ統合されていません。

この統合により、マーチャントは、AEM Assetsと Dynamic Media を活用してシームレスな配信を行い、製品ビデオをスケーラブルかつ最適化された方法で簡単に管理できるようになります。

### 同期 SLA

このトピックについて詳しくは、[&#x200B; 同期SLA](get-started/setup-synchronization.md#synchronization-sla) を参照してください。

## カテゴリ画像

Adobe Commerceを使用すると、マーチャントは画像を商品カテゴリに関連付けて、視覚的に魅力的なストアフロントを作成できます。 AEM Assets統合では、AEM アセットセレクターを活用しているので、マーケターは **Digital Asset Management System （DAM）** から直接、シームレスにアセットを選択できます。 これにより、承認された画像のみが使用され、Adobe Commerceに保存する必要がなくなるので、すべてのエンゲージメントチャネルにわたって一貫性と効率性が維持されます。

### カテゴリ画像に対するAEM アセットセレクターの使用

[AEM アセットセレクター &#x200B;](synchronize/asset-selector-integration.md) を設定した後、それを使用してカタログカテゴリコンテンツにアセットを追加できます。

1. _管理者_ サイドバーで、**[!UICONTROL Catalog]**/**[!UICONTROL Categories]** に移動します。

1. 更新するカテゴリを選択します。

1. 「![」セクションの &#x200B;](../assets/icon-display-expand.png) 展開セレクター **[!UICONTROL Content]** を展開します。

1. 「**[!UICONTROL Content]**」セクションで、カテゴリに関連付けられている *画像フィールド* を見つけます。

   ![&#x200B; カテゴリコンテンツ &#x200B;](assets/category-asset.png){width="600" zoomable="yes"}

1. 「**[!UICONTROL Select from Assets]**」をクリックして、カテゴリ画像を変更します。

   ![&#x200B; カテゴリコンテンツ &#x200B;](assets/asset-view.png){width="600" zoomable="yes"}

1. AEM アセットセレクターから画像を選択します。

   ![&#x200B; カテゴリコンテンツ &#x200B;](assets/select-image.png){width="600" zoomable="yes"}

1. 「**[!UICONTROL Save]**」をクリックして続行します。

   カテゴリの作成について詳しくは、&lbrace;2[Commerce Catalog Management Guide の &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-admin/catalog/categories/create/category-create#step-3-complete-the-category-content) カテゴリのコンテンツの入力 **を参照してください。**

## アセットの更新

AEM Assets内のアセットを更新して承認すると、自動一致機能を使用して、その更新内容がAdobe Commerceに自動的に送信されます。 このプロセスは、アセットの承認時にトリガーされます。 すべての最終的な変更とメタデータの更新が含まれるようにするには、必ずアセットを再処理してから承認してください。

詳しくは、次のAEM Assets ドキュメントを参照してください。

* [&#x200B; デジタルアセットの再処理 &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/assets/manage/reprocessing)

* [&#x200B; アセットの承認 &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/assets/dynamicmedia/dynamic-media-open-apis/approve-assets)
