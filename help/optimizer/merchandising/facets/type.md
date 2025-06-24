---
title: ファセットタイプ
description: ' [!DNL Adobe Commerce Optimizer] の様々なタイプのファセットについて説明します。'
badgeSaas: label="SaaS のみ" type="Positive" url="https://experienceleague.adobe.com/ja/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud ServiceおよびAdobe Commerce Optimizer プロジェクトにのみ適用されます（Adobeで管理される SaaS インフラストラクチャ）。"
source-git-commit: 3020386cd051b4453ed6b90d2c694a5bb31dfb24
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 0%

---

# ファセットのタイプ

[!DNL Adobe Commerce Optimizer] では様々なファセットタイプを使用し、関連性がある場合にのみ *フィルター* リストに表示されます。 使用可能なファセットのリストは、返される製品に応じて変わります。 その表示と動作には、次の特徴が影響します。

- ピンされたファセット – 最も一般的に使用されるファセットをリストの上部にピン留めできます。 残りのファセットは、ピン留めされたファセットの後に *並べ替えタイプ* の順序で一覧表示されます。
- 動的ファセット - [Adobe Sensei](https://www.adobe.com/sensei.html) が商品セットおよびクエリと最も関連性の高い商品を見つけた商品属性。 計算では、カタログ全体の属性メタデータが考慮され、クエリ時に、クエリに最も関連性の高いファセットが決定されます。
- 価格ファセット – 価格範囲別に製品を返します。 [*設定*](../../settings.md) ワークスペースで、選択数と価格範囲間隔を指定できます。

## ファセットラベル

[ ファセットワークスペース ](workspace.md) からファセットラベルを編集できます。

## 並べ替えタイプ

ストアフロント用にレンダリングされるすべてのファセットは、アルファベット順またはカウント順に並べ替えられます。

| 並べ替えタイプ | 説明 |
|--- |--- |
| アルファベット | ストアフロントの *フィルター* リストでは、ファセットがアルファベット順に並べ替えられます。 |
| カウント | ファセットは、返される製品の現在のセットでファセットごとに見つかった値の数で並べ替えることもできます。 |
