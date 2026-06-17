---
title: '[!DNL Adobe Commerce Optimizer Connector] リリースノート'
description: カタログの同期と書き出しに関する新機能、バグ修正、既知の問題など、 [!DNL Adobe Commerce Optimizer Connector]  リリースノートについて説明します。
autotag-review: '2026-06-17T15:08:59.000Z'
feature: Release Notes
TQID: 'https://experienceleague.adobe.com/6NeLAfThvIWIyV4Y6OWtL8V9mC7lPy7UH-Zli8E-WEk'
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047id: b974b164-8a4e-43b8-a9e2-8e67ec131677id: cdf0c6dd-1717-4e20-9530-a24eee57088b
feature_v2: id: f08fa0de-a550-4acd-b570-f81cf1d03aafid: e7dae43f-215c-4cdf-90d3-c5a461a6e669
subfeature_v2: id: dad884f1-e840-49a1-970e-2f965bdbc410id: a40ebd6b-b542-4432-a730-1803ef74518d
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8id: f8a45b24-4be7-4f1b-909b-60d06b483a20
level_v2: id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: aa2f3246-cb95-4b30-8899-fdf7d73550ccid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 182aa9ce819807d1ede85c4fa459714e7dfe0478
workflow-type: tm+mt
source-wordcount: 353
ht-degree: 0%

---

# Adobe Commerce Optimizer Connector リリースノート

これらのリリースノートには、[!DNL Adobe Commerce Optimizer Connector]のすべてのリリースが記載されており、次の内容が含まれています。

![新機能](../assets/new.svg)
![修正された問題](../assets/fix.svg)修正と改善
![既知の問題](../assets/bug.svg)既知の問題

## 2026 リリース

### 1.0.14 リリース

_2026年6月11日_

![修正](../assets/fix.svg) **PHP 8.5との互換性** - [!DNL Adobe Commerce Optimizer Connector]はPHP 8.5をサポートするようになりました。これにより、コネクタ機能やカタログ同期を中断することなく[!DNL Adobe Commerce]環境をアップグレードできます。<!--MDEE-1388-->

![修正](../assets/fix.svg) **価格表は通貨変更後に更新されます** – 更新された価格は、通貨変更後にAdobe Commerce Optimizerに自動的に反映されます。<!--MDEE-1384-->

![修正](../assets/fix.svg) **ナビゲーションが無効または非表示の親カテゴリを尊重** – 無効または非表示のカテゴリ階層の製品がナビゲーションエクスペリエンスに予期せず表示されなくなりました。<!--MDEE-1385-->

![修正](../assets/fix.svg) **ステージング更新後の一貫したカテゴリ URL** - ステージング更新が適用された後も、カテゴリリンクとナビゲーションは正確なままです。<!--MDEE-1395-->

### 1.0.13 リリース

_2026年5月6日_

![修正](../assets/fix.svg) **構成手順[!DNL Adobe Commerce Optimizer Connector]を改善** - Commerce管理者の[!DNL Adobe Commerce Optimizer]設定ページを&#x200B;_[!DNL Adobe Commerce Optimizer Connector]統合ガイド_にリンクするように更新しました。
<!--COMOPT-1922-->

![修正](../assets/fix.svg) **[!DNL Adobe Commerce Optimizer Connector]メタデータの機能強化** - [!DNL Adobe Commerce Optimizer Connector]には、インストール済みのバージョンがメタデータヘッダーに含まれるようになりました。 この改善により、トラブルシューティングまたはサポートの取り組み中に使用されているコネクタバージョンをすばやく特定できるようになります。<!--MDEE-1323-->

### 1.0.12 リリース

_2026年4月2日_

![新規](../assets/new.svg) **`saas:resync` コマンドでカテゴリフィードのサポートを追加**- `saas:resync` CLI コマンドを使用して、最新のカテゴリデータを簡単に更新および表示できるようになりました。

```shell
bin/magento saas:resync --feed=categories
```

### 1.0.11 リリース

_2026年3月10日_

![修正された問題](../assets/fix.svg) [!DNL Adobe Commerce Optimizer Connector]が[!DNL Adobe Commerce] インスタンスにインストールされたときに、Commerce管理者&#x200B;**[!UICONTROL System]**&#x200B;および&#x200B;**[!UICONTROL Configuration]** メニューから[!DNL Commerce Services Connector]設定ページへのアクセスをブロックする互換性の問題を修正しました。  これで、両方の拡張機能がインストールされている場合は、[!DNL Commerce Services Connector]設定ページにアクセスできます。<!--MDEE-1322-->


### 1.0.10 リリース

_2026年3月9日_

![修正](../assets/fix.svg) コネクタ設定を完了する前に&#x200B;**[!UICONTROL Data Feed Sync Status]** ページにアクセスすると、自動的にコネクタ設定ページにリダイレクトされるようになりました。 このガイド付きフローは、コネクタの設定が完了したことを確認し、失敗または不完全なステータス項目につながる可能性のある構成設定が欠落したことによるエラーを防ぐのに役立ちます。<!--MDEE-1296-->

### v1.0.9 リリース

_2026年3月1日_

[!DNL Adobe Commerce Optimizer Connector]の一般公開リリース。

>[!NOTE]
>
>[!DNL Adobe Commerce Optimizer Connector]のBeta プログラムに参加し、以前のバージョンの拡張機能がインストールされている場合は、一般提供バージョンにアップグレードして最新のアップデートを入手してください。
