---
title: Commerce Optimizer用のAEM Assetsの設定
description: ' [!DNL Adobe Commerce Optimizer] のAEM Assets統合を設定する方法について説明します。'
feature: CMS, Media, Configuration, Integration
source-git-commit: 7f0970648663331fea2af19b981c4fd3b3aedcaa
workflow-type: tm+mt
source-wordcount: '1129'
ht-degree: 0%

---


# [!DNL Adobe Commerce Optimizer] 用のAEM Assetsの設定

[!BADGE SaaS のみ ]{type=Positive tooltip="Adobe Commerce Optimizer プロジェクトにのみ適用されます。"}

AEM Assets Integration for [!DNL Adobe Commerce Optimizer] を使用すると、マーチャントは、商品画像に対する一元的なデジタルアセット管理ソリューションとしてAEM Assetsを使用できます。 このガイドでは、[!DNL Commerce Optimizer] に固有の設定について説明します。

Adobe Commerce（PaaS）やAdobe Commerce as a Cloud Service（ACCS）とは異なり、[!DNL Commerce Optimizer] には管理設定 UI がありません。 統合を有効にするには、[!DNL Adobe Commerce Optimizer] とAEM Assetsの詳細を入力して、サポートチケットを作成します。 Adobe サポートは、統合を設定し、テナントをAssets Integration Service に登録します。

次の図は、[!DNL Adobe Commerce Optimizer] とAEM Assets統合の間の製品同期の概要を示しています。

![AEM Assetsから [!DNL Commerce Optimizer] へのフロー ](../assets/aco-asset-sync-architecture.png){width="700"}

この統合には、主に次の 2 つのフローがあります。

* **AEM Assetsから**：アセットが承認、却下または削除されると、イベントはAdobe パイプラインを通じてAssets Integration Service に送られます。 このサービスは、`match-by-SKU` （メタデータ駆動型）または [ カスタムマッチャー（App Builder） ](../synchronize/custom-match.md){target=_blank} を使用してアセットと商品を照合し、`product-asset` のマッピングをCommerce Optimizerに送信して、商品レイヤーとして保存します。

* **[!DNL Adobe Commerce Optimizer]** から：[!DNL Commerce Optimizer] で商品を更新すると、イベントはAdobe パイプラインを通じてAssets Integration Service に送られます。 サービスは、一致するアセットマッピングをすべて [!DNL Adobe Commerce Optimizer] に同期します。

## 前提条件

統合を設定する前に、次のことを確認します。

* Product Visuals の使用権限を持つアクティブな [!DNL Adobe Commerce Optimizer] インスタンス、または Dynamic Media を使用するAEM Assets ライセンス。
* AEM Assets as a Cloud Service環境にアクセスします。
* [!DNL Commerce Optimizer] とAEM Assetsは両方とも同じAdobe IMS組織内にあります。
* AEM Assetsで OpenAPI が有効になっている Dynamic Media。

## オンボーディング

[!DNL Commerce Optimizer] とAEM Assets統合をオンボードするには、[ サポートチケットを作成 ](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#submit-ticket) する必要があります。

Adobe サポートは、チケットに含まれる情報を使用して、Assets Integration Service にテナントを登録し、統合を設定します。

サポートチケットに次の情報を含めます。

* **[!DNL Adobe Commerce Optimizer]テナント ID** （インスタンス ID）が [!DNL Commerce Optimizer] URL またはCommerce Cloud Manager UI に見つかりました。
* **AEM プログラム ID**。
* **AEM環境 ID**。
* **一致ルール**:SKU または [ 外部マッチャー（App Builder） ](../synchronize/custom-match.md){target=_blank} で一致します。
* **レイヤー**: テナントを登録するカタログのレイヤー名。 必要に応じてカスタム名を指定します。 それ以外の場合は、デフォルト `AEM-Assets` が使用されます。
* **ロケール**：テナントを登録するためのカタログソースのロケール（例：`en-US`）。

>[!IMPORTANT]
>
> 統合では、テナントごとに 1 つのソース（1 つのロケールと 1 つのレイヤーの組み合わせ）をサポートしています。

Adobe サポートがチケットを処理すると、統合が設定され、テナントがAssets Integration Service に登録されます。

オンボーディングが完了したら、次の操作を行います。

1. **Assets Integration Service への登録**:[!DNL Commerce Optimizer] テナントは、[!DNL Adobe Commerce Optimizer] テナント ID、Assets プログラム ID、AEM環境 ID およびテナントを使用して、AEM Integration Service に登録されます。

1. **イベント購読**: Assets Integration Service は、以下を購読します。

   * AEM Assets イベント （アセットが承認、更新、削除されました）
   * [!DNL Commerce Optimizer] カタログイベント（製品を作成、更新）

### 制限事項

[!DNL Commerce Optimizer] 統合には次の制限があります。

* **マーチャントごとに 1 つのレイヤー** - AEM Assets統合では、マーチャントごとに 1 つのAEM - Assets レイヤー（テナントごとに 1 つのソース）をサポートします。 現時点では、マーチャントごとに複数のレイヤーを設定することはできません。
* **画像のみ** – この統合では、ビデオやその他のメディアタイプをサポートしていません。
* **カテゴリ画像なし** - カテゴリ画像の同期は使用できません。 AEM AssetsのAssets セレクター用のカテゴリ画像（UI 挿入）はサポートされていません。
* **マルチサイトの違いなし** – 統合では、マルチサイトは処理されません。製品に関連付けられた画像は、すべてのチャネルとポリシーで同じように表示されます。
* **画像の位置/順序** – 画像の位置と順序はサポートされていません。
* **製品が存在する必要があります** – 製品が [!DNL Commerce Optimizer] に存在しない場合、その製品とアセットのマッピング用のレイヤーは作成されません。
* **レイヤーフィールドの上書き** - レイヤー内の値が基本カタログを上書きします。 レイヤーペイロードでフィールドが送信されない場合は、空の値で上書きできます。 AEM Assets コンテンツ用に専用のレイヤーを使用します。他の目的で既存のレイヤーを再利用すると、意図しないデータ損失が生じる可能性があります。

### AEM Assetsの設定

AEM Assetsの [!DNL Commerce Optimizer] のインストールおよび設定プロセスは、Adobe Commerce as a Cloud Serviceの場合と同じです。 手順について詳しくは [Commerce メタデータをサポートするためのAEM Assets プロジェクトの設定 ](configure-aem.md) を参照してください。

AEM Assets環境の準備が整っていることを確認します。

1. **AEM Assets設定**: Commerce メタデータプロファイルを設定します。 [ メタデータプロファイルの設定 ](configure-aem.md#configure-a-metadata-profile) を参照してください。

1. **Dynamic Media のイネーブルメント**:OpenAPI 機能を備えた Dynamic Media がAEM Assetsで有効になっていることを確認します。

## AEM Assetsの設定

製品とアセットの同期を有効にするには、AEM Assets環境を設定します。

### 手順 1:OpenAPI を使用して Dynamic Media を有効にする

OpenAPI を使用した Dynamic Media をAEM Assetsで有効にする必要があります。 製品のビジュアル機能と新しいAEM Assets ライセンスにより、Cloud Managerを使用してセルフサービス方式で有効にできます。 古いAEM Assets ライセンスを有効にするには、Adobe サポートが必要です。 イネーブルメント手順については、[AEM Assets プロジェクトの設定 ](configure-aem.md#prerequisites) を参照してください。

### 手順 2：オプション。 Commerce メタデータプロファイルの設定

AEM Assetsでメタデータプロファイルを設定して、Commerce固有のメタデータを保存します。

手順について詳しくは、[ メタデータプロファイルの設定 ](configure-aem.md#step-2-optional-configure-a-metadata-profile) を参照してください。

### 手順 3：アセットへのメタデータの適用

Commerce メタデータをAEM Assetsの商品画像に追加します。

フィールド定義については [AEM Commerce パッケージのコンテンツ ](configure-aem.md#aem-commerce-assets-commerce-package-contents) を、設定手順については [ メタデータプロファイルの設定 ](configure-aem.md#step-2-optional-configure-a-metadata-profile) を参照してください。

データをトリガーに同期するには、アセットが **承認済み** ステータスになっている必要があります。 メタデータのみを保存しても、イベントはトリガーされません。

>[!CAUTION]
>
> `AEM-Assets` レイヤーを [ カタログビュー ](https://experienceleague.adobe.com/en/docs/commerce/optimizer/setup/catalog-view) に割り当てます。 レイヤーが割り当てられていない場合、製品画像データが予期せず上書きされる可能性があります。

## 同期

設定が完了すると、統合によりマッピング `product-asset` 自動的に同期されます。

詳しくは、[ カスタム自動照合 ](../synchronize/custom-match.md) を参照してください。

### SKU で一致ワークフローの例

既存のアセットを新しい製品に追加する際の一般的なフローは次のとおりです。

1. （API またはデータ取り込みを使用して） [!DNL Commerce Optimizer] で製品を作成します。 製品は、最初は画像なしで存在できます。

1. AEM Assetsで、商品にマッピングするアセットを開きます。

1. 製品 SKU を **commerce:skus** メタデータに追加し、画像の役割（`thumbnail`、`image` など）を割り当てます。

1. 配信するアセットを承認します。 これは、Assets Integration Service が処理するイベントをトリガーにします。

1. Assets統合サービスは、product-image マッピングを [!DNL Commerce Optimizer] に送信します。 [!DNL Commerce Optimizer] の製品は、アセットの画像で更新されます。

1. 画像が表示されていることを確認します。 同期が完了するまで（通常は数分以内）待ってから、[!DNL Commerce Optimizer] UI （データ同期やカタログ表示など）で商品を確認するか、ストアフロント API （カタログサービス、ライブ検索、ストアフロント GraphQL API）をクエリして、画像が返されることを確認します。

## 画像の役割の処理

製品が同じ画像の役割を使用して複数のアセットを持っている場合（例えば、`thumbnail` の役割を持つ 2 つのアセット）、統合によってその役割が保持されるアセットが 1 つだけになり、[!DNL Commerce Optimizer] レイヤーでの役割の重複や予期しないストアフロントの動作が回避されます。

**動作：** AEM Assetsから更新が送信されると、最近更新されたアセットが画像のロール（例：`thumbnail`）を受け取り、そのロールは以前のアセットから削除されます。 これにより、重複する画像の役割がストアフロントに表示されなくなります。

## その他の関連リソース

* [製品ビジュアル](../../optimizer/setup/product-visuals.md)
* [AEM Assets プロジェクトの設定](configure-aem.md)
* [カスタムの自動照合](../synchronize/custom-match.md)
* [AEM Assetsの統合の概要](../overview.md)
