---
title: ' [!DNL Adobe Commerce Optimizer Connector]のシナリオのトラブルシューティング'
description: 同期結果の設定ミスまたは解釈ミスが原因で [!DNL Adobe Commerce Optimizer Connector] の予期しない動作を診断して解決します。
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
feature: Integration, Configuration
badgePaas: label="PaaSのみ" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce on Cloud プロジェクト（Adobeで管理されるPaaS インフラストラクチャ）とオンプレミス プロジェクトにのみ適用されます。"
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047id: b974b164-8a4e-43b8-a9e2-8e67ec131677id: cdf0c6dd-1717-4e20-9530-a24eee57088b
feature_v2: id: dac87252-6066-4d6e-a9d2-f6d84c323de7id: c32adafa-ed01-4b31-997e-2413013911b0id: e7dae43f-215c-4cdf-90d3-c5a461a6e669id: c18ed297-2187-4aec-affb-9d9654eca6fc
subfeature_v2: id: a40ebd6b-b542-4432-a730-1803ef74518d
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2: id: c1579802-ddd4-4214-8a91-97b2066abe11
source-git-commit: 182aa9ce819807d1ede85c4fa459714e7dfe0478
workflow-type: tm+mt
source-wordcount: 516
ht-degree: 0%

---


# [!DNL Adobe Commerce Optimizer Connector]のシナリオのトラブルシューティング

このページでは、一般的に設定ミスや同期結果の誤解釈が原因で[!DNL Adobe Commerce Optimizer Connector]を操作する際に発生する可能性のある動作について説明します。 以下の説明を使用して、根本原因を特定し、適切な解決策を適用します。

## フィードのステータスに「成功」が表示されますが、[!DNL Adobe Commerce Optimizer]にデータは表示されません

**問題：** **[!UICONTROL Data Feed Sync Status]** ページは同期に成功したことを報告していますが、商品、価格などが[!DNL Adobe Commerce Optimizer]に期待どおりに表示されません。

**原因：** フィードの状態が成功した場合は、データが取り込みエンドポイントによって受け入れられたことを意味します。つまり、[!DNL Adobe Commerce Optimizer]を通じたデータの伝達が完了したことを意味しません。 取り込み後、伝播に数分かかる場合があります。

**解決策：**

- 数分待って、[!DNL Adobe Commerce Optimizer] ビューを更新します。
- [!DNL Adobe Commerce]で設定されたテナント IDが、確認中の[!DNL Commerce Optimizer]環境と一致することを確認してください。
- [!DNL Commerce Optimizer]で正しい[ カタログ ソース ](../../optimizer/setup/catalog-sources.md) （ストア ビューのコード）または価格表が選択されていることを確認します。

## 書き出されたカタログに製品が見つかりません

**問題：**&#x200B;一部の製品は、完全なカタログ同期の後に[!DNL Adobe Commerce Optimizer]に表示されません。

**原因：**&#x200B;書き出し中に製品が検証に失敗した場合、同期から除外されます。 カタログで無効または表示されていない製品は、製品APIによって返されません。

**解決策：**

- 影響を受ける製品が、カタログソースとして使用されるweb サイトとストアビューに割り当てられていることを確認します。
- 製品が有効になっており、カタログリストを含む表示に設定されていることを確認します。
- **[!UICONTROL System]** > **[!UICONTROL Data Transfer]** > **[!UICONTROL Data Feed Sync Status]**&#x200B;のカタログフィードの項目別エラーの詳細を確認します。

## [!DNL Adobe Commerce Optimizer]の価格が正しくないか、見つかりません

**問題：**&#x200B;製品は[!DNL Adobe Commerce Optimizer]に表示されますが、[製品GraphQL クエリ ](https://developer.adobe.com/commerce/services/reference/graphql/#products){target="_blank"}で返された価格が表示されないか、価格が[!DNL Adobe Commerce]で設定されているものと一致しません。

**原因：**&#x200B;価格表フィードでは、特定のweb サイトと顧客グループにマッピングするスコープが使用されています。 間違った[ カタログ ビュー](../../optimizer/setup/catalog-view.md)設定は、価格が欠落または誤っている可能性があります。

**解決策：**

- コネクタの書き出し設定で、web サイトが同期用に設定されていることを確認します。 [ データ書き出し設定のカスタマイズ ](../get-started.md#customize-the-commerce-scopes-export-configuration)を参照してください。
- [!DNL Commerce Optimizer]で使用されている価格表IDが、製品クエリの実行に使用された[ カタログ ビュー](../../optimizer/setup/catalog-view.md){target="_blank"}設定に存在することを確認します。

## [!DNL Adobe Commerce Optimizer]のデータが上書きされるか、同期後に予期せず変更されます

**問題：**&#x200B;外部システム（PIMやERPなど）によって[!DNL Adobe Commerce Optimizer]に直接適用されたデータ変更は、コネクタが同期を実行した後に失われたり、元に戻されたりします。

**原因：** [!DNL Adobe Commerce]以外のシステムが[!DNL Adobe Commerce Optimizer]に直接書き込む（PIMや他の外部システムなど）場合、データの競合が発生する可能性があります。 コネクタは[!DNL Adobe Commerce]から[!DNL Adobe Commerce Optimizer]までのデータ *一方向*&#x200B;を同期し、変更を[!DNL Adobe Commerce]に同期しません。 その結果、[!DNL Adobe Commerce Optimizer]に直接書き込まれたデータは[!DNL Adobe Commerce]に反映されず、後で同期するときに上書きできます。


**解決策：**

カタログの変更を[!DNL Adobe Commerce Optimizer]に直接書き込む代わりに、[ カタログレイヤー](../../optimizer/setup/catalog-layer.md){target="_blank"}を使用して、[!DNL Adobe Commerce]以外の場所で変更を適用します。 カタログレイヤーを使用すると、外部システムはコネクタ同期と競合することなく、[!DNL Adobe Commerce Optimizer]内のカタログデータをエンリッチメントまたは上書きできます。

## [!DNL SaaS Data Export]の一般的な問題のトラブルシューティング

コネクタに影響を与える可能性のある基になる[!DNL SaaS Data Export]に関する問題については、[の [!DNL SaaS Data Export]](../../data-export/troubleshooting/troubleshooting-scenarios.md)のトラブルシューティングのシナリオを参照してください。
