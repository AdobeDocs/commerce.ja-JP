---
title: AEM Assets プロジェクトの設定
description: 統合に必要なメタデータを追加することで、Adobe CommerceとAEM Assetsの間でシームレスなアセット同期を可能にします。
feature: CMS, Media, Integration
exl-id: a5d2cbab-5ea1-446b-8ab2-2c638128a40c
source-git-commit: d46526db56dad08a8f865664c92d1214bbf063d8
workflow-type: tm+mt
source-wordcount: '846'
ht-degree: 0%

---

# Commerce メタデータをサポートするようにAEM Assets プロジェクトを設定します

AEM AssetsでCommerce アセットファイルを管理するには、次の手順を実行してAEM Assets プロジェクトにAEM オーサリング環境からCommerce アセットを管理するために必要なパッケージコードとメタデータを設定します。

## AEM Commerce `assets-commerce` パッケージコンテンツ

Adobeは、AEM Commerce環境設定にCommerce名前空間およびメタデータスキーマリソースを追加するためのExperience Manager Assets as a Cloud Service パッケージコード `assets-commerce` ードを提供します。

このパッケージコードは、次のリソースをAEM Assets オーサリング環境に追加します。

* Commerce関連のプロパティを識別するた [&#x200B; の &#x200B;](https://github.com/ankumalh/assets-commerce/blob/main/ui.config/jcr_root/apps/commerce/config/org.apache.sling.jcr.repoinit.RepositoryInitializer~commerce-namespaces.cfg.json) カスタム名前空間 `Commerce`。

   * Adobe Commerce プロジェクトに関連付けられたCommerce アセットにタグ付けするた `commerce:isCommerce` のラベルが付いたカスタムメタデータタイプ `Eligible for Commerce`。

   * カスタムメタデータタイプ `commerce:skus` と、**[!UICONTROL Product Data]** スタムプロパティを追加するための対応する UI コンポーネント。 商品データには、Commerce アセットを商品 SKU に関連付けるためのメタデータプロパティが含まれています。

     ![&#x200B; カスタム製品データ UI コントロール &#x200B;](../assets/aem-commerce-sku-metadata-fields-from-template.png){width="600" zoomable="yes"}

   * Commerceでのアセットのビジュアライゼーション方法を示すカスタムメタデータタイプ `commerce:roles` および `commerce:positions` の属性。

* Commerce アセットにタグ付けするための `Eligible for Commerce` フィールドと `Product Data` フィールドを含む、Commerce タブを持つメタデータスキーマフォーム このフォームには、AEM Assets UI の `roles` フィールドと `position` フィールドを表示または非表示にするオプションも用意されています。

  ![AEM Assets メタデータスキーマフォームの「Commerce」タブ &#x200B;](../assets/assets-configure-metadata-schema-form-editor.png){width="600" zoomable="yes"}

* 最初のアセットの同期をサポートするための [&#x200B; タグ付けされた承認済みCommerce アセット &#x200B;](https://github.com/ankumalh/assets-commerce/blob/main/ui.content/src/main/content/jcr_root/content/dam/wknd/en/activities/hiking/equipment_6.jpg/.content.xml) サンプル `equipment_6.jpg`。 AEM AssetsからAdobe Commerceに同期できるのは、承認済みのCommerce アセットのみです。

>[!NOTE]
>
> [2&rbrace;AEM Commerce パッケージコード &#x200B;](https://github.com/ankumalh/assets-commerce) について詳しくは、&lbrace;readme **ページを参照してください。**

### 前提条件

`assets-commerce` パッケージコードをAEM Assets as a Cloud Service AEM環境にデプロイするには、次のリソースと権限が必要です。

* プログラムおよびデプロイメントマネージャーの役割を使用して [AEM Assets Cloud Manager プログラムおよび環境にアクセス &#x200B;](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/onboarding/journey/cloud-manager#access-sysadmin-bo) します。

* [&#x200B; ローカル AEMローカル開発環境 &#x200B;](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview) およびAEM開発プロセスに精通していること。

* [AEM プロジェクト構造 &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/implementing/developing/aem-project-content-package-structure) およびCloud Managerを使用してカスタムコンテンツパッケージをデプロイする方法を理解します。

### 手順 1:`assets-commerce` パッケージのインストール

1. 必要に応じて、AEM Assets プロジェクトの [&#x200B; 実稼動環境とステージング環境の作成 &#x200B;](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/onboarding/journey/create-environments#creating-environments)AEM Cloud Managerから行います。

1. 必要に応じて、[&#x200B; デプロイメントパイプライン &#x200B;](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/sites/administering/site-creation/quick-site/pipeline-setup#create-front-end-pipeline) を設定します。

1. [Git リポジトリのクローンを作成 &#x200B;](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/sites/administering/site-creation/quick-site/retrieve-access#repo-access) します。

1. GitHub で、[AEM Assets Commerce リポジトリ &#x200B;](https://github.com/ankumalh/assets-commerce) からパッケージコードをダウンロードします。

1. [&#x200B; ローカル AEM開発環境 &#x200B;](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview) から、既存のプロジェクト設定にコードを手動でコピーし、`<my-app>` ージ内のすべての `filter.xml` と、プロジェクト内のすべての `pom.xml files` をアプリ名に置き換えます。

   >[!NOTE]
   >
   > または、カスタムコードを **Maven** パッケージとしてAEM Assets プロジェクト設定にインストールできます。

1. 変更をコミットし、ローカル開発ブランチをCloud Manager Git リポジトリにプッシュします。

1. AEM Cloud Managerから [&#x200B; コードをデプロイしてAEM環境を更新します &#x200B;](https://experienceleague.dobe.com/en/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code#deploying-code-with-cloud-manager)。

1. 変更を検証します。

   * デフォルトのメタデータスキーマには「**Commerce**」タブが含まれています。

   * 製品の SKU が正しく表示される。

問題が発生した場合は、[&#x200B; サポート &#x200B;](../overview.md#support) に記載されている手順に従ってください。

## オプション。 手順 2：メタデータプロファイルの設定

AEM Assets オーサー環境で、メタデータプロファイルを作成して、Commerce アセットメタデータのデフォルト値を設定します。 次に、新しいプロファイルをAEM Asset フォルダーに適用すると、これらのデフォルトが自動的に使用されます。 この設定により、手動の手順が減ることでアセット処理が合理化されます。

メタデータプロファイルを設定する場合、次のコンポーネントを設定するだけで済みます。

* 「Commerce」タブを追加します。 このタブでは、テンプレートによって追加されたCommerce固有の設定を有効にします。

* 「`Eligible for Commerce`」フィールドを「Commerce」タブに追加します。

テンプレートに基づいて、製品データ UI コンポーネントが自動的に追加されます。

### メタデータプロファイルの定義

1. Adobe Experience Manager オーサー環境にログインします。

1. Adobe Experience Manager Workspace から、Adobe Experience Manager アイコンをクリックして、AEM Assetsのオーサーコンテンツ管理ワークスペースに移動します。

   ![AEM Assetsの作成 &#x200B;](../assets/aem-assets-authoring.png){width="600" zoomable="yes"}

1. ハンマーアイコンを選択して、管理者ツールを開きます。

   ![AEM オーサー管理者によるメタデータプロファイルの管理 &#x200B;](../assets/aem-manage-metadata-profiles.png){width="600" zoomable="yes"}

1. 「**[!UICONTROL Metadata Profiles]**」をクリックして、プロファイル設定ページを開きます。

1. Commerce統合用のメタデータプロファイルを **[!UICONTROL Create]** 定します。

   ![AEM オーサー管理者によるメタデータプロファイルの追加 &#x200B;](../assets/aem-create-metadata-profile.png){width="600" zoomable="yes"}

1. Commerce メタデータ用のタブを追加します。

   1. 左側で、「**[!UICONTROL Settings]**」をクリックします。

   1. タブ セクションの [**[!UICONTROL +]**] をクリックし、**[!UICONTROL Tab Name]**、`Commerce` を指定します。

1. `Eligible for Commerce` フィールドをフォームに追加します。

   ![AEM オーサー管理者のプロファイルにメタデータフィールドを追加 &#x200B;](../assets/aem-edit-metadata-profile-fields.png){width="600" zoomable="yes"}

   * 「**[!UICONTROL Build form]**」をクリックします。

   * 「`Single Line text`」フィールドをフォームにドラッグします。

   * 「」をクリックして、ラベルの `Eligible for Commerce` のテキストを追加 **[!UICONTROL Field Label]** ます。

   * 「設定」タブで、ラベルテキストを **フィールドラベル** に追加します。

   * プレースホルダーテキストを `yes` に設定します。

   * **[!UICONTROL Map to Property]** フィールドで、次の値をコピーして貼り付けます

     ```terminal
     ./jcr:content/metadata/commerce:isCommerce
     ```

1. オプション。 承認済みのCommerce アセットをAEM Assets環境にアップロードする際に自動的に同期させるには、「_[!UICONTROL Review Status]_」タブの「`Basic`」フィールドのデフォルト値を `approved` に設定します。

1. 更新を保存します。

#### メタデータプロファイルのCommerce assets ソースフォルダーへの適用

1. [!UICONTROL &#x200B; Metadata Profiles] ページで、「Commerce統合」プロファイルを選択します。

1. アクションメニューから「**[!UICONTROL Apply Metadata Profiles to Folders]**」を選択します。

1. Commerce アセットを含むフォルダーを選択します。

   Commerce フォルダーが存在しない場合は作成します。

1. 「**[!UICONTROL Apply]**」をクリックします。

## 次の手順

* [!BADGE PaaS のみ &#x200B;]{type=Informative tooltip="クラウドプロジェクト上のAdobe Commerceにのみ適用されます（Adobeが管理する PaaS インフラストラクチャ）。"}Adobe Commerce パッケ [&#x200B; ジのインストール &#x200B;](configure-commerce.md)

* **Commerce ストアフロントの設定** - Edge Delivery Servicesを搭載したCommerce Storefront でAEM Assetsを使用するには、「[EDS AEM Assets設定 &#x200B;](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/aem-assets-configuration/)」トピックで説明されているストアフロント設定を行います。
