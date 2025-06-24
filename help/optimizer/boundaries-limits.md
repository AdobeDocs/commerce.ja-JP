---
title: 境界と制限
description: ' [!DNL Adobe Commerce Optimizer] の境界と制限について説明します。'
role: Admin, Developer
badgeSaas: label="SaaS のみ" type="Positive" url="https://experienceleague.adobe.com/ja/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud ServiceおよびAdobe Commerce Optimizer プロジェクトにのみ適用されます（Adobeで管理される SaaS インフラストラクチャ）。"
source-git-commit: 553490762ef10e43ccce1654acec59aeb83bb5f9
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 0%

---

# 境界と制限

[!DNL Adobe Commerce Optimizer] の境界と制限を次に示します。

## カタログ

- カタログの取り込み速度は、1 分あたり 1000 個、1 分あたり 5000 個の製品が保証されています。
- 1 日あたりの製品アップデートの基本数は 1,000,000 です。
- 1 つのインスタンスで許可される SKU の合計数は 250,000 です。 
- カタログソースの最大数は 50 です。
- 製品ごとのバリアントの数は 10,000 です。
- 製品サイズは 200 KB 以下にする必要があります。

## 価格

- 価格帳簿の最大数は 1,000 です。

## 製品の検出とストアフロント

- 1 回の検索リクエストで返される製品の数は 100 です。
- フィルタリング可能な属性の最大数は 200 です。
- 検索可能な属性の最大数は 200 です。
- 並べ替え可能な属性の最大数は 50 です。
- ファセットの最大数は 100 です。 すべてのファセットは、フィルタリング可能な属性である必要があります。
- 単一のファセット cat が返すオプションの最大数は 100 です。これは、サポートリクエストごとに増やすことができます。

## カタログのビューとポリシー

- テナントごとのカタログビューの最大数は 1000 です。
- 1 つのカタログビューに割り当てられるポリシーの最大数は 10 です。
- 1 つのポリシーで使用できる属性値の最大数は 100 です。 

## 推奨事項

- カテゴリや属性の包含や除外はサポートされていません。
- [!DNL Adobe Commerce Optimizer] では、レコメンデーションをプレビューできません。
