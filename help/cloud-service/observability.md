---
title: ' [!DNL Adobe Commerce as a Cloud Service]の観測可能性'
description: 指標、ログ、トレースなど、 [!DNL Adobe Commerce as a Cloud Service]で使用できる識別可能性ツールとテレメトリ機能について説明します。
feature: Cloud, Integration
role: Admin, Developer
level: Intermediate
badgeSaas: label="SaaSのみ" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud ServiceおよびAdobe Commerce Optimizer プロジェクト（Adobeが管理するSaaS インフラストラクチャ）にのみ適用されます。"
source-git-commit: 3c10ecdea3d06295013c9c6e2d6869afd750a0b9
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 0%

---

# 可観測性

オブザーバビリティは、[!DNL Adobe Commerce as a Cloud Service]の操作の重要な側面です。 これには、指標、ロギング、トレースなど、テレメトリデータの収集、処理、可視化が含まれます。これにより、アプリケーションの健全性を監視し、パフォーマンスの問題を診断し、コマースプラットフォームとその統合の信頼性を最適化できます。

## [!DNL Adobe Commerce as a Cloud Service]

### Observability overview

オブザーバビリティにより、Adobe Commerceストアフロントと、接続されているあらゆるApp Builderアプリケーションの健全性とパフォーマンスを可視化できます。 コマースエコシステム全体でテレメトリデータを収集することで、次のことが可能になります。

* **APIの応答時間、リクエスト率とエラー率、リソース使用率などの指標**&#x200B;を追跡して、リアルタイムのパフォーマンスを監視し、傾向を特定します。
* アプリケーション、インフラストラクチャ、CDN、および統合のログを&#x200B;**一元化して単一のビューに表示し、トラブルシューティングを迅速化します。**
* **リクエストを追跡** エンドツーエンドで、フロントエンドからCommerceと接続されたアプリを経由してリクエストを処理します。これにより、顧客に影響を与える前に、ボトルネックや障害を特定できます。

これらの機能を組み合わせることで、問題を迅速に特定して解決し、パフォーマンスを最適化し、顧客に信頼できるエクスペリエンスを提供することができます。 [ オブザーバビリティの概要](https://developer.adobe.com/commerce/extensibility/observability/)では、[!DNL Adobe Commerce as a Cloud Service]がOpenTelemetryを使用して、イベント、Webhook、App Builder アプリケーションをまたいでこのテレメトリコレクションを統合する方法について説明しています。

![可観測性アーキテクチャ ](./assets/observability.png){width="600" zoomable="yes"}

Adobe Commerceは、OpenTelemetryを通じて次のオブザーバビリティ ツールをサポートしています。

* Elasticsearch
* Grafana
* イェーガー
* New Relic
* プロメテウス
* Splunk
* ジプキン

### 購読の設定

[ オブザーバビリティのサブスクリプション ](https://developer.adobe.com/commerce/extensibility/observability/configuration/)を[!UICONTROL Admin]またはREST APIを介して設定し、ログ、指標、またはトレースをOpenTelemetryと互換性のある任意のエンドポイントにルーティングします。 各サブスクリプションは、特定のコンポーネント（webhook、イベント、または[!UICONTROL Admin UI SDK]）をターゲットにしています。

### Observability REST API

[ オブザーバビリティ REST API](https://developer.adobe.com/commerce/extensibility/observability/api/)は、オブザーバビリティ サブスクリプションをプログラムで作成、取得、更新、削除するエンドポイントを提供します。 これらのエンドポイントを使用して、インスタンス間の設定を自動化します。

## Adobe Developer App Builder

### App Builder計装

[ オブザーバビリティを [!DNL App Builder]](https://developer.adobe.com/commerce/extensibility/observability/app-builder/)に実装して、Commerceのトレース コンテキストを[!DNL App Builder]のアクションに反映させ、両方のシステムのログとトレースがオブザーバビリティ プラットフォームで相関するようにします。 Webhook ベースとイベントベースの統合のインストルメンテーションについて説明します。

[!DNL App Builder]には、CLIやDeveloper Consoleへのアクセス、Splunk、Azure、New Relicなどの外部ソリューションへのログ転送など、[ アプリケーションログの管理](https://developer.adobe.com/app-builder/docs/guides/app_builder_guides/application_logging/logging)用のビルトインツールも用意されています。

### 遠隔測定ライブラリ

[`@adobe/aio-lib-telemetry`](https://github.com/adobe/aio-lib-telemetry/blob/main/docs/usage.md) ライブラリは、App Builder アクションがOpenTelemetry互換のログとトレースを生成するために使用するものです。 インストール、設定、エクスポーターの設定について説明します。

### ローカル開発とテスト

[ デプロイする前に、観測可能性の設定をローカルで](https://developer.adobe.com/commerce/extensibility/observability/local-development/) テストします。 ビジュアライゼーションとトンネル転送に[!DNL Grafana]を使用すると（例：[!DNL Ngrok]）、開発用マシン上のリモート Commerce インスタンスからテレメトリを受け取ることができます。

## [!DNL API Mesh]

### API メッシュログ

[API メッシュ ログ ](https://developer.adobe.com/graphql-mesh-gateway/mesh/advanced/logging/)を使用すると、レイ IDを使用してメッシュを流れるリクエストを監視およびデバッグできます。 ログを一括で書き出すか、[!DNL New Relic]などのプラットフォームに転送して一元分析します。

## ストアフロント

### CDNとリアルユーザーモニタリング

CDN オリジンを介した[ プロキシのリアルユーザーモニタリング（RUM） ](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/content-delivery-network/#proxy-rum-through-the-origin-to-avoid-a-tls-handshake) データ収集により、追加のTLS ハンドシェイクを排除し、フロントエンドのパフォーマンス測定を改善します。

## 観察性ビデオ

次のビデオでは、[!DNL Adobe Commerce as a Cloud Service]のオブザーバビリティ機能の概要を説明しています。

* [App Builderの観測性ビデオ](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/observability/overview){target="_blank"}
* [API Mesh ビデオ](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/extensibility/api-mesh/getting-started-api-mesh){target="_blank"}
