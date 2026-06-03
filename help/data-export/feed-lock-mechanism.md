---
title: SaaS データ書き出し用のフィードロック機構
description: ' [!DNL SaaS Data Export] がフィード ロックを使用して、同期操作の競合を防ぎ、同時フィードの更新中にデータの整合性を保護する方法について説明します。'
role: Admin, Developer
feature: Services
source-git-commit: cfa1002653bf66afd3f6b8484b33076adcd1b7d4
workflow-type: tm+mt
source-wordcount: '357'
ht-degree: 0%

---


# SaaS データ書き出し用のフィードロック機構

[!DNL SaaS Data Export]拡張機能では、複数のプロセスが同じフィードを同時に同期しようとすると、競合状態を防ぐためにフィード ロック メカニズムを使用します。 これは、例えば、cron トリガーされた再同期が手動の`saas:resync` CLI呼び出しと重複する場合に発生する可能性があります。

## フィードロックの仕組み

cron ジョブまたは手動の`saas:resync` CLI呼び出しによってトリガーされる各フィード同期操作は、同じ順序に従います。

1. プロセスはフィードロックを取得しようとします。 ロック試行は非ブロッキングであり、ロックが別のプロセスによって既に保持されている場合はすぐに返されます。
1. ロックが&#x200B;**利用できない**&#x200B;場合、[操作はスキップされ、ログに記録されます]。

   データは失われません。 現在のプロセスが完了すると、次のcron実行で保留中の変更が取得されます。
1. ロックが&#x200B;**獲得**&#x200B;の場合、プロセスは診断目的でその名前とPIDを記録し、同期を実行します。
1. 同期が完了または失敗すると、ロックが無条件で解除され、次にスケジュールされたcron ジョブが正常に処理されます。

cronまたはCLIによって起動されたかどうかに関係なく、一度に1つの同期操作のみがフィードロックを保持できます。 フィードロックは[!DNL Adobe Commerce]の`LockManagerInterface`を通じて実装されます。 デフォルトのバックエンドはMySQLで、`GET_LOCK`関数と`RELEASE_LOCK`関数を使用します。 別のロックプロバイダーを設定するには、[&#x200B; ロックプロバイダーの設定](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/tutorials/lock-provider){target="_blank"}を参照してください。

## 予想されるログメッセージ

`commerce-data-export.log`の次のメッセージは正常であり、問題を示していません：

```json
{"feed":"products","operation":"partial sync","status":"operation skipped - process locked by \"full sync(1234)\"", ...}
```

このメッセージは、完全な再インデックスまたは`saas:resync`が既に進行中の間に、クロントリガーによる部分同期が実行を試みたときに表示されます。 スキップされた操作は失われません。 実行中のプロセスが完了してロックを解除すると、次のcron実行が取得され、保留中の変更が同期されます。

>[!NOTE]
>
>`commerce-data-export.log`に記録されたログ形式と操作タイプの一般的な情報については、[&#x200B; ログの確認とトラブルシューティング &#x200B;](troubleshooting-logging.md)を参照してください。

## このトピックの詳細ヘルプ

- [SaaS データ書き出しとデータの同期](data-synchronization.md)
- [Commerce CLIを使用したフィードの同期](data-export-cli-commands.md)
- [ロックプロバイダーの設定](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/tutorials/lock-provider){target="_blank"}
