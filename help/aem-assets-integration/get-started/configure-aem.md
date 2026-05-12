---
title: Commerce メタデータをサポートするようにAEM Assets プロジェクトを設定する
description: Adobe CommerceとAEM Assetsの間で、アセットの統合に必要なメタデータを追加することで、シームレスなアセット同期を実現します。
feature: CMS, Media, Integration
exl-id: a5d2cbab-5ea1-446b-8ab2-2c638128a40c
TQID: https://experienceleague.adobe.com/QPlM-eeRjJ0gwmpGO4SSYR4PLtL97O-NeozWorDWtv0
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: da3860b0-d637-47df-bef0-273751180266
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 33cd0e217447351b690646ec8d230f76060a74da
workflow-type: tm+mt
source-wordcount: 1450
ht-degree: 1%

---

# Commerce メタデータをサポートするようにAEM Assets プロジェクトを設定する

AEM AssetsをCommerceのデジタルアセット管理システム （DAM）として使用する場合、`assets-commerce` パッケージをインストールすると、AEM オーサリング環境からCommerce製品の画像とビデオを管理できます。

AEM オーサリング環境からAEM Assets アセットを管理するために必要なパッケージコードとメタデータを使用してCommerce プロジェクトを設定するには、次の手順を実行します。

1. [`assets-commerce` パッケージの内容について説明します](#aem-commerce-assets-commerce-package-contents)

1. [Commerce メタデータをサポートするようにAEM Assets プロジェクトを設定するには、インストール手順を実行します](#step-1-install-the-assets-commerce-package)

## AEM Commerce assets-commerce パッケージの内容

Adobeは、Experience Manager Assets as a Cloud Service環境設定にCommerce名前空間およびメタデータスキーマリソースを追加するためのAEM Commerce パッケージコード `assets-commerce`を提供します。

このパッケージコードは、次のリソースをAEM Assets オーサリング環境に追加します。

* Commerce関連のプロパティを識別するための[&#x200B; カスタム名前空間](https://github.com/ankumalh/assets-commerce/blob/main/ui.config/jcr_root/apps/commerce/config/org.apache.sling.jcr.repoinit.RepositoryInitializer~commerce-namespaces.cfg.json)、`Commerce`。

   * Adobe Commerce プロジェクトに関連付けられたCommerce アセットにタグ付けするためのラベル `Eligible for Commerce`を持つカスタムメタデータタイプ `commerce:isCommerce`。

   * カスタムメタデータタイプ `commerce:skus`と、対応するUI コンポーネントを使用して&#x200B;**[!UICONTROL Product Data]** プロパティを追加します。 商品データには、Commerce アセットを商品SKUに関連付けるためのメタデータプロパティが含まれています。

     ![&#x200B; カスタム製品データ UI コントロール &#x200B;](../assets/aem-commerce-sku-metadata-fields-from-template.png){width="600" zoomable="yes"}

   * Commerceでのアセットのビジュアライゼーション方法を示すカスタムメタデータタイプ `commerce:roles`と`commerce:positions`属性。

* Commerce アセットのタグ付け用の`Eligible for Commerce`および`Product Data` フィールドを含むCommerce タブを持つメタデータスキーマフォーム。 このフォームには、AEM Assets UIから`roles`および`position` フィールドを表示または非表示にするオプションも用意されています。

  ![AEM Assets メタデータスキーマフォームの「Commerce」タブ &#x200B;](../assets/assets-configure-metadata-schema-form-editor.png){width="600" zoomable="yes"}

* 最初のアセットの同期をサポートするために、[&#x200B; サンプルにタグ付けして承認されたCommerce アセット &#x200B;](https://github.com/ankumalh/assets-commerce/blob/main/ui.content/src/main/content/jcr_root/content/dam/wknd/en/activities/hiking/equipment_6.jpg/.content.xml) `equipment_6.jpg`が含まれています。 AEM AssetsからAdobe Commerceに同期できるのは、承認済みのCommerce アセットのみです。

>[!NOTE]
>
> **AEM Commerce パッケージコード**&#x200B;の詳細については、[readme](https://github.com/ankumalh/assets-commerce) ページを参照してください。

## 前提条件

`assets-commerce` パッケージコードをAEM Assets as a Cloud Service AEM環境にデプロイするには、次のリソースと権限が必要です。

* プログラムおよびデプロイメント マネージャーの役割を持つ[AEM Assets Cloud Manager プログラムおよび環境](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/onboarding/journey/cloud-manager#access-sysadmin-bo)へのアクセス。

* [&#x200B; ローカル ローカル開発環境](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview)と、AEM開発プロセスに関する知識。

* [AEM プロジェクト構造](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/implementing/developing/aem-project-content-package-structure)と、Cloud Managerを使用してカスタムコンテンツパッケージをデプロイする方法について説明します。

* Commerce インスタンスの&#x200B;**IMS組織ID**。 Commerce インスタンスとAEM Assets オーサリング環境の両方が同じIMS組織にある必要があります。

* OpenAPI機能を使用して[Dynamic Mediaを有効にするには](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/dynamicmedia/dynamic-media-open-apis/dynamic-media-open-apis-overview#enable-dynamic-media-open-apis):

>[!BEGINTABS]

>[!TAB 製品ビジュアル ]

OpenAPI機能を備えた[!BADGE SaaSのみ]{type=Positive url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud ServiceおよびAdobe Commerce Optimizer プロジェクト（Adobeが管理するSaaS インフラストラクチャ）にのみ適用されます。"}のDynamic Mediaは、AEM Assetsを活用した商品ビジュアルのセルフサービスです。

1. Cloud Managerに移動します。

1. 目的の環境を選択します。

1. OpenAPI機能を使用して&#x200B;**Dynamic Mediaを有効にする**。

   OpenAPI機能を備えた&#x200B;**Dynamic Media** ボタンがアクティブでない場合は、サポートチケットを開きます。

>[!TAB AEM Assets]

[!BADGE PaaSのみ]{type=Informative tooltip="Cloud プロジェクト上のAdobe Commerce（Adobeで管理されるPaaS インフラストラクチャ）にのみ適用されます。"} AEM as a Cloud Serviceで、次の情報を記載したAdobe サポートチケットを送信します。

* タイトル：Dynamic Media OpenAPIを有効にして、Adobe CommerceとAEM Assetsを完全に統合する

   * サポートチケットの内容：

      * **[!UICONTROL AEM Program ID]**
      * **[!UICONTROL Adobe Commerce URL]**
      * **[!UICONTROL AEM Environment ID]**
      * **[!UICONTROL IMS Org ID]**

サポートチケットを送信すると、AdobeはCloud Services環境でOpenAPI機能を備えたDynamic Mediaを有効にし、IMS クライアント IDなどの詳細を共有して、統合を進めることができます。

>[!ENDTABS]

## 手順1:assets-commerce パッケージのインストール

1. AEM Cloud Managerに移動し、プログラムを選択し、Adobe Commerceと統合する実稼動環境とステージング環境を[作成します](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/onboarding/journey/create-environments#creating-environments)。

1. [&#x200B; デプロイメントパイプライン &#x200B;](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/sites/administering/site-creation/quick-site/pipeline-setup#create-front-end-pipeline)を設定するか、パイプラインが選択した環境に変更をデプロイできることを確認します。

1. [選択したプログラムのAdobe管理Git リポジトリ &#x200B;](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/sites/administering/site-creation/quick-site/retrieve-access#repo-access)を複製します。

1. GitHubから、[AEM Assets Commerce リポジトリ &#x200B;](https://github.com/ankumalh/assets-commerce)からパッケージコードをダウンロードします。

1. [&#x200B; ローカルのAEM開発環境](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview)から、ダウンロードしたコードを既存のAdobe管理リポジトリに手動でコピーします。

1. プロジェクトのすべての`filter.xml`と`pom.xml files`で、`<my-app>`のすべての出現箇所をアプリ名に置き換えます。

>[!NOTE]
>
> または、カスタムコードを&#x200B;**Maven** パッケージとしてAEM Assets プロジェクト設定にインストールすることもできます。

1. 変更を確定し、ローカル開発ブランチをCloud Manager Git リポジトリにプッシュします。

1. AEM Cloud Managerから、[&#x200B; パイプラインを使用してコードをデプロイし、AEM環境を更新します](https://experienceleague.dobe.com/en/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code#deploying-code-with-cloud-manager)。

1. 任意のアセットに移動し、そのプロパティを編集して変更を検証します。

   * デフォルトのメタデータスキーマには、「**Commerce**」タブが含まれています。

   * 製品SKUと`Eligible for Commerce` フィールドが表示されます。

### 「Commerce」タブがプロパティに表示されない

**Commerce** タブがプロパティに表示されない場合は、メタデータスキーマエディターでタブを手動で作成する必要があります。

1. メタデータスキーマエディターに移動します。

1. **編集**&#x200B;をクリックして、デフォルトのメタデータスキーマフォームを変更します。

1. 「**Commerce**」タブを作成し、選択します。

1. **Product** コンポーネントを&#x200B;**Commerce** タブにドラッグ&amp;ドロップし、プロパティ `commerce:skus`にマッピングします。

1. **役割を表示**&#x200B;および&#x200B;**順序を表示**&#x200B;のチェックボックスを選択します。

1. **checkbox** コンポーネントを&#x200B;**Commerce** タブにドラッグ&amp;ドロップし、プロパティ `commerce:isCommerce`にマッピングします。 オプションとして&#x200B;**Yes**&#x200B;と&#x200B;**No**&#x200B;を定義します。

その他の問題が発生した場合は、[&#x200B; サポートチケット &#x200B;](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket)を作成するか、AEM Assets Integrationの営業担当者にお問い合わせください。

## 手順2：オプション。 メタデータプロファイルの設定

AEM Assets オーサー環境で、メタデータプロファイルを作成して、Commerce アセットメタデータのデフォルト値を設定します。 次に、新しいプロファイルをAEM Asset フォルダーに適用して、これらのデフォルトを自動的に使用します。 この設定により、手作業を削減してアセット処理が合理化されます。

メタデータプロファイルを設定する場合、次のコンポーネントのみを設定する必要があります。

* 「Commerce」タブを追加します。 このタブでは、テンプレートによって追加されたCommerce固有の設定を有効にします。

* 「`Eligible for Commerce`」フィールドを「Commerce」タブに追加します。

製品データ UI コンポーネントは、テンプレートに基づいて自動的に追加されます。

### メタデータプロファイルの定義

1. Adobe Experience Manager オーサー環境にログインします。

1. Adobe Experience Manager ワークスペースから、「Adobe Experience Manager」アイコンをクリックして、AEM Assetsのコンテンツ管理ワークスペースを作成します。

   ![AEM Assets オーサリング &#x200B;](../assets/aem-assets-authoring.png){width="600" zoomable="yes"}

1. ハンマーアイコンを選択して、管理者ツールを開きます。

   ![AEM オーサー管理者管理メタデータプロファイル &#x200B;](../assets/aem-manage-metadata-profiles.png){width="600" zoomable="yes"}

1. **[!UICONTROL Metadata Profiles]**&#x200B;をクリックして、プロファイル設定ページを開きます。

1. Commerce統合用のメタデータプロファイル **[!UICONTROL Create]**。

   ![AEM オーサー管理者メタデータプロファイルを追加](../assets/aem-create-metadata-profile.png){width="600" zoomable="yes"}

1. Commerce メタデータのタブを追加します。

   1. 左側で、**[!UICONTROL Settings]**&#x200B;をクリックします。

   1. タブ セクションの&#x200B;**[!UICONTROL +]**&#x200B;をクリックし、**[!UICONTROL Tab Name]**、`Commerce`を指定します。

1. フォームに`Eligible for Commerce` フィールドを追加します。

   ![AEM オーサー管理者がメタデータ フィールドをプロファイルに追加](../assets/aem-edit-metadata-profile-fields.png){width="600" zoomable="yes"}

   * **[!UICONTROL Build form]**&#x200B;をクリックします。

   * `Single Line text` フィールドをフォームにドラッグします。

   * **[!UICONTROL Field Label]**&#x200B;をクリックして、ラベルの`Eligible for Commerce` テキストを追加します。

   * 「設定」タブで、「**フィールドラベル**」にラベルテキストを追加します。

   * プレースホルダーテキストを`yes`に設定します。

   * **[!UICONTROL Map to Property]** フィールドに、次の値をコピーして貼り付けます

     ```terminal
     ./jcr:content/metadata/commerce:isCommerce
     ```

1. オプション。 承認済みのCommerce アセットをAEM Assets環境にアップロードするときに自動的に同期させるには、`Basic` タブの&#x200B;_[!UICONTROL Review Status]_&#x200B;フィールドのデフォルト値を`approved`に設定します。

1. アップデートを保存します。

### メタデータプロファイルをCommerce assets ソースフォルダーに適用する

1. 「[!UICONTROL &#x200B; Metadata Profiles]」ページで、「Commerce統合プロファイル」を選択します。

1. アクションメニューから、**[!UICONTROL Apply Metadata Profiles to Folders]**&#x200B;を選択します。

1. Commerce アセットを含むフォルダーを選択します。

   Commerce フォルダーが存在しない場合は作成します。

1. **[!UICONTROL Apply]**&#x200B;をクリックします。

## 次のステップ

* [!BADGE PaaSのみ]{type=Informative tooltip="Cloud プロジェクト上のAdobe Commerce（Adobeで管理されるPaaS インフラストラクチャ）にのみ適用されます。"} [Adobe Commerce パッケージをインストール &#x200B;](configure-commerce.md)。

* [!BADGE SaaSのみ]{type=Positive url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud ServiceおよびAdobe Commerce Optimizer プロジェクト（Adobeが管理するSaaS インフラストラクチャ）にのみ適用されます。"} [Commerce Admin](setup-synchronization.md)から統合を設定します。
