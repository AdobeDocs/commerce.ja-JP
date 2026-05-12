---
title: ファセットWorkspace
description: ' [!DNL Live Search]  ファセット ワークスペースを中心に学習します。'
exl-id: 7108e41b-44a7-4943-b20f-6ee544d099e9
TQID: https://experienceleague.adobe.com/LsVM4inUqk2EozfVN--FH1Ukggt8A8QBIQXW-SmnxZs
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 33cd0e217447351b690646ec8d230f76060a74da
workflow-type: tm+mt
source-wordcount: 229
ht-degree: 0%

---

# ファセットWorkspace

*ファセット* ワークスペースには、現在使用可能なすべてのファセットが一覧表示され、ファセットの設定と管理に必要なツールにアクセスできます。 ピン留めされたファセットは、既存のファセットのリストの最初に表示され、次に動的ファセットが表示されます。 リストをフィルタリングして、すべてのファセットを表示したり、ピン留めまたは動的なファセットのみを表示したりできます。

![&#x200B; ファセット ワークスペース &#x200B;](assets/faceting-workspace.png)

## 範囲の設定

Adobe Commerceのインストールに複数のストアビューが含まれる場合は、**Scope**&#x200B;をファセット設定が適用される[&#x200B; ストアビュー](https://experienceleague.adobe.com/docs/commerce-admin/start/setup/websites-stores-views.html#scope-settings)に設定します。

## リストをフィルター

1. 「**Filter by**」コントロールをクリックします。
1. 次のいずれかのオプションを選択します。

   * すべてのフィルター
   * ピン留め
   * 動的

## ファセットを追加

1. 「**ファセットを追加**」をクリックします。
1. 詳しい手順については、[&#x200B; ファセットの追加](facets-add.md)を参照してください。

## 列の説明

| 列 | 説明 |
|--- |--- |
| （最初の列） | 買い物客に表示される[label](facets-type.md)によってピン留めされたファセットと動的ファセットをリストします。 |
| 並べ替えタイプ | ファセット値の[並べ替え順序](facets-type.md)。 ファセットは、すべての[!DNL Commerce] ストアフロントでアルファベット順に並べ替えられます。 [ ヘッドレス ]実装の場合、ファセットはアルファベット順またはカウント順に並べ替えることができます。 オプション：アルファベット順、カウント（ヘッドレスのみ） |
| 最大値 | ストアフロントでフィルターとして使用できるファセット値の数（最大10）。 |

## コントロール

| 制御 | 説明 |
|--- |--- |
| ファセットを追加 | [&#x200B; ファセットエディター](facets-add.md)を開きます。 |
| フィルター条件 | リストに表示されるファセットの[&#x200B; タイプ &#x200B;](facets-type.md)を決定します。 オプション：すべて、ピン留め、ダイナミック |
