---
title: デフォルトの自動照合
description: デフォルトの自動照合ルールを使用して、Adobe CommerceとAEM Assets統合の間でシームレスな同期を有効にし、アセットが適切なマーチャンダイジングエンティティに自動的にリンクされるようにする方法を説明します。
feature: CMS, Media, Integration
exl-id: 8a18639b-f508-456e-8d22-18e3e0fdd515
source-git-commit: d426c7878f7a66fe1047673be7c5bf65ae1949a7
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 0%

---

# デフォルトの自動照合

CommerceのAEM Assets統合は、**[!UICONTROL Match by product SKU]** AEM Assets **メタデータ設定に基づいて、デフォルトの自動マッチングメカニズム（**）を提供します。 このルールにより、**Adobe Commerce** と **AEM Assets** 間でシームレスな同期が可能になり、アセットが適切なマーチャンダイジングエンティティに自動的にリンクされるようになります。

## 自動マッチングメカニズムの設定

1. Commerce管理者から、**[!UICONTROL Store]** /設定/ **[!UICONTROL ADOBE SERVICES]** / **[!UICONTROL AEM Assets Integration]** に移動します。

1. 一致するルールとして **[!UICONTROL Match by SKU]** を指定します。

   ![&#x200B; デフォルトの自動照合ルール &#x200B;](../assets/ootb-matching-rule.png){width="600" zoomable="yes"}

1. AEM Assetsでアセットの ID に使用するメタデータフィールド名を入力します。

   >[!NOTE]
   >
   > 標準のオンボーディングプロセスに従った場合は、この値を `commerce:skus` に設定する必要があります。

## 自動マッチングの仕組み

Commerce管理で **[!UICONTROL Match by product SKU]** 一致ルールが設定されている場合、Commerce アセットファイルは、各ファイルに設定されているアセットメタデータに基づいてAEM AssetsからCommerce プロジェクトに自動的に同期されます。 メタデータは、**AEM Assets オーサー** 環境の「AEM **Commerce**」タブから設定します。

1. AEM Assetsで、`Eligible for Commerce` フィールドを `Yes` に設定して画像メタデータを更新し、Adobe Commerceの関連付けを追加します。

   ![&#x200B; メタデータの例 &#x200B;](../assets/metadata-commerce-yes.png){width="600" zoomable="yes"}

1. アセットを関連する製品 SKU にリンクするメタデータ（[!UICONTROL SKU]、[!UICONTROL position]、[!UICONTROL role]）を設定します。

   >[!NOTE]
   >
   > 1 つのアセットを複数の製品に使用する場合は、関連する SKU ごとにメタデータを設定します。

1. 「`Basic`」タブで、「_[!UICONTROL Review Status]_」フィールドのデフォルト値を `approved` に設定します。

   ![&#x200B; メタデータの例 &#x200B;](../assets/metadata-review-status.png){width="600" zoomable="yes"}

このアプローチにより、デジタルアセットがAdobe Commerceで適切にリンクされ、表示されるようになります。 また、マーチャンダイザーやマーケターがAEM Assets内で直接ロールとアセットの位置を管理できるようになり、すべてのエンゲージメントチャネルをまたいで画像の選択と注文のための一貫性のある一元化されたメカニズムが提供されます。
