---
source-git-commit: e7d9c056ef8d565b4a143b05ff4e06d607fbfa8e
workflow-type: tm+mt
source-wordcount: '139'
ht-degree: 0%

---
# Commerce サービスのデータ同期を確認する

データの同期が機能していることを確認するには、[!DNL Adobe Commerce]から正常に書き出され、接続されているCommerce サービスにデータが正常に配信されたことを確認します。 デプロイメントにダッシュボードを使用して、両方の手順を確認します。

エクスポートから開始し、配信を確認します。

1. Commerce Adminで同期ステータスを確認します。

   **[!UICONTROL System]** > **[!UICONTROL Data Transfer]** > **[!UICONTROL Data Feed Sync Status]**&#x200B;に移動します。

   ![&#x200B; フィード項目のステータスがレポートされるデータフィードの同期ステータス ページ &#x200B;](/help/data-export/assets/data-feed-sync-status.png){width="800" zoomable="yes"}

   同期を実行すると、フィード データに正常に送信されたレコードが表示されます。 フィードを選択して、詳細を表示したり、同期の問題をトラブルシューティングしたりします。

1. データが接続されたCommerce サービスに配信されたことを確認します。

   Commerce管理者から、**[!UICONTROL System]** > **[!UICONTROL Data Transfer]** > **[!UICONTROL Data Management Dashboard]**&#x200B;に移動します。

   ![接続されたCommerce サービスに同期されたカタログ データを表示するData Management ダッシュボード &#x200B;](/help/data-export/assets/data-management-dashboard.png){width="700" zoomable="yes"}

   予想される商品、価格、属性が表示されることを確認します。

>[!TIP]
>
>データ同期に関する追加の問題がある場合は、[&#x200B; ログの確認とトラブルシューティング &#x200B;](/help/data-export/troubleshooting/logging.md)を参照してください。

