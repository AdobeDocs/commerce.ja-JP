---
title: 設定
description: データのソースを変更する方法と  [!DNL Product Recommendations]  視覚的なレコメンデーションを有効にする方法を説明します。
exl-id: fe37624d-c53e-40cd-b182-10f62cba74c0
source-git-commit: 458f34c45406db871ec61ff408aa624f163b6ee0
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 0%

---

# 設定

Recommendations の [SaaS データ領域の設定 ](../landing/saas.md#saas-configuration) を行うと、SaaS データ領域はカタログデータとストアフロント行動データを収集します。 [AdobeAI](https://business.adobe.com/ai.html) は、そのデータを分析し、Product Recommendations の提供に使用される商品の関連付けを計算します。

テストやステージングの非実稼動環境では、通常、現実的な製品レコメンデーションを提供するためのストアフロント行動データの量と品質はありません。 実際の買い物客の大規模な行動は、実稼動環境でのみキャプチャできます。 Adobe Commerceでは、この問題を解決するために、実稼動環境の推奨製品を実稼動以外の SaaS データスペースで使用することができます。 非実稼動環境で実際のストアフロントデータを使用すると、買い物客に表示されるレコメンデーションをプレビューし、様々なレコメンデーションタイプやプレースメントの場所を試すことができます。 異なる SaaS データ空間からのレコメンデーションは、買い物客がプレビューすることはできますが、クリックすることはできません。

ステージングオーダーは、ステージングオーダ `environmentId` を使用して記録されます。 実稼動データには影響しません。 実稼働データは `alternateEnvironmentId` を使用して取得されます。

>[!NOTE]
>
>REST を通じて製品レコメンデーションを使用する場合、`alternateEnvironmentId` パラメーターを使用して他のデータセットを指定できます。 [GraphQL](https://developer.adobe.com/commerce/webapi/graphql/schema/product-recommendations/queries/recommendations/) 経由で製品レコメンデーションを使用する場合、このパラメーターは使用できません。

## Recommendations ソースを選択

商品レコメンデーションデータのソースを変更するには、使用する行動データを含む SaaS データスペースを選択します。 開始する前に、次のことを確認します。

- ストアフロントのデータ収集は、実稼動環境に対して [ 設定および有効化 ](install-configure.md) され、行動データがAdobe Commerceに送信されていることを [ 検証 ](https://developer.adobe.com/commerce/services/shared-services/storefront-events/collector/verify/) する必要があります。
- 実稼動以外の環境カタログは、実稼動カタログと基本的に同じである必要があります。 同様のカタログを使用すると、返される製品レコメンデーションユニットが実稼動環境のレコメンデーションユニットに確実に類似します。

1. 実稼動以外のAdobe Commerce環境の管理者にログインします。

1. _管理者_ サイドバーで、**マーケティング**/_プロモーション_/**製品レコメンデーション** に移動します。

1. **設定** をクリックします。

   ![ 製品レコメンデーション設定 ](assets/settings.png)
   _設定_

1. 「_レコメンデーションソース_」セクションで、「**別の SaaS データ領域からレコメンデーションを取得**」オプションを有効にします。 _Recommendations ソース_ セクションは、実稼動以外の環境にのみ表示されます。

   _利用可能な SaaS データ スペース_ の一覧が表示されます。

   ![ 製品レコメンデーション設定 ](assets/settings-select-saas.png)
   _設定_

1. 使用する買い物客データがある SaaS データ領域を選択します。

1. **変更を保存** をクリックします。

   Adobe Commerceは、選択したデータスペースからレコメンデーションを取得するようになりました。

   >[!NOTE]
   >
   > 非実稼動ストアフロントの別の SaaS データ領域から取得したレコメンデーションを表示することはできますが、レコメンデーションをクリックすることはできません。

### 新しい SaaS データ領域の設定

1. 「Recommendations ソース」セクションで、「**設定を編集**」をクリックします。

1. 新しい [[!DNL Commerce]  サービス ](/help/landing/saas.md) を設定するには、その手順に従います。

## ビジュアルのお勧めを有効にする

[ ビジュアル製品レコメンデーション ](install-configure.md) モジュールがインストールされている場合、[ ビジュアル類似性 ](type.md#visualsim) レコメンデーションタイプを使用するには、ビジュアルレコメンデーションを有効にする必要があります。

_ビジュアルレコメンデーション_ セクションで、アクティブな位置に **ビジュアルレコメンデーションを有効にする** を設定します。
