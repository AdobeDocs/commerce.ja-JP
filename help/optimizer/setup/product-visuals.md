---
title: AEM Assetsを使用した製品ビジュアル
description: ' [!DNL Adobe Commerce Optimizer] で、AEM Assetsを商品画像に使用する方法を説明します。'
feature: CMS, Media, Configuration, Integration
role: Admin, Developer
badgeSaas: label="SaaS のみ" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud Serviceおよびプロジェクトのみ（Adobe [!DNL Adobe Commerce Optimizer]  管理される SaaS インフラストラクチャ）に適用されます。"
source-git-commit: c7c21df464685783b5fae1c99d60ca91e0c334d2
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 0%

---


# AEM Assetsを使用した製品ビジュアル

商品ビジュアルを使用 [!DNL Adobe Commerce Optimizer] ると、マーチャントはAdobe Experience Manager（AEM）Assetsを通じて商品の画像を管理できます。 この統合により、カタログレイヤーを使用してAEM Assetsから [!DNL Commerce Optimizer] カタログに高品質の商品画像を同期するためのシームレスなワークフローが提供されます。

## 主なメリット

* **一元的なアセット管理**：エンタープライズクラスのデジタルアセット管理ソリューションであるAEM Assetsで、すべての商品画像を管理します。
* **自動同期**:AEM Assetsでアセットが承認または更新されると、商品イメージは自動的に同期されます。
* **Dynamic Media 配信**:OpenAPI 機能を備えた Dynamic Media を活用して画像配信を最適化します。
* **カタログレイヤー**：商品画像はカタログレイヤーとして適用され、ベースカタログにAEM Assets画像をオーバーレイできます。

## 仕組み

この統合には、主に次の 2 つのフローがあります。

* **AEM Assetsから**：アセットが承認、却下または削除されると、イベントはAdobe パイプラインを通じてAssets Integration Service に送られます。 このサービスは、`match-by-SKU` またはカスタムマッチャー戦略を使用してアセットと製品を照合し、`product-asset` のマッピングを [!DNL Commerce Optimizer] に送信して、製品レイヤーとして保存します。

* **ACO から**:[!DNL Commerce Optimizer] で商品が更新されると、イベントはAdobe パイプラインを通じてAssets Integration Service に送られます。 サービスは、一致するアセットマッピングを ACO に同期し直します。

更新された画像は、ストアフロント API （カタログサービス、ライブ検索、製品レコメンデーション）を通じて利用できます。

### Sourceとレイヤーの設定

AEM Assets内の画像は、次のソース設定を持つカタログレイヤーとして取り込まれます。

> ソース設定の例

```json
{
  "source": {
    "locale": "en-US",
    "layer": "AEM-Assets"
  }
}
```

この設定により、AEM Assets画像がベースの商品カタログ上にオーバーレイとして適用されます。

## 前提条件

製品ビジュアルを有効にする前に、[Commerce Optimizerの前提条件 &#x200B;](../../aem-assets-integration/get-started/configure-aco.md#prerequisites) を満たしていることを確認してください。

## 設定

統合を有効にするには、[&#x200B; とAEM Assetsの詳細を指定して &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#submit-ticket) サポートチケットを作成 [!DNL Commerce Optimizer] します。 Adobe サポートは、統合を設定し、テナントをAssets Integration Service に登録します。

オンボーディングについて詳しくは、[Commerce Optimizer用AEM Assetsの設定 &#x200B;](../../aem-assets-integration/get-started/configure-aco.md) を参照してください。

### AEM Assets メタデータの設定

製品の自動マッチングを有効にするには、Commerce メタデータを使用してAEM Assetsでアセットを設定します。

必須のメタデータフィールドと手順については、[AEM Assetsの設定 &#x200B;](../../aem-assets-integration/get-started/configure-aco.md#configure-aem-assets) を参照してください。

## 製品ビジュアルの使用

統合が設定されたら、AEM Assetsを使用して商品画像を管理します。

### 製品への画像の追加

1. AEM Assets リポジトリに画像をアップロードします。

1. Commerce メタデータをアセットに追加します。 [&#x200B; アセットへのメタデータの適用 &#x200B;](../../aem-assets-integration/get-started/configure-aco.md#step-3-apply-metadata-to-assets) を参照してください。

1. 配信するアセットを承認します。 トリガーの同期では、アセットのステータスが **承認済み** である必要があります。

1. 画像は自動的に [!DNL Commerce Optimizer] に同期されます。

### AEM - Assets レイヤーを適用する

ストアフロントにAEM Assets画像を表示するには、[&#x200B; カタログビューに `AEM-Assets` レイヤーを割り当てる &#x200B;](catalog-layer.md#assign-the-aem-assets-layer-to-a-catalog-view) 必要があります。

## その他の関連リソース

* [カタログレイヤー](catalog-layer.md)
* [カタログビュー](catalog-view.md)
* [AEM Assets統合ガイド](../../aem-assets-integration/overview.md)
