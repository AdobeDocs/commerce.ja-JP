---
title: 手動でのアセット選択
description: マーケターやマーチャンダイザーがCommerce管理に統合されたAEM アセットセレクターを使用して、AEM AssetsからAdobe Commerceに画像を簡単に追加し、アセット管理を効率化する方法を説明します。
feature: CMS, Media, Integration
source-git-commit: d362e6e821e81f6da99c420881e1e1b1058bbd45
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---

# 手動でのアセット選択

マーケターやマーチャンダイザーは **&#x200B;**&#x200B;AEM アセットセレクターを使用して、AEM AssetsからAdobe Commerceに画像を簡単に追加でき、アセット管理プロセスを合理化できます。 この方法では、アセットの選択を [!DNL DAM (Digital Asset Management system)] で確認および承認されたアセットに限定することで、ブランドの一貫性とコンプライアンスを確保します。

**AEM アセットセレクター** は、AEM Assets プロジェクトの IMS クライアント ID がCommerce管理者で設定されている場合に使用できます。 [AEM アセットセレクターの設定 ] を参照してください（#configure-the-aem-asset-selector-in-adobe-commerce。

**AEM アセットセレクター** の統合が設定されると、マーケターとマーチャンダイザーは次のことができます。

* カテゴリ画像を簡単に管理し、ブランドやキャンペーンのガイドラインに合わせることができます。
* [!BADGE PaaS のみ &#x200B;]{type=Informative tooltip="クラウドプロジェクト上のAdobe Commerceにのみ適用されます（Adobeが管理する PaaS インフラストラクチャ）。"} 視覚的にリッチなコンテンツを表示するには、ページビルダーで直接アセットを割り当てます。

>[!NOTE]
>
> AEM アセットセレクターは、AEMをオーサリングアプリケーションと統合するためのAEM Assets Assets フロントエンドコンポーネントです。 このコンポーネントについて詳しくは、&lbrace;2[AEM as a Cloud Service ユーザーガイド ](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/assets/manage/asset-selector/overview-asset-selector){target=_blank} マイクロフロントエンドアセットセレクター *を参照してください。*

## 主なメリット

Adobe Commerce管理パネル内にAEM アセットセレクターを埋め込むと、次のような主な利点があります。

* **ブランドの一貫性** 承認済みのアセットのみを表示し、ストアフロントでの古い画像や準拠していない画像のリスクを最小限に抑えます。

* **効率** - マーケターとマーチャンダイザーは、異なるプラットフォーム間を切り替えることなく、アセットをすばやく割り当てることができます。

* **Collaborationの効率化** - DAM から画像を直接選択でき、手動のダウンロードやアップロードを行わなくても、シームレスなチームワークを促進します。

* **コンテンツ品質の向上** – 製品ページ、カテゴリおよびページビルダー全体で、最適化された高解像度の画像を確実に使用します。

![ アセットセレクター ](../assets/asset-selector.png){width="600" zoomable="yes"}

## Adobe CommerceでのAEM アセットセレクターの設定

1. Commerce管理者から、**[!UICONTROL Store]** /設定/ **[!UICONTROL ADOBE SERVICES]** / **[!UICONTROL AEM Assets Integration]** に移動します。

1. **[!UICONTROL IMS Client ID]** フィールドに入力します。

1. **保存** 設定。

## 次の手順

* [アセットセレクターを使用したカテゴリ画像の管理](../manage-assets.md#category-images)
* [ページビルダーコンテンツでの画像の管理](../manage-assets.md#using-aem-asset-selector-in-page-builder)
