---
title: SaaS データ書き出しモジュール
description: ' [!DNL SaaS Data Export] に含まれるMagento モジュールパッケージと、データ収集、変換、Adobe SaaS サービスへの送信における役割について説明します。'
autotag-review: '2026-06-17T15:08:59.000Z'
role: Developer
feature: Services
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: cc250cf1-34eb-4863-80d0-d170d45ea067
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: 182aa9ce819807d1ede85c4fa459714e7dfe0478
workflow-type: tm+mt
source-wordcount: 111
ht-degree: 0%

---


# SaaS データ書き出しモジュール

[!DNL SaaS Data Export]は2つのモジュールグループで構成されています。1つ目はデータ収集とインデックス作成、2つ目はHTTP転送と送信です。

これらのモジュールは、エンティティの変更検出、フィードのインデックス作成、データ抽出、スキーマ定義を処理します。
次の表は、フレームワークレベルのモジュールのみを示します。使用可能なモジュールの完全なリストは、インストールされているパッケージによって異なります。

| モジュール | 目的 | キークラス |
| --- | --- |--- |
| `DataExporter` | コアフレームワーク：インデクサー、フィードテーブル、ハッシュ、再試行、ロック | `FeedIndexer`, `FeedIndexMetadata`, `FeedMetadataPool`, `FeedLockManager` |
| `QueryXml` | データ収集用のXML ベースのクエリ DSL | `QueryFactory`, `QueryProcessor`, `SelectBuilder` |
| `SaaSCommon` | 共有HTTP トランスポート、再試行、CLI （`saas:resync`）、再同期オーケストレーション | `ExportFeed`, `SubmitFeed`, `ResyncManager`, `ResyncManagerPool`, `ProgressBarManager` |

これらのモジュールが同期中にどのように連携するかを確認するには、[SaaS データ書き出しパイプライン &#x200B;](../sync-overview.md)を参照してください。

>[!MORELIKETHIS]
>
>- [同期の仕組み](../sync-overview.md)
>- [&#x200B; テーブル スキーマをフィード &#x200B;](feed-table-reference.md)
>- [SaaS データ書き出し拡張機能の管理](../manage-extension.md)
