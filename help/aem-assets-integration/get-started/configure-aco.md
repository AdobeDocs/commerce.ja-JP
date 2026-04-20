---
title: Commerce Optimizer用AEM Assetsの設定
description: ' [!DNL Adobe Commerce Optimizer]のAEM Assets統合を設定する方法について説明します。'
feature: CMS, Media, Configuration, Integration
source-git-commit: 14c4178338859d55a7391139033d51d1aa6f7678
workflow-type: tm+mt
source-wordcount: '1129'
ht-degree: 0%

---


# [!DNL Adobe Commerce Optimizer]のAEM Assetsを設定

[!BADGE SaaSのみ]{type=Positive tooltip="Adobe Commerce Optimizer プロジェクトにのみ適用されます。"}

[!DNL Adobe Commerce Optimizer]のAEM Assets統合により、販売者はAEM Assetsを商品画像用の一元的なデジタルアセット管理ソリューションとして使用できるようになります。 このガイドでは、[!DNL Commerce Optimizer]に固有の設定について説明します。

Adobe Commerce （PaaS）またはAdobe Commerce as a Cloud Service （ACCS）とは異なり、[!DNL Commerce Optimizer]には管理者設定UIがありません。 統合を有効にするには、[!DNL Adobe Commerce Optimizer]とAEM Assetsの詳細を記載したサポートチケットを作成します。 Adobe サポートは、統合を設定し、Assets Integration Serviceにテナントを登録します。

次の図は、[!DNL Adobe Commerce Optimizer]とAEM Assets統合の間の製品同期の概要です。

![AEM Assetsから[!DNL Commerce Optimizer] フロー](../assets/aco-asset-sync-architecture.png){width="700"}

この統合には、主に2つのフローがあります。

* **AEM Assets**&#x200B;から：アセットが承認、拒否、または削除されると、イベントはAdobe パイプラインを通じてAssets Integration Serviceに流れます。 このサービスは、`match-by-SKU` （メタデータ駆動型）または[&#x200B; カスタムマッチャー（App Builder） &#x200B;](../synchronize/custom-match.md){target=_blank}を使用してアセットを商品と照合し、次に`product-asset` マッピングをCommerce Optimizerに送信し、そこで商品レイヤーとして保存します。

* **[!DNL Adobe Commerce Optimizer]**&#x200B;から：[!DNL Commerce Optimizer]で商品が更新されると、イベントはAdobe パイプラインを経由してAssets Integration Serviceに流れます。 サービスは、一致するアセットマッピングをすべて[!DNL Adobe Commerce Optimizer]に同期します。

## 前提条件

統合を設定する前に、次のことを確認してください。

* 製品ビジュアルの使用権限を持つアクティブな[!DNL Adobe Commerce Optimizer] インスタンス、またはDynamic Mediaを持つ任意のAEM Assets ライセンス。
* AEM Assets as a Cloud Serviceへのアクセス。
* [!DNL Commerce Optimizer]とAEM Assetsの両方が同じAdobe IMS組織内にあります。
* AEM Assets環境でOpenAPIを有効にしたDynamic Media。

## オンボーディング

AEM Assets統合を[!DNL Commerce Optimizer]でオンボーディングするには、[&#x200B; サポートチケットを作成](https://experienceleague.adobe.com/ja/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#submit-ticket)する必要があります。

Adobe サポートは、チケット内の情報を使用して、Assets Integration Serviceにテナントを登録し、統合を設定します。

サポートチケットに次の情報を含めます。

* **[!DNL Adobe Commerce Optimizer]テナント ID** （インスタンス ID）が[!DNL Commerce Optimizer] URLまたはCommerce Cloud Manager UIに見つかりました。
* **AEM プログラム ID**。
* **AEM Environment ID**。
* **一致するルール**: SKUまたは[外部マッチャー（App Builder） &#x200B;](../synchronize/custom-match.md){target=_blank}によって一致します。
* **Layer**: テナントを登録するカタログ レイヤー名。 必要に応じて、カスタム名を指定します。 それ以外の場合は、デフォルトの`AEM-Assets`が使用されます。
* **ロケール**: テナントを登録するカタログ ソース ロケール （例：`en-US`）。

>[!IMPORTANT]
>
> 統合では、1つのロケールと1つのレイヤーの組み合わせである、テナントごとに1つのソースをサポートしています。

Adobe サポートがチケットを処理すると、統合が設定され、テナントがAssets Integration Serviceに登録されます。

オンボーディングが完了したら：

1. **Assets Integration Serviceへの登録**：お客様の[!DNL Commerce Optimizer] テナントは、[!DNL Adobe Commerce Optimizer] テナント ID、AEM プログラム ID、AEM Environment ID、およびテナントを使用してAssets Integration Serviceに登録されています。

1. **イベントサブスクリプション**:Assets Integration Serviceのサブスクリプション：

   * AEM Assets イベント（アセット承認済み、更新、削除）
   * [!DNL Commerce Optimizer]個のカタログイベント（製品が作成、更新されました）

### 制限

[!DNL Commerce Optimizer]統合には次の制限があります。

* **マーチャントごとに1つのレイヤー** - AEM Assets統合では、マーチャントごとに1つのAEM-Assets レイヤー（テナントごとに1つのソース）がサポートされます。 現在、マーチャントごとに複数のレイヤーを設定することはサポートされていません。
* **画像のみ** – 統合はビデオまたはその他のメディアタイプをサポートしていません。
* **カテゴリ画像がありません**- カテゴリ画像の同期は使用できません。 Assets セレクター（UI挿入）用のAEM Assetsのカテゴリ画像はサポートされていません。
* **マルチサイトの区別がありません** – 統合ではマルチサイトは処理されません。製品に関連付けられている画像は、すべてのチャネルとポリシーで同じように表示されます。
* **画像の位置/順序** – 画像の位置と順序はサポートされていません。
* **製品が存在する必要があります** – 製品が[!DNL Commerce Optimizer]に存在しない場合、その製品アセットマッピング用にレイヤーは作成されません。
* **レイヤーフィールドの上書き** - レイヤー内の値がベースカタログを上書きします。 レイヤーペイロードでフィールドが送信されない場合は、空の値で上書きできます。 AEM Assets コンテンツに専用レイヤーを使用します。他の目的で既存のレイヤーを再利用すると、意図しないデータ損失が発生する可能性があります。

### AEM Assetsの設定

[!DNL Commerce Optimizer]のAEM Assetsのインストールおよび設定プロセスは、Adobe Commerce as a Cloud Serviceの場合と同じです。 詳細な手順については、[Commerce メタデータをサポートするようにAEM Assets プロジェクトを設定する](configure-aem.md)を参照してください。

AEM Assetsを導入しました。

1. **AEM Assets設定**: Commerce メタデータプロファイルを設定します。 [&#x200B; メタデータプロファイルの設定](configure-aem.md#step-2-optional-configure-a-metadata-profile)を参照してください。

1. **Dynamic Mediaの有効化**: AEM Assets環境でOpenAPI機能を使用したDynamic Mediaが有効になっていることを確認します。

## AEM Assetsの設定

製品とアセットの同期を有効にするには、AEM Assets環境を設定します。

### 手順1:OpenAPIでDynamic Mediaを有効にする

AEM Assets環境でDynamic Media with OpenAPIを有効にする必要があります。 製品ビジュアルと新しいAEM Assets ライセンスを使用すると、Cloud Managerを介してセルフサービス方式で有効にできます。 古いAEM Assets ライセンスを有効にするには、Adobe サポートが必要です。 イネーブルメント手順については、[AEM Assets プロジェクトの設定](configure-aem.md#prerequisites)を参照してください。

### 手順2：オプション。 Commerce メタデータプロファイルの設定

AEM Assetsでメタデータプロファイルを設定して、Commerce固有のメタデータを保存します。

詳しい手順については、[&#x200B; メタデータプロファイルの設定](configure-aem.md#step-2-optional-configure-a-metadata-profile)を参照してください。

### 手順3：アセットへのメタデータの適用

AEM AssetsでCommerceのメタデータを商品画像に追加しましょう。

フィールド定義については[AEM Commerce パッケージの内容](configure-aem.md#aem-commerce-assets-commerce-package-contents)、設定手順については[&#x200B; メタデータプロファイルの設定](configure-aem.md#step-2-optional-configure-a-metadata-profile)を参照してください。

トリガーにデータを同期するには、アセットが&#x200B;**承認済み** ステータスである必要があります。 メタデータのみを保存しても、イベントはトリガーされません。

>[!CAUTION]
>
> `AEM-Assets` レイヤーを[&#x200B; カタログビュー](https://experienceleague.adobe.com/ja/docs/commerce/optimizer/setup/catalog-view)に割り当てます。 レイヤーが割り当てられていない場合、製品画像データが予期せず上書きされる可能性があります。

## 同期

設定が完了すると、統合によって`product-asset` マッピングが自動的に同期されます。

詳しくは、[&#x200B; カスタム自動一致](../synchronize/custom-match.md)を参照してください。

### SKU ワークフローによる一致の例

既存のアセットを新製品に追加する際の一般的な流れ：

1. [!DNL Commerce Optimizer]で製品を作成します（APIまたはデータ取り込み経由）。 製品は、最初は画像なしで存在できます。

1. AEM Assetsで、商品にマッピングするアセットを開きます。

1. 商品SKUを&#x200B;**commerce:skus** メタデータに追加し、画像の役割を割り当てます（例：`thumbnail`、`image`）。

1. アセットの配信を承認します。 これにより、Assets Integration Serviceが処理するイベントがトリガーされます。

1. Assets Integration Serviceは、product-image マッピングを[!DNL Commerce Optimizer]に送信します。 [!DNL Commerce Optimizer]の製品が、アセットの画像で更新されます。

1. 画像が表示されていることを確認します。 同期が完了するまでの時間（通常は数分以内）を許可してから、[!DNL Commerce Optimizer] UI （データ同期やカタログビューなど）で商品を確認するか、ストアフロント API （カタログサービス、ライブサーチ、ストアフロントGraphQL API）をクエリして、画像が返されることを確認します。

## 画像の役割の処理

製品に同じ画像の役割を使用する複数のアセットがある場合（例えば、`thumbnail`の役割を持つ2つのアセット）、統合により、その役割を1つのアセットのみが保持され、[!DNL Commerce Optimizer] レイヤーでの役割の重複とストアフロントの予期しない動作が回避されます。

**ビヘイビアー：** AEM Assetsから更新が送信されると、最も新しく更新されたアセットに画像の役割（`thumbnail`など）が割り当てられ、その役割は前のアセットから削除されます。 これにより、重複した画像の役割がストアフロントに表示されるのを防ぐことができます。

## その他

* [製品ビジュアル](../../optimizer/setup/product-visuals.md)
* [AEM Assets プロジェクトの設定](configure-aem.md)
* [カスタム自動一致](../synchronize/custom-match.md)
* [AEM Assetsとの連携の概要](../overview.md)
