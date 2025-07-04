---
title: デフォルトの自動照合
description: デフォルトの自動照合ルールを使用して、Adobe Commerceと製品ビジュアルのシームレスな同期を有効にし、アセットが適切なマーチャンダイジングエンティティに自動的にリンクされるようにする方法を説明します。
feature: CMS, Media, Integration
source-git-commit: 3ecc429003490235211a812af064d1b10d053e38
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 0%

---


# デフォルトの自動照合

[!DNL Product Visuals] の統合により、**AEM Assets** のメタデータ設定に基づいて、デフォルトの自動マッチングメカニズム（**[!UICONTROL Match by product SKU]**）が提供されます。 このルールにより、**Adobe Commerce** と **AEM Assets** 間でシームレスな同期が可能になり、商品のビジュアルが適切なマーチャンダイジングエンティティに自動的にリンクされます。


## 自動マッチングメカニズムの設定

1. Commerce管理者から、**[!UICONTROL Store]** /設定/ **[!UICONTROL ADOBE SERVICES]** / **[!UICONTROL AEM Assets Integration]** に移動します。

1. 一致するルールとして **[!UICONTROL Match by SKU]** を指定します。

   ![ デフォルトの自動照合ルール ](../assets/ootb-matching-rule.png){width="600" zoomable="yes"}

1. AEM Assetsでアセットの ID に使用するメタデータフィールド名を入力します。

   >[!NOTE]
   >
   > 標準のオンボーディングプロセスに従った場合は、この値を `commerce:skus` に設定する必要があります。

## 自動マッチングの仕組み

Commerce管理で **[!UICONTROL Match by product SKU]** 一致ルールが設定されている場合、Commerce アセットファイルは、各ファイルに設定されているアセットメタデータに基づいてAEM AssetsからCommerce プロジェクトに自動的に同期されます。 メタデータは、**AEM Assets オーサー** 環境の「AEM **Commerce**」タブから設定します。

![ メタデータの例 ](../assets/example-metadata.png){width="600" zoomable="yes"}

1. AEM Assetsで、画像メタデータを更新して、Adobe Commerceの関連付け `Commerce=yes` を追加します。

1. アセットを関連する製品 SKU にリンクするメタデータ（[!UICONTROL SKU]、[!UICONTROL position]、[!UICONTROL role]）を設定します。

   >[!NOTE]
   >
   > 1 つのアセットを複数の製品に使用する場合は、関連する SKU ごとにメタデータを設定します。

このアプローチにより、デジタルアセットがAdobe Commerceで適切にリンクされ、表示されるようになります。 また、マーチャンダイザーやマーケターがAEM Assets内で直接ロールとアセットの位置を管理できるようになり、すべてのエンゲージメントチャネルをまたいで画像の選択と注文のための一貫性のある一元化されたメカニズムが提供されます。
