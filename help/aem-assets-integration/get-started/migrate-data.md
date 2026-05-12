---
title: AEMへのメディアファイルの移行
description: Adobe Commerceまたは外部ソースからAEM Assets DAMにメディアファイルを移行します。
feature: CMS, Media, Integration
exl-id: ccb13e90-8b18-4f1e-94ce-f0dacea2f617
TQID: https://experienceleague.adobe.com/-fCE7lTivOuhLDzEMNexxGWLTkL52oo9p-sm54HxpQM
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: da3860b0-d637-47df-bef0-273751180266
source-git-commit: 33cd0e217447351b690646ec8d230f76060a74da
workflow-type: tm+mt
source-wordcount: 1010
ht-degree: 0%

---

# AEM Assets DAMへのメディアファイルの移行

Adobe CommerceとAdobe Experience Manager（AEM）の両方には、CommerceからAEM Assets **デジタルアセット管理システム（DAM）**&#x200B;へのメディアファイルの移行を効率化する機能が組み込まれています。 他のソースからメディアファイルを移行することもできます。

## 前提条件

| カテゴリ | 要件 |
|----------|-------------|
| **必要システム構成** | <ul><li>AEM AssetsでプロビジョニングされたAEM as a Cloud Service環境</li><li>十分なストレージ容量</li><li>大規模なファイル転送に対応するネットワーク帯域幅</li></ul> |
| **必要なアクセスと権限** | <ul><li>AEM Assets as a Cloud Serviceへの管理者アクセス</li><li>メディアファイルが保存されているソースシステム（Adobe Commerceまたは外部システム）へのアクセス</li><li>クラウドストレージサービスにアクセスするための適切な権限</li></ul> |
| **クラウドストレージアカウント** | <ul><li>AWS S3またはAzure Blob Storage アカウント</li><li>プライベートコンテナ/バケット設定</li><li>認証情報</li></ul> |
| **Source コンテンツ** | <ul><li>移行用に整理されたメディアファイル</li><li>AEM Assets</a>でサポートされている<a href="https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/assets/file-format-support#image-formats">形式の画像およびビデオファイル。</li><li>重複したアセットの整理</li></li> |
| **メタデータの準備** | <ul><li><a href="https://experienceleague.adobe.com/ja/docs/commerce-admin/content-design/aem-asset-management/getting-started/aem-assets-configure-aem">Commerce assets用に設定されたAEM Assets メタデータプロファイル </a></li><li>各アセットのマッピングされたメタデータ値</li><li>CSV ファイルエディター（例：Microsoft Excel）</li></ul> |

## 移行のベストプラクティス

1. 未使用および重複するコンテンツを削除して、移行前にアセットをキュレートします。

1. サイズ、形式、ユースケースごとに、アセットを論理的に整理します。

1. 大規模な移行を小規模なバッチに分割することを検討する。

1. オフピーク時に、リソース集約的なインポートをスケジューリングします。

1. 完全に読み込む前に、メタデータマッピングを検証します。

## 移行ワークフロー

移行ワークフローに従って、Adobe Commerceまたは他の外部システムからメディアファイルを書き出し、AEM Assets DAMに読み込みます。

### 手順1：既存のデータソースからコンテンツを書き出す

[!BADGE PaaSのみ]{type=Informative tooltip="Cloud プロジェクト上のAdobe Commerce（Adobeで管理されるPaaS インフラストラクチャ）にのみ適用されます。"}

Adobe Commerceのマーチャントの場合、**リモートストレージモジュール**&#x200B;を使用すると、メディアファイルの読み込みと書き出しが容易になります。 AWS S3などのリモートストレージサービスを使用して、メディアファイルを保存および管理できます。 Commerce インスタンスのリモートストレージを設定するには、**Commerce設定ガイド**&#x200B;の[&#x200B; リモートストレージの設定](https://experienceleague.adobe.com/ja/docs/commerce-operations/configuration-guide/storage/remote-storage/remote-storage-aws-s3)を参照してください。

Adobe Commerce以外にメディアファイルが保存されている場合は、AEM as a Cloud Serviceでサポートされている[&#x200B; データソース &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/assets/assets-view/bulk-import-assets-view#prerequisites)のいずれかに直接アップロードします。

### 手順2：メタデータマッピング用のCSV ファイルの作成

各メディアファイルをCommerceの商品データにマッピングするCSV ファイルを作成します。 次のいずれかの方法を選択します。

* **Adobe Commerce （PaaS）**: CLI コマンドを使用して、カタログからCSVを自動生成します
* CSV ファイルを手動で作成する

#### CLIを使用したメタデータのエクスポート

[!BADGE PaaSのみ]{type=Informative tooltip="Cloud プロジェクト上のAdobe Commerce（Adobeで管理されるPaaS インフラストラクチャ）にのみ適用されます。"}

AEM Assets Integration CLI コマンドを使用すると、Commerce プロジェクトに保存されているプロダクトメディアファイルから、画像URL、位置、役割を含むメタデータ CSV ファイルを自動生成できます。

1. AEM Assets統合モジュールがインストールされていることを確認するために、使用可能なコマンドを一覧表示します。

   ```bash
   bin/magento list aem
   ```

   カスタム拡張コマンドは、コマンドリストの先頭にある`aem`の下に表示されます。

1. AEM パスのプレフィックスを使用して、metadata export コマンドを実行します。

   ```bash
   bin/magento aem:assets:export:csv <AEM-path-prefix>
   ```

   `<AEM-path-prefix>`は、アセットがAEM Assets DAMに保存されるベース フォルダーパスです（例：`/content/dam/commerce/`）。

   ```bash
   bin/magento aem:assets:export:csv /content/dam/commerce/
   ```

   これにより、Commerce カタログ内の各商品アセットの画像URL、位置、役割を含む`var/export` ディレクトリに`metadata.csv` ファイルが作成されます。

#### CSVを手動で作成

Adobe Commerce以外に保存されているメディアファイルの場合は、CSV ファイルを手動で作成します。 列ヘッダー&#x200B;**は、[AEM Assets メタデータプロファイル &#x200B;](configure-aem.md)で設定されたフィールド名**&#x200B;と一致する必要があります。 ファイルを作成したら、各メディアファイルのメタデータ値を行に入力します。

| メタデータ | 説明 | 値 |
|-------|-------------|--------|
| assetPath | アセットがAEM Assets リポジトリに保存されるフルパス。<br><br> パスを使用してサブフォルダーを作成し、Commerce アセットを整理します（例：`content/dam/commerce/<brand>/<type>`）。 | `/content/dam/commerce/<sub-folder>/..<filename>` |
| commerce:positions | 製品ギャラリー内のアセットの位置/順序 | パイプで区切られた複数の数値（「数値：複数」） |
| commerce:isCommerce | アセットがコマースで使用されているかどうかを示すフラグ | `Yes` |
| commerce:skus | このアセットに関連付けられた製品SKU | パイプで区切られた複数の文字列値（文字列：複数） |
| commerce:roles | アセットの役割または画像の種類（例：`thumbnail`、`main image`、`swatch`） | セミコロンで区切られた複数の値（例：「thumbnail; image; swatch_image; small_image」） |

+++CSV コード

このサンプルのCSV コードを使用して、コードエディターまたはMicrosoft Excelなどのスプレッドシートアプリケーションでファイルを作成します。

```csv
assetPath,commerce:positions{{Number: multi}},commerce:isCommerce{{String}},commerce:skus{{String: multi}},commerce:roles{{String: multi}}
/content/dam/commerce/sample1.jpg,1,Yes,sku1,thumbnail; image; swatch_image; small_image
/content/dam/commerce/sample2.jpg,1|1|1,Yes,sku1|sku2|sku3,thumbnail; image; swatch_image; small_image|image|image; small_change
```

+++

### ステップ 3:AssetsをAEM Assetsに一括読み込む

メタデータマッピングファイルを作成したら、AEM Assetsの一括読み込みツールを使用してアセットを読み込みます。

次に、ツールの概要を示します。

1. [AEM Assets as a Cloud Service オーサー環境](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/onboarding/journey/aem-users#login-aem)にログインします。

1. Experience Manager ツール ビューから、**[!UICONTROL Assets]** > **[!UICONTROL Bulk Import]**&#x200B;を選択します。

   ![AEM Assets オーサリング &#x200B;](../assets/aem-assets-bulk-import-selection.png){width="600" zoomable="yes"}

1. 一括読み込み設定から、**[!UICONTROL Create]**&#x200B;を選択して設定フォームを開きます。

   ![AEM Assets オーサリング &#x200B;](../assets/aem-assets-bulk-import-configuration.png){width="600" zoomable="yes"}

1. 設定を設定して保存します。

   次のようなものがあります。

   * データソースの認証情報
   * 読み込んだファイルが保存されるAEM Assetsのターゲットフォルダー
   * オプション。 インポート設定をカスタマイズするためのMIME タイプ、ファイルサイズおよびその他のパラメーターに関する情報
   * クラウドストレージインスタンスにアップロードしたメタデータマッピング CSV ファイルへのパス。

   詳細な手順については、*AEM Assets as a Cloud Service ユーザーガイド*&#x200B;の「[一括読み込みツールの設定](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/assets/manage/add-assets#configure-bulk-ingestor-tool)」を参照してください。

1. 設定を保存した後、一括読み込みツールを使用してテストし、読み込み操作を実行します。

>[!MORELIKETHIS]
>
> [一括読み込みツールのビデオ デモ](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/assets/manage/add-assets#asset-bulk-ingestor)
> [ヒント、ベストプラクティス、制限事項](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/assets/manage/add-assets#tips-limitations)
> [API](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/assets/admin/developer-reference-material-apis#asset-upload)を使用したアセットのアップロードまたは取り込み
