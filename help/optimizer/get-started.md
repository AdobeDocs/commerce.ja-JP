---
title: 基本を学ぶ
description: ' [!DNL Adobe Commerce Optimizer] の使用を開始する方法について説明します。'
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="SaaS のみ" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud ServiceおよびAdobe Commerce Optimizer プロジェクトにのみ適用されます（Adobeで管理される SaaS インフラストラクチャ）。"
exl-id: de57d93d-e156-45c1-86aa-de29a8c34bd2
source-git-commit: f920cfe7cd433e85f343fefe1062a1972e5e5e5f
workflow-type: tm+mt
source-wordcount: '852'
ht-degree: 0%

---

# はじめに

このガイドでは、[!DNL Adobe Commerce Optimizer] の設定を最初から最後まで説明します。 このガイドではすべての役割をカバーしていますが、開発者固有のコンテンツについて詳しくは、[ 開発者ドキュメント ](https://developer.adobe.com/commerce/services/optimizer/) を参照してください。

## 前提条件

開始する前に、次のことを確認します。

- **Adobe Experience Cloud アカウント** （[!DNL Adobe Commerce Optimizer] 使用権限）
- **組織管理者アクセス**：インスタンスを作成し、ユーザーを管理します。
- **GitHub アカウント** （サンプルデータの読み込みとストアフロント開発に使用）
- e コマースの概念に関する **基本的な理解**

## クイックスタートガイド

[!DNL Adobe Commerce Optimizer] 環境を実行するには、次の基本的な手順に従います。

### 手順 1. インスタンスの作成

1. [Adobe Experience Cloud](https://experience.adobe.com/) にログインします。
1. **Commerce** / **Commerce Cloud Manager** に移動します。
1. **インスタンスを追加**/**Commerce Optimizer** をクリックします。

   ![ インスタンスを作成 ](./assets/create-aco-instance.png){width="60%" zoomable="yes"}

1. インスタンス設定を指定：
   - **名前**：わかりやすい名前（「My Company Sandbox」など）
   - **説明**：目的の簡単な説明
   - **地域**：優先する地域を選択します
   - **環境タイプ**：テスト用の **サンドボックス** 環境から開始

1. **インスタンスを追加** をクリックします。

   Cloud Managerが更新され、新しいインスタンスが追加されます。 アクセスと管理について詳しくは、「[ インスタンスの管理 ](#manage-an-instance)」を参照してください。

>[!NOTE]
>
>サンドボックスインスタンスは、北米リージョンに制限されています。 作成後に領域を変更することはできません。

### 手順 2. 環境の設定

インスタンスの作成後：

1. Commerce Cloud Manager で [ インスタンスを管理 ](#manage-an-instance) します。
1. [User Management ガイド ](./user-management.md) を使用してユーザーアクセスを設定します。

### 手順 3. サンプルデータを追加（オプション）

テストと学習については、[ サンプルデータの読み込み ](#add-sample-data) の手順に従ってください。

## 役割ベースのワークフロー

設定と管理 [!DNL Adobe Commerce Optimizer]、次の 3 つの主要な役割に依存しています。 各役割には、次のような特定のタスクと責務があります。

![ ワークフローの概要 ](./assets/high-level-workflow.png){zoomable="yes"}

### 管理者のタスク

管理者は、インスタンス、ユーザーおよび組織設定を管理します。

| タスク | 説明 | リンク |
|---|---|---|
| **ユーザーの管理** | ユーザー、開発者、管理者を追加 | [ ユーザー管理 ](./user-management.md) |
| **インスタンスの作成** | サンドボックス環境と実稼動環境のセットアップ | [ インスタンスを作成 ](#create-an-instance) |
| **アクセスの設定** | カタログ表示とポリシーの設定 | [ カタログ ビュー ](./setup/catalog-view.md) |

### 開発者タスク

開発者は、プラットフォームのアーキテクチャタスクなど、技術的な実装とデータ統合を処理します。

| タスク | 説明 | リンク |
|---|---|---|
| **Developer Consoleへのアクセス** | プロジェクトの作成と資格情報の生成 | [Developer Console](https://developer.adobe.com/developer-console/docs/guides/getting-started) |
| **カタログデータの取り込み** | 既存システムからの製品データのインポート | [ データ取得 API](https://developer-stage.adobe.com/commerce/services/composable-catalog/data-ingestion/using-the-api/) |
| **ストアフロントの設定** | Edge Delivery Services ストアフロントの設定 | [ ストアフロントの設定 ](./storefront.md) |

### マーチャンダイザータスク

マーチャンダイザーは、製品の検出とレコメンデーションを通じて、ショッピングエクスペリエンスを最適化およびパーソナライズします。 また、買い物客のデータと分析を使用して、ストアフロントでの製品の配置、価格、プロモーションに関する戦略的な決定を行います。

| タスク | 説明 | リンク |
|---|---|---|
| **製品の検出** | 検索とフィルタリングの設定 | [ マーチャンダイジングの概要 ](./merchandising/overview.md) |
| **推奨事項** | AI を活用した製品レコメンデーションの設定 | [ 製品の推奨事項 ](./merchandising/recommendations/overview.md) |
| **パフォーマンストラッキング** | 成功指標の監視 | [ 成功指標 ](./manage-results/success-metrics.md) |

## インスタンスの管理

1. [Adobe Experience Cloud](https://experience.adobe.com/) にログインします。

1. Commerce Cloud Manager を開きます。
   - **クイックアクセス** で、**Commerce** をクリックします。
   - 使用可能なインスタンスを表示します。

1. インスタンスにアクセス：

   インスタンス名をクリックして、[!DNL Adobe Commerce Optimizer] アプリケーションを開きます。 アプリケーション内で、ページ上部のドロップダウンを使用して、様々な [!DNL Adobe Commerce Optimizer] インスタンスを切り替えることができます。

   ![ インスタンススイッチャー ](./assets/context-switcher.png){zoomable="yes"}

   表示されるインスタンスはすべて同じ組織に属しています。 インスタンスを切り替えて、サンドボックス環境と実稼動環境など、それぞれに対応するデータと設定を表示できます。

1. インスタンスの詳細を取得：
   - インスタンス名の横にある情報アイコンをクリックします。
   - GraphQL エンドポイント、データ取り込み用のカタログサービスエンドポイント、インスタンス ID （`tenant ID` とも呼ばれます）に注意してください。

   ![ インスタンスの詳細 ](./assets/aco-instance-details.png){width="60%" zoomable="yes"}

   フロントエンドアプリケーションやバックエンドシステムと統合するには、エンドポイントとインスタンス ID （テナント ID）の詳細が必要です。 [!DNL Adobe Commerce Optimizer] アプリケーションにアクセスするための URL もこちらから提供されます。

   すべてのAdobe Commerce Optimizer ユーザーがCloud Managerおよびインスタンスの詳細にアクセスできるわけではありません。 アクセス権は、ユーザーアカウントに割り当てられた役割と権限によって異なります。 アクセス権がない場合は、組織の管理者に問い合わせてインスタンスの詳細を取得してください。

1. インスタンス名と説明を編集します。
   - インスタンス名の横にある **編集** アイコンをクリックします。
   - 必要に応じて、名前と説明を更新します。
   - **保存** をクリックします。

   また、検索およびフィルターオプションを使用して、特定のインスタンスをすばやく見つけることもできます。

## サンプルデータを追加

Adobeは、[!DNL Adobe Commerce Optimizer] の機能を学習およびテストするのに役立つサンプルデータとツールを含む GitHub リポジトリを提供します。
サンプルデータは、[Carvelo ビジネスシナリオ ](./use-case/admin-use-case.md) に基づいており、次のものが含まれます。

- 自動車部品の製品カタログ
- 複数の価格台帳と価格設定シナリオ
- 異なるディーラー向けのカタログビューとポリシー
- 完全なエンドツーエンドワークフローの例

**サンプルデータを読み込みます。**

1. GitHub リポジトリにアクセスします。
   - [Sample Catalog Data Ingestion](https://github.com/adobe-commerce/aco-sample-catalog-data-ingestion) にアクセスします

1. リポジトリの README ファイルの設定手順に従います。

   - データ取り込みの設定と実行
   - サンプルデータを使用したカタログポリシーとビューの設定
   - サンプルデータのクリーンアップ（オプション）

## 次の手順

設定が完了したら、次の手順を実行します。

1. ストアフロントの設定：
   - [Edge Delivery Services ストアフロント ](./storefront.md) を設定
   - カタログデータへの接続

1. Carvelo のユースケースを見る：
   - [ エンドツーエンドのワークフロー ](./use-case/admin-use-case.md) に従う
   - 実際のシナリオを使用して練習する

1. マーチャンダイジングを設定：
   - 設定 [ 製品検出 ](./merchandising/overview.md)
   - 作成 [recommendations](./merchandising/recommendations/overview.md)

1. 監視パフォーマンス：
   - トラック [ 成功指標 ](./manage-results/success-metrics.md)
   - 分析 [ パフォーマンスの検索 ](./manage-results/search-performance.md)

## トラブルシューティング

### よくある問題

| 問題 | 解決策 |
|---|---|
| **インスタンスを作成できません** | 使用権限と管理者権限 [!DNL Adobe Commerce Optimizer] あることを確認します。 |
| **インスタンスが表示されません** | Adobe IMSー組織を確認し、ページを更新します。 |
| **インスタンスにアクセスできません** | Admin Consoleでユーザーとして追加されていることを確認します。 |
| **サンプルデータが読み込まれない** | インスタンスの資格情報と API エンドポイントを確認します。 |

### ヘルプを表示

- **開発者向けリソース**: [ 開発者向けドキュメント ](https://developer-stage.adobe.com/commerce/services/composable-catalog/)
- **ストアフロントのリソース**:[Commerce ストアフロントのドキュメント ](https://experienceleague.adobe.com/developer/commerce/storefront/)
- **サポート**: [Adobe Commerce サポートリソース ](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/overview)
