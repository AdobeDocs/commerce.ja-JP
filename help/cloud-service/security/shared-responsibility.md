---
title: 共通の責任
description: ' [!DNL Adobe Commerce as a Cloud Service]  プロジェクトに関わる各パーティのセキュリティに関する責任について説明します。'
feature: Cloud, Security
role: Admin, Developer, Leader
level: Intermediate
exl-id: 424fe5cd-5d54-425d-97ce-024476d18dde
badgeSaas: label="SaaSのみ" type="Positive" url="https://experienceleague.adobe.com/ja/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud ServiceおよびAdobe Commerce Optimizer プロジェクト（Adobeが管理するSaaS インフラストラクチャ）にのみ適用されます。"
source-git-commit: 4c8f897e35f889b43004e5bb99e830f23aad4357
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 0%

---

# 責任セキュリティと運用モデルの共有

[!DNL Adobe Commerce as a Cloud Service]は、共有責任セキュリティと運用モデルに依存するオンデマンドサービスです。 Adobeとお客様は、これらの責任を負い、Adobe Commerce アプリケーションのセキュリティと運用について、各当事者が明確な責任を負います。

>[!BEGINSHADEBOX]

次のサマリーテーブルでは、RACI モデルを使用して、Adobeとお客様の間で共有されているセキュリティ責任を示しています。

**R** – 責任
**A** – 説明責任
**C** — コンサルテーション済み
**I** – 通知

>[!ENDSHADEBOX]

| タスク | Adobe | お客様 |
| --- | --- | --- |
| バックエンドのオリジンWAF ルールの定義 | RA | |
| バックエンド CDN WAF ルールの定義 | RA | |
| [!DNL Adobe Developer App Builder] アプリケーションのデプロイと保守 | | RA |
| バックエンドプラットフォームのWAF ルールのデプロイ | RA | |
| バックエンド CDN WAF ルールのデプロイ | RA | |
| [!DNL Adobe Commerce as a Cloud Service]のコア バグを修正しています | RA | I |
| [!DNL Adobe Commerce as a Cloud Service]個のインフラストラクチャのパッチをリリースしています | RA | |
| 拡張（インフラ） | RA | |
| 拡大（コアアプリケーション） | RA | |
| 外部アプリケーションの統合 | | RA |
| App Builder アプリのインストール | | RA |
| すべてのApp Builder アプリケーションのパフォーマンスをテストする | | RA |
| App Builderカスタムアプリのテーマとデザイン | | RA |
| バックエンド DNSの設定 | RA | I |
| バックエンド CDNのオンボーディング | RA | I |
| バックエンド CDNのサポート | RA | I |
| バックエンド DNS プロバイダーの取得 | RA | |
| 本番環境とサンドボックス環境のプロビジョニング | A | R |
| Adobe Commerce オンクラウド インフラストラクチャのDynamicsへのアクセス | R | C |
| バックエンドの顧客セキュリティ問題の解決 | RA | I |
| バックエンド CDNのセキュリティ問題の解決 | RA | |
| セキュリティ調査（スキャン/監査）によるAdobeのサポート | RA | |
| PCI ASV スキャンの実行 | RA | I |
| Adobe Commerce インフラストラクチャのPCI スキャンの修正 | R | |
| OSとプラットフォームのシークレットの管理 | RA | |
| バックエンドのセキュリティログの監視 | RA | |
| カスタマーサポートとアクセスの制御 | A | R |
| Adobe DRの計画とバックアップおよび復元に関する年間テストとドキュメント | RA | |
| 災害復旧計画の年間テストと文書化 | RA | |
| デバッグと問題の分離 | R | R |
| デバッグと問題分離プロセスのタイムリーなサポート | R | R |
| アップデートとパッチのAdobe Commerce コアへの公開 | RA | I |
| Adobe Commerce コアへのアップデートとパッチのインストール | RA | I |
| Core Adobe Commerceのアプリケーション品質 | RA | |
