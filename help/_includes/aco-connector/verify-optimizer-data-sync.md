---
source-git-commit: 3d05a7307e58ea2758ac4b6f2b70d24b8ea7a5ac
workflow-type: tm+mt
source-wordcount: '144'
ht-degree: 0%

---
# Optimizer データ同期の検証

データがCommerce管理者から正常にエクスポートされ、データが[!DNL Commerce Optimizer]に正常に配信されたことを確認します。 Commerce Adminで書き出しから開始し、[!DNL Commerce Optimizer]で配信を確定します。

1. **Commerce管理者の同期ステータスを確認：**

   **[!UICONTROL System]** > **[!UICONTROL Data Transfer]** > **[!UICONTROL Data Feed Sync Status]**&#x200B;に移動します。

   ![ フィード項目のステータスがレポートされるデータフィードの同期ステータス ページ ](/help/aco-connector/assets/data-feed-sync-status.png){width="700" zoomable="yes"}

   同期を実行すると、フィード データに正常に送信されたレコードが表示されます。 フィードを選択して、詳細を表示したり、同期の問題をトラブルシューティングしたりします。

1. **確認データが[!DNL Commerce Optimizer]に配信されました：**

   [!DNL Commerce Optimizer] メニューから、**[!UICONTROL Data Sync]**&#x200B;を選択します。

   同期されたカタログデータを表示するAdobe Commerce Optimizerの![ データ同期ページ ](/help/aco-connector/assets/data-sync.png){width="700" zoomable="yes"}

   予想される商品、価格、属性が表示されることを確認します。

同期が期待どおりに機能している場合：

- **[!UICONTROL Data Feed Sync Status]**&#x200B;は、コネクタフィードに対して正常に送信されたレコードを表示しますが、未解決のアイテムレベルのエラーはありません。
- [!DNL Commerce Optimizer]の&#x200B;**[!UICONTROL Data Sync]**&#x200B;には、予想されるカタログ ソース、製品、価格および属性が一覧表示されます。

>[!TIP]
>
>データ同期に問題がある場合は、[ トラブルシューティング ](/help/aco-connector/troubleshooting.md) ガイドを参照してください。
