---
title: 共通の責任
description: ' [!DNL Adobe Commerce Optimizer]  プロジェクトに関わる各パーティのセキュリティに関する責任について説明します。'
role: Admin, Developer, Leader
badgeSaas: label="SaaSのみ" type="Positive" url="https://experienceleague.adobe.com/ja/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud Serviceおよび [!DNL Adobe Commerce Optimizer]  プロジェクトにのみ適用されます（Adobeで管理されるSaaS インフラストラクチャ）。"
exl-id: 9e09790f-832d-43ab-b2df-6389ad52b43d
source-git-commit: ba445bf33ec9334c853245fce125af12cd244367
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 0%

---

# 責任セキュリティと運用モデルの共有

>[!BEGINSHADEBOX]

次のサマリーテーブルでは、RACI モデルを使用して、Adobeとお客様の間で共有されているセキュリティ責任を示しています。

**R** – 責任
**A** – 説明責任
**C** — コンサルテーション済み
**I** – 通知

>[!ENDSHADEBOX]

| タスク | Adobe | お客様 |
| --- | --- | --- |
| Adobe Commerce インフラストラクチャパッチの適用 | RA | |
| サポートサービスへのパッチの適用 | RA | |
| バックエンドのオリジンWAF ルールの定義 | RA | |
| バックエンド CDN WAF ルールの定義 | RA | |
| バックエンドプラットフォームのWAF ルールのデプロイ | RA | |
| バックエンド CDN WAF ルールのデプロイ | RA | |
| [!DNL Adobe Commerce Optimizer]のバグを修正しています | RA | I |
| [!DNL Adobe Commerce Optimizer] インフラストラクチャのパッチをリリースしています | RA | |
| 拡張（インフラ） | RA | I |
| 外部アプリケーションの統合 | | RA |
| App Builder アプリのインストール | | RA |
| すべてのApp Builder アプリケーションのパフォーマンスをテストする | | RA |
| App Builderカスタムアプリのテーマとデザイン | | RA |
| バックエンド DNSの設定 | RA |  |
| バックエンド CDNのオンボーディング | RA |  |
| バックエンド CDNのサポート | RA |  |
| バックエンド DNS プロバイダーの取得 | RA | |
| 本番環境とサンドボックス環境のプロビジョニング | A | R |
| [!DNL Adobe Commerce Optimizer]のDynamicsにアクセスしています | R | C |
| バックエンドの顧客セキュリティ問題の解決 | RA | I |
| バックエンド CDNのセキュリティ問題の解決 | RA | |
| セキュリティ調査（スキャン/監査）によるAdobeのサポート | RA | |
| PCI ASV スキャンの実行 | RA | I |
| [!DNL Adobe Commerce Optimizer] インフラストラクチャのPCI スキャンを修復しています | R | |
| OSとプラットフォームのシークレットの管理 | RA | |
| バックエンドのセキュリティログの監視 | RA | |
| カスタマーサポートとアクセスの制御 | A | R |
| Adobe DRの計画とバックアップおよび復元に関する年間テストとドキュメント | RA | |
| 災害復旧計画の年間テストと文書化 | RA | |
| デバッグと問題の分離 | R | R |
| デバッグと問題分離プロセスのタイムリーなサポート | R | R |
| [!DNL Adobe Commerce Optimizer]の更新とパッチをインストールしています | RA | I |
| コア [!DNL Adobe Commerce Optimizer] アプリケーション品質 | RA | |
