---
title: カタログデータの同期の監視
description: カタログデータの同期を検証し、データフィードの同期ステータスを介して[!DNL Adobe Commerce]と[!DNL Adobe Commerce Optimizer]の間でコネクタフィードを手動で再同期する方法について説明します。
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
feature: Integration, Configuration
badgePaas: label="PaaSのみ" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce on Cloud プロジェクト（Adobeで管理されるPaaS インフラストラクチャ）とオンプレミス プロジェクトにのみ適用されます。"
last-update: 2026-10-01
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
    internal-label: Commerce on Prem
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
    internal-label: Commerce on Cloud
feature_v2:
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
  - id: e7dae43f-215c-4cdf-90d3-c5a461a6e669
    internal-label: Admin tools and workspace
  - id: cc04bd17-78d5-5120-8c3d-1b8a57e49280
    internal-label: Integration
subfeature_v2:
  - id: a40ebd6b-b542-4432-a730-1803ef74518d
    internal-label: Data Transfer
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
topic_v2:
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
    internal-label: Data management
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
    internal-label: Data integration
source-git-commit: c76e776250d9f996daf61d3cf62e2070803e998c
workflow-type: tm+mt
source-wordcount: '378'
ht-degree: 0%
---
# カタログデータの同期を監視する

[!DNL Adobe Commerce Optimizer Connector]を設定すると、スケジュールされたcron ジョブを通じて、ほとんどのカタログ更新が自動的に同期されます。 自動同期の仕組みについて詳しくは、[&#x200B; コネクタ同期パイプライン &#x200B;](connector-sync-pipeline.md)を参照してください。 このトピックのツールを使用して、製品、価格、カテゴリのデータが[!DNL Adobe Commerce Optimizer]に達することを確認し、必要に応じてフィードを手動で再同期します。

## データ同期が機能していることを確認します {#verify-that-the-data-sync-is-working}

{{$include /help/_includes/aco-connector/verify-optimizer-data-sync.md}}

## データを手動で再同期 {#manually-resync-data}

部分同期と自動再試行で同期の問題が解決されない場合は、カタログデータを手動で再同期できます。 選択するオプションは、問題の発生場所と必要なコントロールの量によって異なります。

| タスク | オプション | メモ |
| --- | --- | --- |
| 製品が見つからない場合に、同期ステータスを確認し、アップストリームシステムから再同期します | **アップストリームシステムの再同期** | [!DNL Commerce Optimizer]で、**[!UICONTROL Data Sync]**&#x200B;を選択し、予想されるカタログ ソース、製品、価格、属性が表示されることを確認します。 製品が見つからない場合は、**[!UICONTROL Data Feed Sync Status]** ページまたはCommerce CLIを使用して、アップストリーム [!DNL Adobe Commerce] インスタンスから再同期します（次の行を参照）。 |
| 選択した失敗または問題のあるコネクタフィード項目の再同期 | Commerce Admin **の**&#x200B;[!UICONTROL Data Feed Sync Status] ページ | エクスポートのステータスを監視し、選択したコネクタフィード項目をCommerce管理者から再同期します。 [&#x200B; データ同期が機能していることを確認してください](#verify-that-the-data-sync-is-working)。 |
| 操作制御によるターゲットコネクタフィードの再同期 | **Commerce CLI** | コネクタフィードの[!DNL Adobe Commerce] インスタンスから`saas:resync`を実行します。 Commerce CLI[&#128279;](../data-export/data-export-cli-commands.md)と[&#x200B; サポートされているフィード &#x200B;](reference/connector-reference.md#supported-feeds)を使用して フィードを同期するを参照してください。 |

>[!MORELIKETHIS]
>
> - [&#x200B; コネクタ同期パイプライン &#x200B;](connector-sync-pipeline.md) – 自動同期、cron スケジュール、エラー処理の仕組みについて説明します
> - [&#x200B; データ量と同期時間の見積もり](reference/estimate-data-volume-sync-time.md) – 予想される同期時間の計算
> - [&#x200B; トラブルシューティング &#x200B;](troubleshooting.md) – 資格情報、同期、スコープ書き出しの問題を診断します
> - [Commerce スコープの書き出し設定をカスタマイズ &#x200B;](./get-started.md#customize-the-commerce-scopes-export-configuration) — スコープレベルごとにフィードを設定し、ビヘイビアーを有効または無効にし、管理手順を実行します
> - [&#x200B; コネクタ モジュールとフィード エンドポイント &#x200B;](reference/connector-reference.md) — モジュール、API エンドポイント、サポートされているフィードの確認
> - Commerce Admin[&#128279;](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-feed-sync-status){target="_blank"}の データフィードの同期ステータス ページ – フィードのステータスをモニタリングするために使用できるフィールドと機能について詳しく説明します
> - [&#x200B; データ同期ダッシュボード in [!DNL Commerce Optimizer]](https://experienceleague.adobe.com/en/docs/commerce/optimizer/setup/data-sync){target="_blank"} — カタログデータ同期の監視に使用できるフィールドとアクションに関する参照ドキュメント
