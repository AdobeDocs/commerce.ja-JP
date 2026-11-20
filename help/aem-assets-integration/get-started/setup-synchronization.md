---
title: 統合の設定
description: Adobe Commerce プロジェクトとExperience Manager Assets プロジェクトを接続して、これらの2つのシステム間でアセットを同期する方法を説明します。
feature: CMS, Media
exl-id: 3533d010-926f-4d78-935c-98a9b7040d27
TQID: 'https://experienceleague.adobe.com/MM-neGrH-N8xBcCwLgnsaIrIjhbX6uYL5kS41QdV79I'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
  - id: ddbd0f6e-b569-5a04-8a70-55058777c373
    internal-label: CMS
  - id: 4ca54350-01cb-5b22-8966-5f2873dc6d90
    internal-label: Media
subfeature_v2:
  - id: ae62cf09-5996-4921-bda8-fbe67b62e470
    internal-label: Storefront configuration
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
    internal-label: Metadata
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
source-git-commit: 5e9c42e5c93ac81604aa38bf3e55c5df729650a0
workflow-type: tm+mt
source-wordcount: '1355'
ht-degree: 1%
---
# 統合の設定

CommerceをAEM Assets インスタンスに接続し、アセットの同期に一致する方法を選択して、統合を設定します。

AEM Assets プロジェクトを特定したら、Adobe CommerceとAEM Assets間でアセットを同期するための一致するルールを選択します。

* **[!UICONTROL Match by product SKU]** - アセットが正しい商品に関連付けられていることを確認するために、アセットメタデータのSKUと[Commerce商品SKU](https://experienceleague.adobe.com/en/docs/commerce-operations/implementation-playbook/glossary#sku)を一致させるデフォルトのルール。

* **[!UICONTROL Custom match]** – より複雑なシナリオまたはカスタム一致ロジックを必要とする特定のビジネス要件の一致ルール。 カスタムマッチングを実装するには、Adobe Developer App Builderでカスタムコードを開発して、アセットと商品のマッチング方法を定義する必要があります。 [自動マッチングのカスタム ](../synchronize/custom-match.md)を参照してください。

初期設定では、デフォルトの&#x200B;**[!UICONTROL Match by product SKU]** ルールを使用します。

## 要件定義

AEM Assets統合を設定する前に、次の手順を完了していることを確認します。

* [AEM Assets プロジェクトの設定](configure-aem.md)

* [!BADGE PaaSのみ]{type=Informative tooltip="Cloud プロジェクト上のAdobe Commerce（Adobeで管理されるPaaS インフラストラクチャ）にのみ適用されます。"} [Adobe Commerce パッケージ ](configure-commerce.md)をインストールして拡張機能を追加し、拡張機能を使用するために必要な資格情報と接続を生成します。

* [ ユーザー権限とIMS](permissions.md) - アセットセレクター、AEM環境の選択、ドメインマッピングに必要な権限を設定します。

## 接続の設定

![環境とドメイン値の例を含むAEM Assets統合設定](../assets/aem-assets-view.png){width="900" zoomable="yes"}

1. Commerce管理者から、**[!UICONTROL Stores]** > **[!UICONTROL Settings]** > **[!UICONTROL Configuration]** > **[!UICONTROL ADOBE SERVICES]** > **[!UICONTROL AEM Assets Integration]**&#x200B;に移動します。

>[!INFO]
>
> AEM Assets統合では、グローバル（デフォルト）スコープでの設定のみがサポートされます。 Web サイトレベルの設定はサポートされていません。 Web サイトレベルで統合を設定しようとすると、システムはweb サイトレベルの設定を無視し、代わりにグローバル設定値を使用します。

1. [!BADGE PaaSのみ]{type=Informative tooltip="Cloud プロジェクト上のAdobe Commerce（Adobeで管理されるPaaS インフラストラクチャ）にのみ適用されます。"} 「**[!UICONTROL Asset Selector IMS Client ID]**」を入力します。

   アセットセレクターを有効にするには、このIDが必要です。 このIDを取得するには、[ ユーザー権限とIMS](permissions.md)を参照してください。 アセットセレクターについて詳しくは、[ アセットの手動選択](../synchronize/asset-selector-integration.md)を参照してください。

1. **[!UICONTROL AEM Environment]**&#x200B;から、[AEM Assets プロジェクトの設定](configure-aem.md)で設定された環境を選択します。

   このリストには、ユーザーがオーサーまたは配信製品プロファイルを持つAEM環境が含まれます。 想定される環境が見つからない場合は、[ ユーザー権限とIMS](permissions.md)を確認してください。

   代わりに、設定に&#x200B;**[!UICONTROL Program ID]**&#x200B;と&#x200B;**[!UICONTROL Environment ID]**&#x200B;のフィールドが別々に表示される場合は、その環境の識別子を指定します。 手動入力の場合は、AEM Cloud Managerからコピーするか、作成者URL `https://author-p<ProgramID>-e<EnvironmentID>.adobeaemcloud.com/`から派生させます。 `p`と`e`のプレフィックスを含まない数値識別子のみを入力します。

   **[!UICONTROL Use system value]** チェックボックスを含むフィールドの場合は、デフォルト値を上書きする前にチェックボックスをオフにします。

1. **[!UICONTROL AEM Domain Mapping]**&#x200B;を確認してください。 選択したAEM環境に基づいて、使用可能なドメインが自動的に読み込まれます。 プロジェクトでカスタムアセット配信ドメインを使用している場合は、[ カスタムドメイン URLの設定](#optional-configure-the-custom-domain-url)に従います。

1. [!BADGE PaaSのみ]{type=Informative tooltip="Cloud プロジェクト上のAdobe Commerce（Adobeで管理されるPaaS インフラストラクチャ）にのみ適用されます。"} Commerceとアセットマッチングサービス間のリクエストを認証する[[!UICONTROL Commerce integration]](configure-commerce.md#add-the-integration-to-the-commerce-environment)を選択します。

1. **[!UICONTROL Synchronization enabled]**&#x200B;を`Yes`に設定して、CommerceがAEM Assetsからの受信アップデートを受け入れるようにします。

   統合を有効にすると、アセットの一致条件を指定するための追加の設定オプションが使用できるようになります。

1. **[!UICONTROL Asset matching rule]** ドロップダウンから、アセット同期用のアセット一致ルールのいずれかを選択します。

   * [既定の自動一致](../synchronize/default-match.md)に対して&#x200B;**[!UICONTROL Match by product SKU]**&#x200B;を選択します。
   * [ カスタム自動一致](../synchronize/custom-match.md)の&#x200B;**[!UICONTROL Custom match]**&#x200B;を選択します。 このオプションには[Adobe Developer App Builder](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/extensibility/adobe-developer-app-builder/introduction-to-app-builder)が必要です。

1. **[!UICONTROL Match by product SKU]**&#x200B;の場合、**[!UICONTROL Match by product SKU attribute name]** フィールドに[AEM Assets メタデータプロパティ名](../metadata.md)を入力します。 デフォルトは`commerce:skus`です。

   製品のSKU値ではなく、プロパティ名を入力します。 [ デフォルトの自動一致](../synchronize/default-match.md)の説明に従って、AEM Assetsの各アセットの&#x200B;**[!UICONTROL Product Data]** メタデータに実際の商品SKUを追加します。

1. [ ビジュアライゼーション所有者](#configure-the-visualization-owner)の設定を確認します。 移行中は、アセットの同期が完了するまで&#x200B;**Adobe Commerce**&#x200B;の所有権を保持します。

1. **[!UICONTROL Save Config]**&#x200B;を選択して更新を適用し、アセットの同期を開始します。

   設定の更新により、最初の同期プロセスがトリガーされ、CommerceはAEM Assetsからの受信アップデートを受け入れることができます。 同期に必要な時間は、アセットの量と特定の設定によって異なります。 統合では、自動化されたプロセスを活用して、同期に必要な時間を最小限に抑えます。

### Synchronization SLA

統合用のservice level agreement（SLA）では、次の同期パフォーマンスレベルが保証されます。

* `< 5 minutes for 99% of updates`

* `< 30 minutes for 99.9% of updates`

このレベルのサービスにより、商品ページは常に最新の画像を表示できるようになり、ストアフロントコンテンツを正確で視覚的に魅力的なものに保つことができます。

## ローカライズされたalt テキストの同期

ローカライズされたalt テキストは、既存のアセット同期プロセスを使用します。 新しいイベントタイプや個別の同期設定は必要ありません。

1. AEM アセットの&#x200B;**[!UICONTROL Commerce]** タブに1つ以上のstore-view alt-text行を追加します。

1. アセットをCommerceの商品SKUに関連付けます。

1. AEM Assetsでアセットを承認します。

1. アセットイベントと同期プロセスが完了するのを待ちます。

1. Commerce管理者とストアフロントのレスポンスで、ローカライズされた値を確認します。

フィールド名、検証ルールおよびCommerceの結果については、[AEM AssetsのCommerce メタデータ ](../metadata.md)を参照してください。

## ビジュアライゼーション所有者の設定

**ビジュアライゼーション所有者**&#x200B;の設定により、統合で製品イメージを提供するシステムが決まります。

* Adobe Commerce - Commerceでホストされている画像を使用します。

* AEM Assets - AEMから同期された画像を使用します。

管理者はその所有者の利用可能な画像を表示し、残りの画像はグレー表示され、**非表示** ラベルが付いて表示されます。

画像の表示動作について詳しくは、[画像の詳細を設定](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/products/digital-assets/product-image#set-image-details){target=_blank} トピックを参照してください。

>[!TIP]
>
> CommerceからAEM Assetsへの移行中に、**Visualization Owner**&#x200B;をCommerceに設定して、画像リンクの破損を防ぎます。 すべての製品がAEM Assetsと正常に同期されたら、AEM Assets オーナーに切り替えて移行を完了します。 これにより、プロセス全体で画像の可用性を継続的に確保できます。

1. **[!UICONTROL Stores]** > **[!UICONTROL Settings]** > **[!UICONTROL Configuration]** > **[!UICONTROL ADOBE SERVICES]** > **[!UICONTROL AEM Assets Integration]**&#x200B;に移動します。

   ![ ビジュアライゼーション所有者がAEM Assets](../assets/visualization-owner-detail.png){width="700" zoomable="yes"}に設定されました

1. 画像を表示するには、**ビジュアライゼーション所有者** ソースを選択します。

1. **[!UICONTROL Save Config]**&#x200B;をクリックして更新を適用します。

   **AEM Assets**&#x200B;に切り替える前に、[ アセットが予想される製品](#verify-the-integration)に関連付けられていることを確認してください。 次に、[AEM Assetsの商品画像を表示するようにストアフロント ](configure-storefront.md)を設定します。

## オプション。 カスタムドメイン URLの設定

AEM Assets as a Cloud Service プロジェクトに[ カスタムドメイン名](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/custom-domain-names/add-custom-domain-name){target=_blank}が設定されている場合は、Commerce用のAEM Assets統合で使用できるように、Commerce ストア設定にドメイン名を追加する必要があります。

AEM管理者から、設定されたasset-delivery カスタムドメイン URLを取得します。 この設定は、AEM配信URLに代わるもので、プログラム IDと環境IDの識別に使用されるAEM オーサーURLではありません。 プロジェクトでカスタムドメインを使用しない場合は、ドメインマッピングは変更しないでください。

>[!NOTE]
>
>カスタムドメイン URLを設定しても、以前に同期されたアセットのURLは更新されません。 これらのアセットは、AEM Assets](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/manage/reprocessing){target=_blank}で[再処理されるまで、以前のURLを保持します。 カスタムドメイン設定を保存したら、これらのアセットを再処理してURLを更新し、カスタムドメインを使用します。

1. **[!UICONTROL Stores]** > **[!UICONTROL Settings]** > **[!UICONTROL Configuration]** > **[!UICONTROL ADOBE SERVICES]** > **[!UICONTROL AEM Assets Integration]**&#x200B;に移動します。

1. 選択した&#x200B;**[!UICONTROL AEM Environment]**&#x200B;を確認してから、**[!UICONTROL AEM Domain Mapping]**&#x200B;から設定済みのカスタムドメインを選択します。 選択した環境で使用可能なドメインが自動的に読み込まれます。

![AEM環境およびドメインセレクターと値の例](../assets/aem-assets-environment-domain.png){width="700" zoomable="yes"}

    代わりに**[!UICONTROL Asset Custom Domain]** テキストフィールドを表示する設定の場合は、カスタムドメイン URLをそのフィールドに入力します。

1. **[!UICONTROL Save Config]**&#x200B;をクリックして更新を適用します。

## 統合の検証

>[!NOTE]
>
>Sync StatusはAdobe Commerce Optimizerでは使用できません。 以下のCommerce管理者チェックの代わりに、[Commerce Optimizerの検証ワークフロー](configure-aco.md#match-by-sku-workflow-example)に従います。

1. 既存のCommerce製品を選択し、そのSKUを書き留めます。

1. AEM Assetsで、テストアセットを&#x200B;**[!UICONTROL Eligible for Commerce]**&#x200B;としてマークし、その商品SKUに関連付け、その役割とポジションを設定します。 アセットを承認します。 [既定の自動一致](../synchronize/default-match.md)を参照するか、設定済みの[ カスタム一致ルール ](../synchronize/custom-match.md)を使用してください。

1. 同期が完了したら、Commerce Adminで製品を開き、関連するアセット、ロール、およびポジションについて&#x200B;**[!UICONTROL Images And Videos]** セクションを確認します。 [ アセットの管理](../manage-assets.md)を参照してください。

1. アセットの同期結果については、[同期ステータス ](sync-status.md)を確認してください。 同期が失敗した場合は、**[!UICONTROL Error]**&#x200B;列を確認してください。

1. ビジュアライゼーションオーナーとして&#x200B;**AEM Assets**&#x200B;を選択し、[ ストアフロント設定](configure-storefront.md)を完了した後、ストアフロントで商品を開き、予想される画像が表示されることを確認します。

[!BADGE PaaSのみ]{type=Informative tooltip="Cloud プロジェクト上のAdobe Commerce（Adobeで管理されるPaaS インフラストラクチャ）にのみ適用されます。"}その他の同期のトラブルシューティングについては、[統合ログ ](logs.md)を確認してください。

## 次のステップ

* [Edge Delivery Servicesを使用してAEM Assetsの商品画像を表示するように、Commerce ストアフロント ](configure-storefront.md)を設定します。

* Adobe CommerceとAEM Assets統合の間で[一致するルール ](../synchronize/default-match.md)を設定します。

* [Commerce アセットの管理](../manage-assets.md)。
