---
title: AEM Assets プロジェクトの設定
description: assets-commerce パッケージをデプロイし、AEM プロジェクトでAdobe Commerce メタデータを設定することで、CommerceとAEM Assets間でアセットを同期する方法について説明します。
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
source-git-commit: 0c2e50338cbf286704239b6d1f628180e85a3bef
workflow-type: tm+mt
source-wordcount: 1741
ht-degree: 1%

---

# AEM Assets プロジェクトの設定

ここでは、「AEM Assetsの名前空間」、「メタデータスキーマ」、「[!UICONTROL Commerce]」タブをAEM オーサリング環境で使用できるように、Commerce プロジェクトを設定する方法について説明します。 これらのリソースの背景については、[AEM AssetsのCommerce メタデータ &#x200B;](../metadata.md)を参照してください。

AEM Assets プロジェクトを設定するには、次の2つのオプションがあります。

* [!BADGE 推奨]{type=Positive} **セルフサービス オンボーディング** — AEM リリース `2026.5.26309`以降では、環境変数を設定し、OpenAPI機能を使用してDynamic Mediaをアクティブ化することで、Cloud Managerでの統合を有効にします。 カスタムコードのデプロイメントは必要ありません。 [Commerce統合（セルフサービス）を有効にする](#enable-aem-commerce-self-service)を参照してください。

* **手動設定** — Cloud Manager パイプラインを使用して`assets-commerce` パッケージをデプロイします。 カスタムパッケージコードをデプロイする必要がある場合、または`2026.5.26309`より前のAEM リリースを使用している場合は、これらの手動ステップを使用します。 [Assets-commerce パッケージを手動でインストールする](#install-the-assets-commerce-package-manually)を参照してください。

>[!TIP]
>
>現在のAEM バージョンは、右上のメニュー（**[!UICONTROL Help]** > **[!UICONTROL About AEM]**）から確認できます。

## Commerce統合（セルフサービス）を有効にする {#enable-aem-commerce-self-service}

[!BADGE &#x200B; サポート対象]{type=Informative tooltip="サポート対象"} AEM リリース `2026.5.26309`以降。

サポートされているAEM リリースでは、カスタムコードをデプロイせずに、Cloud ManagerからのCommerce統合を有効にします。 Commerceの名前空間、メタデータスキーマ、および&#x200B;**[!UICONTROL Commerce]** タブは、オーサーサービスでの統合を有効にすると自動的にプロビジョニングされます。

### セルフサービスの前提条件

* プログラムおよびデプロイメント マネージャーの役割を持つ[AEM Cloud Manager プログラムおよび環境](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/onboarding/journey/cloud-manager#access-sysadmin-bo)へのアクセス。

* リリース `2026.5.26309`以降のAEM プログラム。

* Commerce インスタンスの&#x200B;**IMS組織ID**。

  Commerce インスタンスとAEM Assets オーサリング環境の両方が同じIMS組織にある必要があります。

### 手順1：プログラムと環境の作成

Cloud Managerでのプログラムの作成は、1つのウィザードプロセスです。プログラムとその環境は、複数の手順で設定され、最後にまとめて保存されます。

1. Cloud Managerで、**[!UICONTROL Add Program]**&#x200B;を選択します。

1. **[!UICONTROL Set up for production]**&#x200B;を選択し、プログラム名を入力してから、**[!UICONTROL Continue]**&#x200B;を選択します。

1. **[!UICONTROL Solutions & Add-ons]** ステップで、**[!UICONTROL Dynamic Media]**&#x200B;を含め、プロジェクトに必要なソリューションとアドオンを選択し、**[!UICONTROL Continue]**&#x200B;を選択します。

   ![Dynamic Mediaを選択したCloud Manager ソリューションとアドオンの手順](../assets/aem-cloud-manager-program-addons.png){width="600" zoomable="yes"}

1. **[!UICONTROL Add Environment]** ステップで、**実稼動**&#x200B;および&#x200B;**ステージング**&#x200B;環境の名前を入力し、地域を選択します。

   ![実稼動環境とステージの詳細を含むCloud Manager Add environment ダイアログ &#x200B;](../assets/aem-cloud-manager-add-environment.png){width="600" zoomable="yes"}

1. 環境を使用してプログラムを作成するには、**[!UICONTROL Save]**&#x200B;を選択します。

### 手順2:Commerce統合変数を有効にする

Cloud Managerで、手順1で作成した環境を開き、次の操作を行います。

1. 「**[!UICONTROL Configuration]**」タブを選択します。

1. 次の値を持つ環境変数を追加し、**[!UICONTROL Add]**&#x200B;と&#x200B;**[!UICONTROL Save]**&#x200B;を選択します。

   | フィールド | 値 |
   |---|---|
   | 名前 | `COMMERCE_INTEGRATION_ENABLED` |
   | 値 | `true` |
   | 適用されたサービス | オーサー |
   | タイプ | 変数 |

   ![COMMERCE_INTEGRATION_ENABLED変数がオーサーサービスに適用されたCloud Manager環境設定](../assets/aem-cloud-manager-commerce-integration-variable.png){width="600" zoomable="yes"}

   環境が更新され、設定が適用されます。 環境ステータスが&#x200B;**[!UICONTROL Running]**&#x200B;に戻るまで待ちます。

### 手順3:OpenAPI機能を使用したDynamic Mediaのアクティベーション

1. 環境&#x200B;**[!UICONTROL General]** タブで、**[!UICONTROL Dynamic Media]**&#x200B;を見つけます。

1. *OpenAPI機能の横にある*&#x200B;を選択します。**[!UICONTROL Click to activate]**

   ![Dynamic Media OpenAPI アクティベーションリンクを表示する「環境一般」タブ &#x200B;](../assets/aem-cloud-manager-dynamic-media-activate.png){width="600" zoomable="yes"}

   アクティベーションはバックグラウンドで実行されます。 完了すると、Commerceとの連携の準備が整います。

   >[!NOTE]
   >
   > **[!UICONTROL Click to activate]**&#x200B;が利用できない場合は、サポートチケットを開いて、OpenAPI機能を備えたDynamic Mediaを有効にします。

### 手順4：設定の検証

**AEM Assets オーサー環境**&#x200B;に切り替えて、任意のアセットを開きます。 プロパティを編集し、デフォルトのメタデータスキーマに「**[!UICONTROL Commerce]**」タブが含まれており、**[!UICONTROL Product Data]**&#x200B;および&#x200B;**[!UICONTROL Eligible for Commerce]** フィールドが表示されていることを確認します。

## assets-commerce パッケージの手動インストール

>[!NOTE]
>
> カスタムパッケージコードをデプロイする場合や、`2026.5.26309`より前のAEM リリースを使用している場合は、この手動メソッドを使用します。 サポートされているリリースでは、代わりに[Commerce統合を有効にする（セルフサービス） &#x200B;](#enable-aem-commerce-self-service)を使用してください。

### 前提条件

`assets-commerce` パッケージ コードをAEM Assets as a Cloud Service AEM環境にデプロイするには、次のリソースと権限が必要です。

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

* タイトル：Dynamic Media OpenAPIを有効にして、Adobe CommerceをAEM Assetsと完全に統合する

   * サポートチケットの内容：

      * **[!UICONTROL AEM Program ID]**
      * **[!UICONTROL Adobe Commerce URL]**
      * **[!UICONTROL AEM Environment ID]**
      * **[!UICONTROL IMS Org ID]**

サポートチケットを送信すると、AdobeはCloud Services環境でOpenAPI機能を備えたDynamic Mediaを有効にし、統合を進めるためにIMS Client IDなどの詳細を共有します。

>[!ENDTABS]

### インストール手順

1. AEM Cloud Managerに移動し、プログラムを選択し、Adobe Commerceと統合する実稼動環境とステージング環境を[作成します](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/onboarding/journey/create-environments#creating-environments)。

1. [選択したプログラムのAdobe管理Git リポジトリ &#x200B;](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/sites/administering/site-creation/quick-site/retrieve-access#repo-access)を複製します。

   ![Cloud Manager リポジトリの資格情報とコピーコマンド &#x200B;](../assets/cloud-manager-repository-info.png){width="600" zoomable="yes"}

   Cloud Manager **パイプライン**&#x200B;で、**[!UICONTROL Access Repo Info]**&#x200B;を選択して&#x200B;**[!UICONTROL Repository Info]**&#x200B;を開きます。 **[!UICONTROL URL]**&#x200B;または&#x200B;**[!UICONTROL Git command line]**&#x200B;の値をコピーし、必要に応じてアクセス パスワードを生成してから、Git クライアントとローカルにクローンを作成します。

1. GitHubから、[AEM Assets Commerce リポジトリ &#x200B;](https://github.com/ankumalh/assets-commerce)からパッケージコードをダウンロードします。

1. [&#x200B; ローカルのAEM開発環境](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/local-development-environment-set-up/overview)から、ダウンロードしたコードを既存のAdobe管理リポジトリに手動でコピーします。

1. プロジェクトのすべての`filter.xml`および`pom.xml` ファイルで、&lt;my-app>のすべての出現箇所をアプリ名に置き換えます。

   >[!NOTE]
   >
   > または、カスタムコードを&#x200B;**Maven** パッケージとしてAEM Assets プロジェクト設定にインストールすることもできます。

1. 変更を確定し、ローカル開発ブランチをCloud Manager Git リポジトリにプッシュします。

1. [&#x200B; デプロイメントパイプライン &#x200B;](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/sites/administering/site-creation/quick-site/pipeline-setup#create-front-end-pipeline)を設定するか、パイプラインが選択した環境に変更をデプロイできることを確認します。

   ![Cloud Manager パイプライン &#x200B;](../assets/cloud-manager-pipelines.png){width="600" zoomable="yes"}

   パイプラインが存在する場合、アクションメニュー（**...**）を開きます **[!UICONTROL Run]**、**[!UICONTROL Edit]**、**[!UICONTROL View/Edit variables]**&#x200B;またはその他のアクションへ – 上記のリンクされたCloud Manager パイプラインのドキュメントを参照してください。

1. AEM Cloud Managerから、[&#x200B; パイプラインを使用してコードをデプロイし、AEM環境を更新します](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/deploy-code#deploying-code-with-cloud-manager)。

1. 任意のアセットに移動し、そのプロパティを編集して変更を検証します。

   * デフォルトのメタデータスキーマには、「**Commerce**」タブが含まれています。

   * 製品SKUと`Eligible for Commerce` フィールドが表示されます。

### 「Commerce」タブがプロパティに表示されない

「**Commerce**」タブがプロパティに表示されない場合は、メタデータスキーマエディターで次の手順を手動で実行する必要があります。

1. メタデータスキーマエディターに移動します。

1. **編集**&#x200B;を選択して、デフォルトのメタデータスキーマフォームを変更します。

1. 「**Commerce**」タブを作成し、選択します。

1. **Product** コンポーネントを&#x200B;**Commerce** タブにドラッグ&amp;ドロップし、プロパティ `commerce:skus`にマッピングします。

1. **役割を表示**&#x200B;および&#x200B;**順序を表示**&#x200B;のチェックボックスを選択します。

1. **checkbox** コンポーネントを&#x200B;**Commerce** タブにドラッグ&amp;ドロップし、プロパティ `commerce:isCommerce`にマッピングします。 オプションとして&#x200B;**Yes**&#x200B;と&#x200B;**No**&#x200B;を定義します。

その他の問題が発生した場合は、[&#x200B; サポートチケット &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#submit-ticket)を作成するか、AEM Assets Integrationの営業担当者にお問い合わせください。

## メタデータプロファイルの設定（オプション）

AEM Assets オーサー環境で、メタデータプロファイルを作成して、Commerce アセットメタデータのデフォルト値を設定します。 これらのデフォルトを自動的に使用するには、新しいプロファイルをAEM Asset フォルダーに適用します。 この設定により、手作業を削減してアセット処理が合理化されます。

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

1. オプション。 承認済みのCommerce アセットがAEM Assets環境にアップロードされるときに自動的に同期するには、`Basic` タブの&#x200B;_[!UICONTROL Review Status]_&#x200B;フィールドのデフォルト値を`approved`に設定します。

1. アップデートを保存します。

### メタデータプロファイルをCommerce assets ソースフォルダーに適用する

1. **[!UICONTROL Metadata Profiles]** ページから、Commerce統合プロファイルを選択します。

1. アクションメニューから、**[!UICONTROL Apply Metadata Profiles to Folders]**&#x200B;を選択します。

1. Commerce アセットを含むフォルダーを選択します。

   Commerce フォルダーが存在しない場合は作成します。

1. **[!UICONTROL Apply]**&#x200B;を選択します。

## 次のステップ

* [!BADGE PaaSのみ]{type=Informative tooltip="Cloud プロジェクト上のAdobe Commerce（Adobeで管理されるPaaS インフラストラクチャ）にのみ適用されます。"} [Adobe Commerce パッケージをインストール &#x200B;](configure-commerce.md)。

* [!BADGE SaaSのみ]{type=Positive url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud ServiceおよびAdobe Commerce Optimizer プロジェクト（Adobeが管理するSaaS インフラストラクチャ）にのみ適用されます。"} [管理者](setup-synchronization.md)から統合を設定します。
