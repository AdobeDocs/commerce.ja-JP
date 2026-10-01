---
source-git-commit: a3ade1a31d3c2905b601f71bda118de89c43cf59
workflow-type: tm+mt
source-wordcount: '109'
ht-degree: 0%
---
# [!DNL Commerce Optimizer] インスタンスの詳細を取得

_テナント ID_&#x200B;を、[!DNL Commerce Optimizer] インスタンス [[!DNL Instance details]  ページ ](/help/optimizer/get-started.md#manage-instances)の&#x200B;_[!DNL Instance Id]_フィールドまたはインスタンスへのアクセスに使用したURLから取得します。 例：`https://experience.adobe.com/#/@<your organization>/in:<tenant>/commerce-optimizer-studio/home`。

1. Commerce管理者から「**[!UICONTROL Adobe Commerce Optimizer]**」を選択し、手順を含む設定ページを表示します。

   ![[!DNL Commerce Optimizer]設定ページ ](/help/aco-connector/assets/aco-connector-admin-installation.png){width="500" zoomable="yes"}

1. コマンドラインから、[SSH](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/develop/secure-connections)を使用して[!DNL Adobe Commerce] ステージング環境に接続します。

1. 統合を設定するには、次の[!DNL Adobe Commerce] CLI コマンドを実行し、プレースホルダー値を[!DNL Commerce Optimizer] プロジェクトの値に置き換えます。

   ```shell
   bin/magento aco:config:init --org_id=your-org --tenant_id=your-tenant --client_id=your-client-id --client_secret=your-secret
   ```

1. Commerce管理者に戻り、[!UICONTROL Adobe Commerce Optimizer] オプションを選択して、接続を確認します。

   オプションを選択すると、新しいタブで[!DNL Commerce Optimizer] UIが開きます。
