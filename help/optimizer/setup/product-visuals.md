---
title: AEM Assetsを使用した製品ビジュアル
description: ' [!DNL Adobe Commerce Optimizer]の商品画像にAEM Assetsを使用する方法について説明します。'
feature: CMS, Media, Configuration, Integration
role: Admin, Developer
badgeSaas: label="SaaSのみ" type="Positive" url="https://experienceleague.adobe.com/ja/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud Serviceおよび [!DNL Adobe Commerce Optimizer]  プロジェクトにのみ適用されます（Adobeで管理されるSaaS インフラストラクチャ）。"
source-git-commit: 264658bee09a22cfd55828c6960153cc1239d3fb
workflow-type: tm+mt
source-wordcount: '634'
ht-degree: 0%

---


# AEM Assetsを使用した製品ビジュアル

Product Visualsを使用すると、[!DNL Adobe Commerce Optimizer]人の販売者がAdobe Experience Manager（AEM）Assetsを通じて商品画像を管理できます。 この統合により、カタログレイヤーを使用して、AEM Assetsから[!DNL Commerce Optimizer] カタログに高品質な製品画像を同期するためのシームレスなワークフローが提供されます。

>[!NOTE]
>
>**製品ビジュアル**&#x200B;は、[!DNL Adobe Commerce as a Cloud Service]および[!DNL Adobe Commerce Optimizer]で提供されるバンドルの名前です。 [Dynamic MediaとOpenAPI機能](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/assets/dynamicmedia/dynamic-media-open-apis/dynamic-media-open-apis-overview)および[AEM Assets Prime](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/assets/assets-prime)を組み合わせています。
>
>別のAEM Assets ライセンス（例：**AEM Assets Ultimate**）を持つお客様は、同じ統合を使用できます。AEM リリースのみが、ライセンスの種類ではなく、オンボーディング手順に影響します。

## 主な特長

* **一元管理されたアセット管理**：エンタープライズ向けのデジタルアセット管理ソリューションであるAEM Assetsですべての商品画像を管理します。
* **自動同期**: AEM Assetsでアセットが承認または更新されると、製品画像が自動的に同期されます。
* **Dynamic Media配信**:OpenAPI機能を使用したDynamic Mediaを活用して、画像配信を最適化します。
* **カタログレイヤー**：商品画像はカタログレイヤーとして適用され、ベースカタログにAEM Assets画像をオーバーレイできます。

## 仕組み

統合には、2つの独立したイベントフローがあります。 どちらも[Adobe I/O Events](https://developer.adobe.com/events/docs/)を使用してAssets統合サービスにイベントを転送しますが、各方向で独自のイベントプロバイダーが使用されます。

* **AEM AssetsからAssets統合サービス**: アセットが承認、拒否、または削除されると、そのイベントはAssets統合サービスに配信されます。 このサービスは、`match-by-SKU`またはカスタムマッチャー戦略を使用してアセットを製品に一致させ、次に`product-asset` マッピングを[!DNL Commerce Optimizer]に送信し、そこで製品レイヤーとして保存します。

* **[!DNL Commerce Optimizer]からAssets Integration Service**&#x200B;へ：[!DNL Commerce Optimizer]で製品が更新されると、そのイベントはAssets Integration Serviceに配信されます。 サービスは、一致するアセットマッピングをすべて[!DNL Commerce Optimizer]に同期します。

更新された画像は、ストアフロント API （カタログサービス、ライブサーチ、商品レコメンデーション）を通じて利用できます。

### Sourceとレイヤー設定

AEM Assetsの画像は、次のソース設定を持つカタログレイヤーとして取り込まれます。

> ソース設定の例

```json
{
  "source": {
    "locale": "en-US",
    "layer": "AEM-Assets"
  }
}
```

この設定により、AEM Assetsの画像がベースとなる商品カタログにオーバーレイとして適用されます。

## 前提条件

製品ビジュアルを有効にする前に、Commerce Optimizer[&#128279;](../../aem-assets-integration/get-started/configure-aco.md#prerequisites)の前提条件を満たしていることを確認してください。

## 設定

統合を有効にするには、[&#x200B; サポートチケット &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-learn/tutorials/help-and-support/create-a-support-ticket)を[!DNL Commerce Optimizer]とAEM Assetsの詳細とともに作成します。 Adobe サポートは、統合を設定し、Assets Integration Serviceにテナントを登録します。

オンボーディングについて詳しくは、[Commerce Optimizer用AEM Assetsの設定](../../aem-assets-integration/get-started/configure-aco.md)を参照してください。

### AEM Assets メタデータの設定

商品の自動マッチングを有効にするには、Commerce メタデータを使用してAEM Assetsのアセットを設定します。

必要なメタデータフィールドと手順については、[AEM Assets](../../aem-assets-integration/get-started/configure-aco.md#configure-aem-assets-first)の設定を参照してください。

## 制限

商品ビジュアルを使用する前に、[統合の制限](../../aem-assets-integration/get-started/configure-aco.md#limitations)を確認してください。これは、AEM Assets データとベースカタログの結合方法に影響するレイヤー関連の制約です。

容量と使用状況の割り当て（アセットのストレージ、Dynamic Mediaの操作、ユーザーライセンス）については、_境界と制限ガイド_&#x200B;の[製品ビジュアルの制限](../boundaries-limits.md#product-visuals-limits)を参照してください。

## 製品ビジュアルの活用

統合の設定後は、AEM Assetsで商品画像を管理します。

### 製品への画像の追加

1. AEM Assetsリポジトリに画像をアップロードします。

1. Commerce メタデータをアセットに追加します。

   [既定の自動一致](../../aem-assets-integration/synchronize/default-match.md)および[&#x200B; カスタム自動一致](../../aem-assets-integration/synchronize/custom-match.md)を参照してください。

1. アセットの配信を承認します。 トリガーを同期するには、アセットが&#x200B;**approved** ステータスである必要があります。

1. 画像は自動的に[!DNL Commerce Optimizer]に同期されます。

### AEMとAssetsのレイヤーの適用

ストアフロントにAEM Assets画像を表示するには、[&#x200B; カタログビューに`AEM-Assets` レイヤーを割り当てます](catalog-layer.md#assign-the-aem-assets-layer-to-a-catalog-view)。

## その他

* [カタログレイヤー](catalog-layer.md)
* [カタログビュー](catalog-view.md)
* [AEM Assets統合ガイド](../../aem-assets-integration/overview.md)
