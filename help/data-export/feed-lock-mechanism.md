---
title: SaaS データ書き出し用のフィードロック機構
description: ' [!DNL SaaS Data Export] がフィード ロックを使用して、同期操作の競合を防ぎ、同時フィードの更新中にデータの整合性を保護する方法について説明します。'
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
feature: Services
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: 182aa9ce819807d1ede85c4fa459714e7dfe0478
workflow-type: tm+mt
source-wordcount: 355
ht-degree: 0%

---


# SaaS データ書き出し用のフィードロック機構

[!DNL SaaS Data Export]拡張機能では、複数のプロセスが同じフィードを同時に同期しようとすると、競合状態を防ぐためにフィード ロック メカニズムを使用します。 これは、例えば、cron トリガーされた再同期が手動の`saas:resync` CLI呼び出しと重複する場合に発生する可能性があります。

## フィードロックの仕組み

cron ジョブまたは手動の`saas:resync` CLI呼び出しによってトリガーされる各フィード同期操作は、同じ順序に従います。

1. プロセスはフィードロックを取得しようとします。 ロック試行は非ブロッキングであり、ロックが別のプロセスによって既に保持されている場合はすぐに返されます。
1. ロックが&#x200B;**利用できない**&#x200B;場合、操作はスキップされ、ログに記録されます。

   データは失われません。 現在のプロセスが完了すると、次のcron実行で保留中の変更が取得されます。
1. ロックが&#x200B;**獲得**&#x200B;の場合、プロセスは診断目的でその名前とPIDを記録し、同期を実行します。
1. 同期が完了または失敗すると、ロックが無条件で解除され、次にスケジュールされたcron ジョブが正常に処理されます。

cronまたはCLIによって起動されたかどうかに関係なく、一度に1つの同期操作のみがフィードロックを保持できます。 フィードロックは[!DNL Adobe Commerce]の`LockManagerInterface`を通じて実装されます。 デフォルトのバックエンドはMySQLで、`GET_LOCK`関数と`RELEASE_LOCK`関数を使用します。 別のロックプロバイダーを設定するには、[&#x200B; ロックプロバイダーの設定](https://experienceleague.adobe.com/ja/docs/commerce-operations/installation-guide/tutorials/lock-provider){target="_blank"}を参照してください。

## 予想されるログメッセージ

`commerce-data-export.log`の次のメッセージは正常であり、問題を示していません：

```json
{"feed":"products","operation":"partial sync","status":"operation skipped - process locked by \"full sync(1234)\"", ...}
```

このメッセージは、完全な再インデックスまたは`saas:resync`が既に進行中の間に、クロントリガーによる部分同期が実行を試みたときに表示されます。 スキップされた操作は失われません。 実行中のプロセスが完了してロックを解除すると、次のcron実行が取得され、保留中の変更が同期されます。

>[!NOTE]
>
>`commerce-data-export.log`に記録されたログ形式と操作タイプの一般的な情報については、[&#x200B; ログの確認とトラブルシューティング &#x200B;](troubleshooting/logging.md)を参照してください。

>[!MORELIKETHIS]
>
> - [SaaS データ書き出しとデータの同期](sync-overview.md)
> - [Commerce CLIを使用してフィードを同期](data-export-cli-commands.md)
> - [&#x200B; コネクタ同期パイプライン &#x200B;](../aco-connector/connector-sync-pipeline.md)
> - [&#x200B; ロックプロバイダーの設定](https://experienceleague.adobe.com/ja/docs/commerce-operations/installation-guide/tutorials/lock-provider){target="_blank"}
