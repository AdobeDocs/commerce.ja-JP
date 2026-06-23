---
title: ' [!DNL Adobe Commerce Optimizer Connector] 同期の管理'
description: カタログデータの同期を検証し、 [!DNL Adobe Commerce] から [!DNL Adobe Commerce Optimizer]の間でコネクタフィードを手動で再同期する方法について説明します。
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
feature: Integration, Configuration
badgePaas: label="PaaSのみ" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce on Cloud プロジェクト（Adobeで管理されるPaaS インフラストラクチャ）とオンプレミス プロジェクトにのみ適用されます。"
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047id: b974b164-8a4e-43b8-a9e2-8e67ec131677id: cdf0c6dd-1717-4e20-9530-a24eee57088b
feature_v2: id: dac87252-6066-4d6e-a9d2-f6d84c323de7id: c32adafa-ed01-4b31-997e-2413013911b0id: e7dae43f-215c-4cdf-90d3-c5a461a6e669
subfeature_v2: id: a40ebd6b-b542-4432-a730-1803ef74518d
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2: id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: 0bfd368c50707692c7a0adda6e70e3776bd9692a
workflow-type: tm+mt
source-wordcount: 349
ht-degree: 0%

---

# [!DNL Commerce Optimizer]への同期を管理

[!DNL Adobe Commerce Optimizer Connector]を設定すると、スケジュールされたcron ジョブを通じて、ほとんどのカタログ更新が自動的に同期されます。 自動同期の仕組みについて詳しくは、[ コネクタ同期パイプライン ](connector-sync-pipeline.md)を参照してください。 このトピックのツールを使用して、データが[!DNL Adobe Commerce Optimizer]に達することを確認し、必要に応じてフィードを手動で再同期します。

## データ同期が機能していることを確認します {#verify-that-the-data-sync-is-working}

{{$include /help/_includes/aco-connector/verify-optimizer-data-sync.md}}

## データを手動で再同期 {#manually-resync-data}

部分同期と自動再試行で同期の問題が解決されない場合は、カタログデータを手動で再同期できます。 選択するオプションは、問題の発生場所と必要なコントロールの量によって異なります。

| タスク | オプション | メモ |
| --- | --- | --- |
| 製品が見つからない場合に、同期ステータスを確認し、アップストリームシステムから再同期します | **アップストリームシステムの再同期** | [!DNL Commerce Optimizer]で、**[!UICONTROL Data Sync]**&#x200B;を選択し、予想されるカタログ ソース、製品、価格、属性が表示されることを確認します。 製品が見つからない場合は、**[!UICONTROL Data Feed Sync Status]** ページまたはCommerce CLIを使用して、アップストリーム [!DNL Adobe Commerce] インスタンスから再同期します（次の行を参照）。 |
| 選択した失敗または問題のあるコネクタフィード項目の再同期 | Commerce Admin **の**[!UICONTROL Data Feed Sync Status] ページ | エクスポートのステータスを監視し、選択したコネクタフィード項目をCommerce管理者から再同期します。 [ データ同期が機能していることを確認してください](#verify-that-the-data-sync-is-working)。 |
| 操作制御によるターゲットコネクタフィードの再同期 | **Commerce CLI** | Adobe Commerce インスタンスから`saas:resync`を実行して、コネクタフィードを取得します。 Commerce CLI](../data-export/data-export-cli-commands.md)と[ サポートされているフィード ](reference/connector-reference.md#supported-feeds)を使用して[ フィードを同期するを参照してください。 |

>[!MORELIKETHIS]
>
> - [ コネクタ同期パイプライン ](connector-sync-pipeline.md) – 自動同期、cron スケジュール、エラー処理の仕組みについて説明します
> - [ データ量と同期時間の見積もり](reference/estimate-data-volume-sync-time.md) – 予想される同期時間の計算
> - [ トラブルシューティング ](troubleshooting.md) – 資格情報、同期、スコープ書き出しの問題を診断します
> - [ コネクタ モジュールとフィード エンドポイント ](reference/connector-reference.md) — モジュール、API エンドポイント、サポートされているフィードの確認
> - Commerce Admin](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-feed-sync-status){target="_blank"}の[ データフィードの同期ステータス ページ – フィードのステータスをモニタリングするために使用できるフィールドと機能について詳しく説明します
> - [ データ同期ダッシュボード in [!DNL Commerce Optimizer]](https://experienceleague.adobe.com/en/docs/commerce-optimizer/data-sync/data-sync){target="_blank"} — カタログデータ同期の監視に使用できるフィールドとアクションに関する参照ドキュメント
