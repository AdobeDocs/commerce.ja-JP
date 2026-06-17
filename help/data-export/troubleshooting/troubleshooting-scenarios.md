---
title: ' [!DNL SaaS Data Export]のシナリオのトラブルシューティング'
description: 設定の誤り、インデクサー設定、または同期結果の誤った解釈によって発生する予期しない [!DNL SaaS Data Export] 同期動作を診断して解決する方法について説明します。
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
feature: Integration, Configuration
badgePaas: label="PaaSのみ" type="Informative" url="https://experienceleague.adobe.com/ja/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce on Cloud プロジェクト（Adobeで管理されるPaaS インフラストラクチャ）とオンプレミス プロジェクトにのみ適用されます。"
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
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
source-git-commit: 182aa9ce819807d1ede85c4fa459714e7dfe0478
workflow-type: tm+mt
source-wordcount: 991
ht-degree: 0%

---


# [!DNL SaaS Data Export]のシナリオのトラブルシューティング

このページでは、一般的に設定ミスや同期結果の誤解釈が原因で[!DNL SaaS Data Export]を操作する際に発生する可能性のある動作について説明します。 以下の説明を使用して、根本原因を特定し、適切な解決策を適用します。

## Commerce サービスで設定可能またはバンドル製品が見つからない {#configurable-bundle-missing}

**問題：**&#x200B;設定可能な製品またはバンドル製品のステータスは[!DNL Adobe Commerce]で&#x200B;*有効*&#x200B;ですが、ストアフロントで返されないか、Commerce SaaS サービスで&#x200B;*無効* ステータスで表示されます。

**原因：**&#x200B;複合製品の有効な状態は、親製品の状態だけでなく、子製品の状態によって異なります。 CommerceのSaaS サービスは、次の計算済みステータスを反映します。

- **構成可能な製品** – 少なくとも1つの製品バリアントを有効にする必要があります。
- **バンドル製品** – 必要なバンドルオプションごとに、少なくとも1つの製品を有効にする必要があります。

これらの条件が満たされない場合、親の製品は、独自のステータスが&#x200B;*有効*&#x200B;に設定されていても、無効として扱われます。

**解決策：**

- 設定可能な製品について、少なくとも1つの関連するシンプルな製品バリエーションが有効になっていて、正しいweb サイトとストアビューに割り当てられていることを確認します。
- バンドル製品の場合、必要な各バンドルオプションに少なくとも1つの有効な子製品があることを確認します。 すべての無効な子に対して必須オプションを指定すると、バンドル全体が無効として扱われます。
- 適切な子製品を有効にした後、再同期をトリガーするか、次回のスケジュールされた同期を待ってから、Commerce SaaS サービスで更新されたステータスを確認します。

## カタログ価格ルールのアクティブ化後に価格が更新されない {#prices-not-updated}

**問題：** スケジュールされた更新機能を使用してカタログ価格ルールをアクティブ化した後、価格は更新されません。 スケジュールされた更新が適用された後、`commerce-data-export.log`には`prices` フィードの`synced: 0`が表示されます。

**原因：** カタログ価格ルールに予定更新を使用すると、クローングループ間で競合状態が発生する可能性があります。 `catalog_data_exporter_product_prices` インデクサーは、依存関係である`catalogrule_product` インデックスの再構築が完了する前に実行される可能性があります。 その結果、価格エクスポーターは古いデータを読み取り、変更を書き出しません。

**解決策：**

この問題の即時の修正は回避策です。両方のcron グループを順次実行するように設定して、レース条件を排除します。

1. **[!UICONTROL Stores]** > **[!UICONTROL Configuration]** > **[!UICONTROL Advanced]** > **[!UICONTROL System]** > **[!UICONTROL Cron (Scheduled Tasks)]**&#x200B;に移動します。
1. 両方に&#x200B;**[!UICONTROL Use Separate Process]**&#x200B;を&#x200B;**[!UICONTROL No]**&#x200B;に設定：
   - グループのCron設定オプション：**[!UICONTROL index]**
   - グループのCron設定オプション：**[!UICONTROL staging]**
1. 保存後に設定キャッシュをフラッシュします。

>[!NOTE]
>
>両方のグループがプロセス内で順次実行されている場合、完全インデックスの再作成が遅いと、ステージングが完了するまで実行がブロックされます。 大規模なカタログでは、ステージング更新が遅れる場合があります。

## [!DNL Adobe Commerce]と接続サービス間のカタログデータの相違 {#catalog-data-discrepancy}

**問題：**&#x200B;接続されたCommerce サービス（[!DNL Live Search]や[!DNL Product Recommendations]など）に表示されている製品データが[!DNL Adobe Commerce]のカタログデータと一致しません。 例えば、ストアフロントで商品名、価格、説明が古かったり、間違っていたりします。

**原因：**&#x200B;再同期がトリガーされた後、データが更新され、UI コンポーネントに反映されるまでに最大1時間かかる場合があります。 そのウィンドウを超えて矛盾が続く場合は、フィード データが既に最新としてマークされているため、アイテムが最後の同期で取得されなかった可能性があります。または、同期で変更が検出されなかった可能性があります。

**解決策：**

1. Commerce ストアフロントから、検索結果を開きます。 次に、該当する製品を選択して、詳細ビューを開きます。
1. JSON出力をコピーし、[!DNL Commerce] カタログにあるものと一致することを確認します。
1. コンテンツが一致しない場合は、スペースやピリオドの追加など、カタログ内の製品を少し変更して、変更を強制的に検出します。
1. 再同期を待つか、管理者のCLIまたは[[!UICONTROL Data Feed Sync Status]](https://experienceleague.adobe.com/ja/docs/commerce-admin/systems/data-transfer/data-sync/data-feed-sync-status) ページから手動再同期をトリガーします。

[!DNL Product Recommendations]のカタログデータのトラブルシューティングについて詳しくは、[Commerce ナレッジベースの商品レコメンデーションモジュール &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/troubleshoot-product-recommendations-module-in-magento-commerce)のトラブルシューティングを参照してください。

## スケジュールでデータ同期が実行されていません {#sync-not-on-schedule}

**問題：** データの同期がスケジュールどおりに実行されないか、[!DNL Adobe Commerce]の製品の変更にもかかわらずアイテムが同期されていません。

**原因：**&#x200B;最も一般的な原因は、cron ジョブが実行されていないか、**[!UICONTROL Update by Schedule]** モードでインデクサーが設定されていないことです。

**解決策：**

- [cron ジョブが実行中であることを確認します](https://experienceleague.adobe.com/ja/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/cron-readiness-check-issues)。
- 次のフィードのインデックスが&#x200B;**[!UICONTROL Update by Schedule]**&#x200B;に設定されていることを確認します。カタログ属性、製品、製品の上書き、製品バリアント。 Commerce管理者の[[!UICONTROL Index Management]](https://experienceleague.adobe.com/ja/docs/commerce-admin/systems/tools/index-management)またはCLI: `bin/magento indexer:show-mode | grep -i feed`を使用して確認します。

## カタログ同期のステータスが「失敗」です {#catalog-sync-failed}

**問題：** カタログの同期で、**[!UICONTROL Data Feed Sync Status]** ページに&#x200B;**失敗** ステータスが表示されます。

**原因：** データの収集または送信フェーズ中に、回復不能なエラーが発生しました。 一般的な原因には、API認証の問題、ネットワークエラー、データ検証エラーなどがあります。

**解決策：**

1. エラーの詳細については、データ書き出しエラーログを参照してください。 ログ形式と拡張ログ オプションについては、[&#x200B; ログの確認とトラブルシューティング &#x200B;](logging.md)を参照してください。
   - データ収集中にエラーが発生した`var/log/commerce-data-export-errors.log`。
   - データ送信中にエラーが発生した`var/log/saas-export-errors.log`。
1. エラーが設定またはサードパーティの拡張機能に関連しない場合は、[関連するログエントリを含むサポートチケット &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#submit-ticket)を送信します。

## ログに「操作がスキップされました – プロセスがロックされました」というメッセージが表示される {#process-locked}

**問題：** `commerce-data-export.log` ファイルには、次のようなエントリが含まれています。

```json
{"feed":"products","operation":"partial sync","status":"operation skipped - process locked by \"full sync(1234)\"", ...}
```

**原因：**&#x200B;これは予期された動作であり、エラーではありません。 完全な再インデックスまたは`saas:resync`が既に進行中の間に、クロントリガーによる部分的な同期が実行しようとすると、メッセージが表示されます。 [!DNL SaaS Data Export]拡張機能では、フィード ロック メカニズムを使用して、同時同期操作の競合を防止しています。

**解決策：**

アクションは必要ありません。 実行中のプロセスが完了してロックを解除すると、次のcron実行が取得され、保留中の変更が同期されます。 ロックメカニズムの仕組みについて詳しくは、[SaaS データ書き出し用のフィードロックメカニズム &#x200B;](../feed-lock-mechanism.md)を参照してください。

>[!MORELIKETHIS]
>
> - [&#x200B; ログの確認とトラブルシューティング &#x200B;](logging.md)
> - [&#x200B; ログコード参照](log-codes-reference.md)
> - [SaaS データ書き出し用のフィードロックメカニズム &#x200B;](../feed-lock-mechanism.md)
