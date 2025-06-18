---
title: AEMへのメディアファイルの移行
description: Adobe Commerceまたは外部ソースからAEM Assets DAM にメディアファイルを移行します。
feature: CMS, Media, Integration
source-git-commit: b6e190e883087a942630f0a27781654cd2c68781
workflow-type: tm+mt
source-wordcount: '734'
ht-degree: 0%

---


# AEM Assets DAM へのメディアファイルの移行

Adobe CommerceとAdobe Experience Manager（AEM）には、CommerceからAEM Assets **Digital Asset Management System （DAM）** へのメディアファイル移行を効率化する組み込み機能が用意されています。 他のソースからメディア ファイルをマイグレーションすることもできます。

## 前提条件

| カテゴリ | 要件 |
|----------|-------------|
| **必要システム構成** | <ul><li>AEM AssetsでプロビジョニングされたAEM as a Cloud Service環境</li><li>十分なストレージ容量</li><li>大きなファイル転送のネットワーク帯域幅</li></ul> |
| **必要なアクセスと権限** | <ul><li>AEM Assets as a Cloud Serviceへの管理者アクセス</li><li>メディアファイルが格納されているソースシステム（Adobe Commerceまたは外部システム）へのアクセス</li><li>クラウドストレージサービスにアクセスするための適切な権限</li></ul> |
| **クラウドストレージアカウント** | <ul><li>AWS S3 または Azure Blob Storage アカウント</li><li>プライベートコンテナ / バケット設定</li><li>認証資格情報</li></ul> |
| **Source コンテンツ** | <ul><li>整理されたメディア ファイルの移行の準備ができました</li><li>の画像およびビデオファイル <a href="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/file-format-support#image-formats">AEM Assetsでサポートされる形式 </a>。</li><li>重複したアセットのクリーンアップ</li></li> |
| **メタデータの準備** | <ul><li><a href="https://experienceleague.adobe.com/en/docs/commerce-admin/content-design/aem-asset-management/getting-started/aem-assets-configure-aem">Commerce アセット用に設定されたAEM Assets メタデータプロファイル </a></li><li>各アセットのマッピングされたメタデータ値</li><li>CSV ファイルエディター（Microsoft Excel など）</li></ul> |

## 移行のベストプラクティス

1. 未使用および重複したコンテンツを削除することで、移行前にアセットをキュレーションできます。

1. サイズ、形式、ユースケース別にアセットを論理的に整理する。

1. 大きな移行は小さなバッチに分割することを検討してください。

1. ピーク以外の時間帯に、リソースを大量に消費する読み込みをスケジュールします。

1. 完全に読み込む前にメタデータマッピングを検証します。

## 移行ワークフロー

移行ワークフローに従って、Adobe Commerceまたは別の外部システムからメディアファイルを書き出し、AEM Assets DAM に読み込みます。

### 手順 1：既存のデータソースからのコンテンツのエクスポート

[!BADGE PaaS のみ ]{type=Informative tooltip="クラウドプロジェクト上のAdobe Commerceにのみ適用されます（Adobeが管理する PaaS インフラストラクチャ）。"}

Adobe Commerceのマーチャントにとっては、**リモートストレージモジュール** は、メディアファイルの読み込みと書き出しを容易にすることができます。 このモジュールを使用すると、企業はAWS S3 などのリモートストレージサービスを使用してメディアファイルを保存および管理できます。 Commerce インスタンスにリモートストレージを設定するには、**Commerce設定ガイド ](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/storage/remote-storage/remote-storage-aws-s3) の [ リモートストレージの設定** を参照してください。

メディアファイルがAdobe Commerce以外に保存されている場合は、AEM as a Cloud Serviceでサポートされている [ データソース ](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/assets-view/bulk-import-assets-view#prerequisites) の 1 つに直接アップロードします。

### 手順 2：メタデータマッピング用の CSV ファイルの作成

メディアファイルを書き出したら、CSV ファイルを作成して、自動化に必要なメタデータでこれらのアセットをマッピングします。 CSV には、{product **、{position** および **role mapping** のフィールドを含める必要があり、**6** AEM Assets メタデータプロファイル ](configure-aem.md#configure-a-metadata-profile) と整合している必要があります。[

次の表に示すように、Commerce アセットの [AEM Assets メタデータプロファイルに含まれるメタデータフィールドの値を ](configure-aem.md) 移行するメディアファイルごとに指定します。

| メタデータ | 説明 | 値 |
|-------|-------------|--------|
| assetPath | AEM Assets リポジトリー内でアセットが保存されるフルパス。<br><br> パスを使用して、Commerce アセットを整理するためのサブフォルダーを作成します（例：`content/dam/commerce/<brand>/<type>`）。 | `/content/dam/commerce/<sub-folder>/..<filename>` |
| コマース：ポジション | 商品ギャラリー内のアセットの位置/順序 | パイプで区切られた複数の数値（csv ファイルを参照） |
| commerce:isCommerce | アセットがコマースで使用されているかどうかを示すフラグ | `Yes` |
| commerce:sku | このアセットに関連付けられている製品 SKU | パイプで区切られた複数の文字列値（csv ファイルを参照） |
| コマース：ロール | アセットの画像の役割またはタイプ（`thumbnail`、`main image`、`swatch` など） | セミコロンで区切られた複数の値（例：&quot;thumbnail; image; swatch_image; small_image&quot;） |

+++CSV コード

このサンプルの CSV コードを使用して、Microsoft Excel などのコードエディターまたはスプレッドシートアプリケーションでファイルを作成します。

```csv
assetPath,commerce:positions{{Number: multi}},commerce:isCommerce{{String}},commerce:skus{{String: multi}},commerce:roles{{String: multi}}
/content/dam/commerce/sample1.jpg,1,Yes,sku1,thumbnail; image; swatch_image; small_image
/content/dam/commerce/sample2.jpg,1|1|1,Yes,sku1|sku2|sku3,thumbnail; image; swatch_image; small_image|image|image; small_change
```

+++

### 手順 3:AEM AssetsへのAssetsの一括読み込み

メタデータマッピングファイルを作成した後、AEM Assets一括読み込みツールを使用してアセットを読み込みます。

以下は、このツールの使用の概要です。

1. [AEM Assets as a Cloud Service オーサー環境にログインします ](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/onboarding/journey/aem-users#login-aem)。

1. Experience Managerのツール ビューで、**[!UICONTROL Assets]** / **[!UICONTROL Bulk Import]** を選択します。

   ![AEM Assetsの作成 ](../assets/aem-assets-bulk-import-selection.png){width="600" zoomable="yes"}

1. 一括読み込み設定で「**[!UICONTROL Create]**」を選択して、設定フォームを開きます。

   ![AEM Assetsの作成 ](../assets/aem-assets-bulk-import-configuration.png){width="600" zoomable="yes"}

1. 設定を行い、設定を保存します。

   次が必要です。

   * データソースの認証資格情報
   * 読み込まれたファイルが保存されるAEM Assetsのターゲットフォルダー
   * オプション。 読み込み設定をカスタマイズするための MIME タイプ、ファイルサイズおよびその他のパラメーターに関する情報です
   * クラウドストレージインスタンスにアップロードしたメタデータマッピング CSV ファイルへのパス。

   手順について詳しくは、*AEM Assets as a Cloud Service ユーザーガイド ](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/manage/add-assets#configure-bulk-ingestor-tool) 一括読み込みツールの設定 [ を参照してください*。

1. 設定を保存したら、一括読み込みツールを使用して、読み込み操作をテストおよび実行します。

>[!MORELIKETHIS]
>
> [ 一括読み込みツールのビデオデモ ](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/manage/add-assets#asset-bulk-ingestor)
> > [ヒント、ベストプラクティス、制限事項 ](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/manage/add-assets#tips-limitations)
> > [API を使用したアセットのアップロードまたは取り込み ](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/admin/developer-reference-material-apis#asset-upload)
