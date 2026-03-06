---
title: 共有責任
description: プロジェクトに関与する各パーティのセキュリティ責任について説明  [!DNL Adobe Commerce Optimizer]  ます。
role: Admin, Architect, Leader
badgeSaas: label="SaaS のみ" type="Positive" url="https://experienceleague.adobe.com/ja/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud Serviceおよびプロジェクトのみ（Adobe [!DNL Adobe Commerce Optimizer]  管理される SaaS インフラストラクチャ）に適用されます。"
exl-id: 9e09790f-832d-43ab-b2df-6389ad52b43d
source-git-commit: c7c21df464685783b5fae1c99d60ca91e0c334d2
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 0%

---

# 共有責任セキュリティと運用モデル

>[!BEGINSHADEBOX]

次の概要テーブルでは、RACI モデルを使用して、Adobeとお客様の間で共有されるセキュリティの責任を示しています。

**R** – 担当
**A** — Accountable
**C** – 問い合わせ
**I** – 情報

>[!ENDSHADEBOX]

| タスク | Adobe | 顧客 |
| --- | --- | --- |
| Adobe Commerce インフラストラクチャパッチの適用 | RA | |
| サポートサービスへのパッチの適用 | RA | |
| バックエンドのオリジンWAFルールの定義 | RA | |
| バックエンド CDN WAF ルールの定義 | RA | |
| バックエンドプラットフォームのWAF ルールのデプロイ | RA | |
| バックエンド CDN WAF ルールのデプロイ | RA | |
| [!DNL Adobe Commerce Optimizer] でのバグの修正 | RA | I |
| [!DNL Adobe Commerce Optimizer] インフラストラクチャパッチのリリース | RA | |
| スケーリング（インフラストラクチャ） | RA | I |
| 外部アプリケーションの統合 | | RA |
| App Builder アプリのインストール | | RA |
| すべてのApp Builder アプリのパフォーマンスのテスト | | RA |
| カスタム App Builder アプリのテーマ設定とデザイン | | RA |
| バックエンド DNS の設定 | RA |  |
| オンボーディングバックエンド CDN | RA |  |
| バックエンド CDN のサポート | RA |  |
| バックエンド DNS プロバイダーを取得しています | RA | |
| 実稼動環境とサンドボックス環境のプロビジョニング | A | R |
| [!DNL Adobe Commerce Optimizer] 用 Dynamics へのアクセス | R | C |
| バックエンドの顧客セキュリティ問題の解決 | RA | I |
| バックエンド CDN セキュリティの問題の解決 | RA | |
| Adobeのセキュリティリサーチの支援（スキャン/監査） | RA | |
| PCI ASV スキャンの実行 | RA | I |
| インフラストラクチャ [!DNL Adobe Commerce Optimizer]PCI スキャンの修正 | R | |
| OS およびプラットフォームの秘密鍵の管理 | RA | |
| バックエンドのセキュリティログの監視 | RA | |
| カスタマーサポートおよびアクセスの制御 | A | R |
| Adobe DR 計画およびバックアップ/リストアの年間テストと文書化 | RA | |
| ディザスタリカバリ計画の年 1 回のテストと文書化 | RA | |
| デバッグとイシューの分離 | R | R |
| デバッグと問題の分離プロセスをタイムリーにサポート | R | R |
| [!DNL Adobe Commerce Optimizer] へのアップデートとパッチのインストール | RA | I |
| コア [!DNL Adobe Commerce Optimizer] アプリケーション品質 | RA | |
