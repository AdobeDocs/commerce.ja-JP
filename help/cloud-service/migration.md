---
title: 移行先  [!DNL Adobe Commerce as a Cloud Service]
description: ' [!DNL Adobe Commerce as a Cloud Service] への移行方法を説明します。'
exl-id: 9065c92a-f6b2-4464-8ec0-5c549bf78104
badgeSaas: label="SaaS のみ" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud ServiceおよびAdobe Commerce Optimizer プロジェクトにのみ適用されます（Adobeで管理される SaaS インフラストラクチャ）。"
role: Architect
source-git-commit: 395def94181016b12a00ce675bb15ef6c8f10309
workflow-type: tm+mt
source-wordcount: '1001'
ht-degree: 0%

---

# [!DNL Adobe Commerce as a Cloud Service] に移行

{{accs-early-access}}

[!DNL Adobe Commerce as a Cloud Service] は、ほとんどの設定を標準で提供しています。 ただし、既存のAdobe Commerce on Cloud またはオンプレミスインスタンスから移行する場合は、設定に応じて異なる移行操作を実行する必要があります。

## 移行パス

[!DNL Adobe Commerce as a Cloud Service] は、タイムライン、ストアフロント、カスタマイズに応じて、複数の移行パスをサポートしています。

完全移行の代わりに、[!DNL Adobe Commerce as a Cloud Service] ではCommerce Optimizerまたは増分アプローチを使用した段階的な移行をサポートしています。

* **増分移行** – このアプローチでは、データ、カスタマイズおよび統合を段階的に移行します。 このアプローチは、複雑なカスタマイズやデータを自分のペースで徐々に移行したいと考えている、カスタマイズが多い大規模なマーチャントに [!DNL Adobe Commerce as a Cloud Service] 適です。

![ 増分移行 ](./assets/incremental.png){width="600" zoomable="yes"}

* **Commerce Optimizer** – このアプローチを使用すると、Commerce Optimizerを移行段階として使用して、複雑なカスタマイズとデータを自分のペースで [!DNL Adobe Commerce as a Cloud Service] に移行することで、繰り返し移行できます。 Commerce Optimizerを使用すると、カタログチャネルとポリシーを活用したマーチャンダイジングサービス、Edge Deliveryを活用したCommerce Storefront、AEM Assetsを活用した製品ビジュアルにアクセスできます。

![ 反復移行 ](./assets/optimizer.png){width="600" zoomable="yes"}

* **完全移行**：このアプローチでは、すべてのデータ、カスタマイズ、統合を一度に移行します。 このアプローチは、[!DNL Adobe Commerce as a Cloud Service] に迅速に移行したいカスタマイズが少ない小規模なマーチャントに最適です。

次の表は、様々なストアフロントと設定での移行プロセスの概要を示しています。

|                    | LUMA ストアフロント | PWA ストアフロント | Edge DeliveryによるCommerce ストアフロント | ヘッドレス |
|--------------------|----------------------------------------|----------------------------------------|------------------------------------------------------|----------------------------------------|
| データ移行 | 必須 | 必須 | 必須 | 必須 |
| ストアフロント | Edge Deliveryを使用したCommerce ストアフロントへの移行 | Edge Deliveryまたは Maintain を使用したCommerce ストアフロントへの移行 | 影響なし | 影響なし |
| API メッシュ | 新しいメッシュを作成 | 新しいメッシュを構築または既存のメッシュを再構成 | 新しいメッシュを構築または既存のメッシュを再構成 | 新しいメッシュを構築または既存のメッシュを再構成 |
| 統合 | 統合スターターキットを活用 | 統合スターターキットを活用 | 統合スターターキットを活用 | 統合スターターキットを活用 |
| カスタマイズ | App Builderと API メッシュに移動 | App Builderと API メッシュに移動 | App Builderと API メッシュに移動 | App Builderと API メッシュに移動 |
| Assetsの管理 | OOTB を使用する場合は移行が必要 | OOTB を使用する場合は移行が必要 | OOTB を使用する場合は移行が必要 | OOTB を使用する場合は移行が必要 |
| 拡張機能 | App Builderへの移行 | App Builderへの移行 | App Builderへの移行 | App Builderへの移行 |

表に示されているように、各移行の緩和策は次の要素で構成されます。

* **データ移行** – 提供された移行ツールを使用して、既存のインスタンスから [!DNL Adobe Commerce as a Cloud Service] にデータを移行します。
* **ストアフロント** – 既存の EDS およびヘッドレスストアフロントは軽減を必要としませんが、LUMA ストアフロントはEdge Deliveryを活用したCommerce Storefront に移行する必要があります。 PWA Studio ストアフロントは、Edge Deliveryを活用して、または現在の状態で維持しながら、Commerce ストアフロントに移行できます。 Adobeは、ストアフロントへの移行を支援するためのアクセラレーターを提供します。
* **[API メッシュ ](https://developer.adobe.com/graphql-mesh-gateway)** – 新しいメッシュを作成するか、既存のメッシュを修正します。 Adobeは、このプロセスを支援するために事前設定済みのメッシュを提供します。
* **統合** – すべての統合は、[ 統合スターターキット ](https://developer.adobe.com/commerce/extensibility/starter-kit/integration/) または [[!DNL Adobe Commerce as a Cloud Service] REST API](https://developer.adobe.com/commerce/services/reference/cloud-service/core-admin/) のいずれかを活用する必要があります。
* **カスタマイズ** – すべてのカスタマイズは、App Builderと API メッシュに移動する必要があります。
* **Assets Management** – すべての Assets Management には移行が必要です。 既にAEM Assetsを使用している場合は、移行する必要はありません。
* **拡張機能** – 処理中の拡張機能は、プロセス外の拡張機能として再作成する必要があります。 2025 年末までに、Adobeは、ビルド時間を最小限に抑えるために、最も一般的な拡張機能へのアクセスを提供します。

## 移行フェーズ

現在のAdobe Commerce インスタンスから新しい [!DNL Adobe Commerce as a Cloud Service] インスタンスへの移行には、主に次の段階が必要です。

* **[準備](#readiness-phase)** – 最初に、ACCS に移行する準備ができているかどうかを判断します。 この段階では、ACCS によって導入された変更点についても理解しておく必要があります&#x200B;
* **[実装](#implementation-phase)** – 次に、コード、ストアフロント、拡張機能、移行のための統合の準備を行います。 移行を容易にするために、Adobeでは [ 短期と長期の両方の繰り返しアプローチ ](#migration-paths) が可能です&#x200B;。
* **[運用開始](#go-live-phase)** – すべてが整っていることをテストして確認してから、データ移行を実行します。
* **[運用開始後](#post-go-live-phase)** - Adobeと連携して問題を監視し、移行完了後に必要に応じてパフォーマンスを向上させます。

### 準備フェーズ

1. まず、[!DNL Adobe Commerce as a Cloud Service] のアーキテクチャ、拡張フレームワークおよびストアフロント機能を確認します。

   * [Adobe Commerce on Cloud Services のアーキテクチャ ](./overview.md) - プラットフォームのアーキテクチャと、現在のAdobe Commerce インスタンスとの違いを確認します。
   * [Adobe Commerce拡張フレームワーク ](https://developer.adobe.com/commerce/extensibility/) – 現在のカスタマイズの移行方法を特定します。
   * [Edge DeliveryによるCommerce Storefront](https://experienceleague.adobe.com/developer/commerce/storefront/) – 推奨されるストアフロントソリューションを確認します。

1. カスタマイズの互換性を監査します。

   * 現在のカスタムモジュールとサードパーティの統合を特定します。
   * App Builderを使用して、再実装が必要なカスタマイズを評価します。
   * 現在のカスタマイズを、同等のApp Builder拡張機能にマッピングします。

1. ストアフロントの要件を確認し、Adobe Edge 配信機能と一致していることを確認します。

1. 現在のサードパーティ統合を確認し、[!DNL Adobe Commerce as a Cloud Service] プラットフォームとの API の互換性を確認します。

### 実装フェーズ

移行の開発および実行プロセスの概要を次に示します。

1. 新しい [!DNL Adobe Commerce as a Cloud Service] インスタンスを [Commerce Cloud Manager](./getting-started.md#create-an-instance) に作成します。

1. 必要なアプリとカスタマイズをインストールします。 [!DNL Adobe Commerce as a Cloud Service] は、最も人気のあるアプリにアクセスできます。 追加のアプリやカスタマイズが必要な場合は、App Builderを使用して再実装できます。

1. 次のGraphQL ベースのストアフロントのいずれかを設定します。

   * [Commerce ストアフロントの作成 ](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/)
   * [PWA Studioを使用して、GraphQLベースのカスタムのストアフロントを作成する ](https://developer.adobe.com/commerce/pwa-studio/)

1. 以前のCommerce インスタンスから ACCS にデータを移行します。

   * データ移行ツールを使用してネイティブのAdobe Commerce データを移行します。
   * サードパーティの拡張機能とカスタマイズの移行
   * 設定および統合データを移行します。
      * [Adobe Commerce統合スターターキット ](https://developer.adobe.com/commerce/extensibility/starter-kit/integration/) を使用して、API メッシュ設定、サードパーティのサービス、システム統合を転送します。

### 運用開始段階

起動する前に、サンドボックス環境を使用して新しい [!DNL Adobe Commerce as a Cloud Service] インスタンスを検証およびテストします。

* **機能テスト**：移行されたデータ、ストアフロント機能、カスタマイズがシームレスに機能することを確認します。

* **パフォーマンステスト** - ストアの速度と拡張性を評価して、グローバルに最適なパフォーマンスを確保します。

* **セキュリティ監査** - API アクセス制御や潜在的な脆弱性など、セキュリティ対策を確認します。

新しい [!DNL Adobe Commerce as a Cloud Service] サンドボックスインスタンスを検証およびテストしたら、実稼動インスタンスを起動できます。

### 運用開始後フェーズ

運用開始後、ローンチ後の以下のアクティビティを実行します。

1. 運用開始フォローアップ

   * 新しいプラットフォームにトラフィックをリダイレクトし、パフォーマンスを監視します。
   * 古いAdobe Commerce インスタンスを無効にします。

1. 起動後の監視

   * 監視ツールを使用して、安定した運用を確保し、起動後の問題に対処します。
