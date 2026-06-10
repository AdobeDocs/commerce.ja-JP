---
title: ' [!DNL Adobe Commerce Optimizer Connector]のトラブルシューティング'
description: ' [!DNL Adobe Commerce] PaaS統合の [!DNL Adobe Commerce Optimizer Connector] 資格情報、カタログ同期、スコープ書き出しの問題のトラブルシューティング方法について説明します。'
role: Admin, Developer
feature: Integration, Configuration
badgePaas: label="PaaSのみ" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce on Cloud プロジェクト（Adobeで管理されるPaaS インフラストラクチャ）とオンプレミス プロジェクトにのみ適用されます。"
autotag-review: '2026-06-09T19:00:00.000Z'
TQID: 'https://experienceleague.adobe.com/ei86QuJ3nQ2d-6NRoAeJslgDxjGlZRejD-Nx-6SAVdc'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: c32adafa-ed01-4b31-997e-2413013911b0
  - id: e7dae43f-215c-4cdf-90d3-c5a461a6e669
  - id: c18ed297-2187-4aec-affb-9d9654eca6fc
subfeature_v2:
  - id: a40ebd6b-b542-4432-a730-1803ef74518d
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
source-git-commit: 1f901b4a72c10dc4e710742b98c03e88cbc8739f
workflow-type: tm+mt
source-wordcount: 273
ht-degree: 0%

---

# Adobe Commerce Optimizer コネクタのトラブルシューティング

このガイドでは、初期設定、カタログフィードの同期、スコープの書き出し設定中に[!DNL Adobe Commerce Optimizer Connector]に発生する一般的な問題を診断および解決する方法を説明します。 以下のセクションでは、資格情報とテナントの検証、データ同期エラー、および関連する[!DNL SaaS Data Export]診断について説明します。

## 資格情報またはテナントの検証が失敗する

資格情報の検証中に`aco:config:init`が失敗した場合：

- `bin/magento aco:config:show` [!DNL Adobe Commerce] CLI コマンドを実行して、保存された値を確認します。
- テナント IDが、資格情報の取得に使用するIMS組織に属していることを確認します。
- OAuth クライアントが[!DNL Commerce Optimizer]取り込みサービスに必要なスコープを持っていることを確認します（[IMS資格情報の取得](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/authentication/#obtain-ims-credentials)を参照）。

## データが同期されていません

**アイテムレベルのエラーの詳細を確認：**

1. Commerce管理者から、**[!UICONTROL System]** > **[!UICONTROL Data Transfer]** > **[!UICONTROL Data Feed Sync Status]**&#x200B;に移動します。
2. 失敗したフィードを選択して、項目ごとのエラーの詳細を表示します。

エラー処理に関する重要なポイント：

- **400 エラー**&#x200B;は再試行されません。 ペイロードで、形式が正しくないか、必須フィールドが欠落していないかを調べます。 想定される形式については、[&#x200B; コネクタフィードのフィールドマッピング &#x200B;](reference/field-mapping.md)を参照してください。
- **5xx エラー**&#x200B;は、`*_resend_failed_items` cron ジョブによって自動的に再試行されます（5分ごとに実行）。

**スコープ設定を確認：**

問題が特定のカタログソース（ストアビューコード）または価格表のみに影響する場合は、対応するweb サイトまたはストアビューの同期が無効になっているかどうかを確認します。 [&#x200B; データ書き出し設定のカスタマイズ &#x200B;](./get-started.md#customize-the-commerce-scopes-export-configuration)を参照してください。

## [!DNL SaaS Data Export]診断

ログの場所とフィード再同期コマンドを含む下位レベルの[!DNL SaaS Data Export]診断については、[[!DNL SaaS Data Export]  トラブルシューティングガイド &#x200B;](https://experienceleague.adobe.com/en/docs/commerce/saas-data-export/logs-troubleshooting/troubleshooting-logging){target="_blank"}を参照してください。
