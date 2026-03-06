---
title: ファセットWorkspace
description: ' [!DNL Adobe Commerce Optimizer] でファセットワークスペースを使用する方法を説明します。'
badgeSaas: label="SaaS のみ" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud Serviceおよびプロジェクトのみ（Adobe [!DNL Adobe Commerce Optimizer]  管理される SaaS インフラストラクチャ）に適用されます。"
exl-id: bd977769-6565-48ca-b5aa-963a217df3ea
source-git-commit: c7c21df464685783b5fae1c99d60ca91e0c334d2
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 1%

---

# ファセットWorkspace

*ファセット* ワークスペースには、現在使用可能なすべてのファセットが一覧表示され、ファセットの設定と管理に必要なツールにアクセスできます。 ピン留めされたファセットは、最初に既存のファセットのリストに表示され、次に動的ファセットが表示されます。 ファセットのリストを検索できます。

![ ファセットWorkspace](../../assets/facet-workspace.png)

## フィールドの説明

| フィールド | 説明 |
|--- |--- |
| ファセットの作成 | [ ファセットエディター ](add.md) を開きます。 |
| ラベル | ストアフロントに表示される [ ファセットラベル ](type.md#facet-labels) は、ブランドとの一貫性を保つために編集できます。 |
| 並べ替えタイプ | ファセットの [ 並べ替え ](type.md#sort-type) に使用するメソッド。 すべてのストアフロント [!DNL Adobe Commerce Optimizer]、ファセットをアルファベット順および `Count` 順に並べ替えます。 オプション：<br /> アルファベット順 – ファセットをアルファベット順に並べ替えます。<br />Count – 見つかった一致数に基づいてファセットを並べ替えます。 |
| 最大値 | 各ファセットのストアフロントに表示できる値の最大数。 値の範囲を表すファセットは、均等に配分されます。 有効なエントリ：0～100、デフォルト：8。 |

## コントロール

| 制御 | 説明 |
|--- |--- |
| ![ ピンセレクター ](../../assets/btn-pin-blue.png) | *フィルター* リストの上部にファセットをピン留めまたはピン留めを解除します。 |
| ![ 詳細セレクター ](../../assets/btn-more.png) | 選択したファセットに適用できるその他のアクションのメニューを表示します。 オプション：編集、削除 |
