---
title: 共有された責任
description: プロジェクトに関与する各パーティのセキュリティ責任について説明  [!DNL Adobe Commerce as a Cloud Service]  ます。
role: Admin, Architect, Leader
exl-id: 424fe5cd-5d54-425d-97ce-024476d18dde
badgeSaas: label="SaaS のみ" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud ServiceおよびAdobe Commerce Optimizer プロジェクトにのみ適用されます（Adobeで管理される SaaS インフラストラクチャ）。"
source-git-commit: a06d64566fda76c0527aabfa9e8fdf27e7c149ca
workflow-type: tm+mt
source-wordcount: '343'
ht-degree: 0%

---

# 共有責任セキュリティと運用モデル

[!DNL Adobe Commerce as a Cloud Service] は、責任の共有セキュリティと運用モデルに依存するオンデマンドサービスです。 これらの責務は、Adobeとお客様の間で共有されます。 各パーティは、Adobe Commerce アプリケーションを保護および運用する明確な責任を負います。

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
| サポートサービス（Nginx や MySQL など）へのパッチの適用 | RA | |
| バックエンドのオリジンWAFルールの定義 | RA | |
| バックエンド CDN WAF ルールの定義 | RA | |
| バックエンドプラットフォームのWAF ルールのデプロイ | RA | |
| バックエンド CDN WAF ルールのデプロイ | RA | |
| [!DNL Adobe Commerce as a Cloud Service] のコアバグの修正 | RA | I |
| インフラストラクチャ [!DNL Adobe Commerce as a Cloud Service] パッチのリリース | RA | |
| スケーリング（インフラストラクチャ） | RA | |
| スケーリング（コアアプリケーション） | RA | |
| 外部アプリケーションの統合 | | RA |
| App Builder アプリのインストール | | RA |
| すべてのApp Builder アプリのパフォーマンスのテスト | | RA |
| カスタム App Builder アプリのテーマ設定とデザイン | | RA |
| バックエンド DNS の設定 | RA | I |
| オンボーディングバックエンド CDN | RA | I |
| バックエンド CDN のサポート | RA | I |
| バックエンド DNS プロバイダーを取得しています | RA | |
| 実稼動環境とサンドボックス環境のプロビジョニング | A | R |
| クラウドインフラストラクチャー上のAdobe Commerce用 Dynamics へのアクセス | R | C |
| バックエンドの顧客セキュリティ問題の解決 | RA | I |
| バックエンド CDN セキュリティの問題の解決 | RA | |
| Adobeのセキュリティリサーチの支援（スキャン/監査） | RA | |
| PCI ASV スキャンの実行 | RA | I |
| Adobe Commerce インフラストラクチャの PCI スキャンの修正 | R | |
| OS およびプラットフォームの秘密鍵の管理 | RA | |
| バックエンドのセキュリティログの監視 | RA | |
| カスタマーサポートおよびアクセスの制御 | A | R |
| Adobe DR 計画およびバックアップ/リストアの年間テストと文書化 | RA | |
| ディザスタリカバリ計画の年 1 回のテストと文書化 | RA | |
| デバッグとイシューの分離 | R | R |
| デバッグと問題の分離プロセスをタイムリーにサポート | R | R |
| Adobe Commerce Core へのアップデートとパッチの公開 | RA | I |
| Adobe Commerce Core へのアップデートとパッチのインストール | RA | I |
| コア Adobe Commerce アプリケーションの品質 | RA | |
