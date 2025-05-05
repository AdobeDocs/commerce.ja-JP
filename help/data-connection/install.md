---
title: インストール  [!DNL Data Connection]
description: Adobe Commerceから拡張機能をインストール、更新、アンインストールす  [!DNL Data Connection]  方法について説明します。
role: Admin, Developer
feature: Install
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '448'
ht-degree: 0%

---

# [!DNL Data Connection] のインストール

拡張機能をインストールする前に、[ 前提条件を確認 ](overview.md#prereqs) してください。

## 拡張機能のインストール

[!DNL Data Connection] 拡張機能は、[Adobe Marketplace](https://commercemarketplace.adobe.com/magento-experience-platform-connector.html) から利用できます。 サーバーのコマンドラインからこの拡張機能をインストールすると、Adobe Commerceのインストールに [ サービス ](../landing/saas.md) として接続します。 プロセスが完了すると、**[!DNL Data Connection]** と **Commerce サービスコネクタ** がCommerceの **管理** の **サービス** の下の _システム_ メニューに表示されます。

拡張機 ![[!DNL Data Connection] の管理者表示 ](assets/epc-adminui.png)

>[!IMPORTANT]
>
>拡張機能の名前はExperience Platform コネクタから [!DNL Data Connection] に変更されましたが、後方互換性をサポートするために、パッケージ名は `experience-platform-connector` のままです。

1. `experience-platform-connector` パッケージをダウンロードするには、コマンドラインから次のコマンドを実行します。

   ```bash
   composer require magento/experience-platform-connector
   ```

   このメタパッケージには、次のモジュールと拡張機能が含まれています。

   - `magento/orders-connector`
   - `magento/data-services`
   - `magento/customers-connector`
   - `magento/module-experience-connector`
   - `magento/module-experience-connector-admin`
   - `magento/module-experience-connector-admin-graph-ql`
   - `magento/module-experience-connector-aep-integration`

1. （任意） [ 検索イベント ](events.md#search-events) を含む [!DNL Live Search] データを含めるには、[[!DNL Live Search]](../live-search/install.md) 拡張機能をインストールします。

1. （任意） [ 要求イベント ](events.md#b2b-events) を含む B2B データを含めるには、[B2B 拡張機能 ](#install-the-b2b-extension) をインストールします。

1. （オプション）ヘルスケアのマーチャントの場合は、[!DNL Commerce] バックオフィスデータが HIPAA に対応するように [ データサービス HIPAA](#install-the-data-services-hipaa-extension) 拡張機能をインストールします。

### Adobe I/O Eventsのインストールと customers-connector モジュールの設定

`experience-platform-connector` 拡張機能をインストールした後、Adobe I/O Events for Adobe Commerceをインストールし、`customers-connector` モジュールを設定する必要があります。

次の手順は、クラウドインフラストラクチャー上のAdobe Commerceとオンプレミスの両方のインストールに適用されます。

1. Commerce 2.4.4 または 2.4.5 を実行している場合は、次のコマンドを使用してイベントモジュールを読み込みます。

   ```bash
   composer require magento/commerce-eventing=^1.0 --no-update
   ```

   Commerce 2.4.6 以降では、これらのモジュールが自動的に読み込まれます。

1. プロジェクトの依存関係を更新します。

   ```bash
   composer update
   ```

1. 新しいモジュールを有効にします。

   ```bash
   bin/magento module:enable Magento_AdobeCommerceEventsClient Magento_AdobeCommerceEventsGenerator Magento_AdobeIoEventsClient Magento_AdobeCommerceOutOfProcessExtensibility
   ```

クラウドインフラストラクチャー上のAdobe Commerceまたはオンプレミスのデプロイメントタイプに基づいて、インストールを最終処理します。

#### クラウドインフラストラクチャー上

クラウドインフラストラクチャー上のAdobe Commerceで、`.magento.env.yaml` の `ENABLE_EVENTING` グローバル変数を有効にします。 [ 詳細情報 ](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure/env/stage/variables-global.html?lang=ja#enable_eventing)。

```bash
stage:
   global:
      ENABLE_EVENTING: true
```

更新されたファイルをコミットしてクラウド環境にプッシュします。 デプロイメントが完了したら、次のコマンドでイベントの送信を有効にします。

```bash
bin/magento config:set adobe_io_events/eventing/enabled 1
```

#### オンプレミス

オンプレミス環境では、コード生成とAdobe Commerce イベントを手動で有効にする必要があります。

```bash
bin/magento events:generate:module
bin/magento module:enable Magento_AdobeCommerceEvents
bin/magento setup:upgrade
bin/magento setup:di:compile
bin/magento config:set adobe_io_events/eventing/enabled 1
```

### B2B 拡張機能のインストール

B2B マーチャントの場合、次の拡張機能をインストールして [ 購買依頼リスト ](events.md#b2b-events) イベントデータを含めます。

コマンドラインから次のコマンドを実行して、`magento/experience-platform-connector-b2b` 拡張機能をダウンロードします。

```bash
composer require magento/experience-platform-connector-b2b
```

### データサービス HIPAA 拡張機能のインストール

医療関係者向けに、次の拡張機能をインストールして、バックオフィスイベントデータが HIPAA に対応していることを確認します。

コマンドラインから次のコマンドを実行して、`magento/module-data-services-hipaa` 拡張機能をダウンロードします。

```bash
composer require magento/module-data-services-hipaa
```

## [!DNL Data Connection] 拡張機能の更新 {#update}

[!DNL Data Connection] 拡張機能を更新するには、コマンドラインから次のコマンドを実行します。

```bash
composer update magento/experience-platform-connector --with-dependencies
```

または、B2B マーチャントの場合：

```bash
composer update magento/experience-platform-connector-b2b --with-dependencies
```

2.0.0 から 3.0.0 などのメジャーバージョンにアップデートするには、プロジェクトのルート [!DNL Composer] `.json` ファイルを次のように編集します。

1. ルート `composer.json` ファイルを開き、`magento/experience-platform-connector` を検索します。

1. `require` セクションで、バージョン番号を次のように更新します。

   ```json
   "require": {
      ...
      "magento/experience-platform-connector": "^3.0",
      ...
    }
   ```

1. **保存** `composer.json`. コマンドラインから次のコマンドを実行します。

   ```bash
   composer update magento/experience-platform-connector –-with-dependencies
   ```

   または、B2B マーチャントの場合：

   ```bash
   composer update magento/experience-platform-connector-b2b --with-dependencies
   ```

## [!DNL Data Connection] 拡張機能をアンインストールします {#uninstall}

[!DNL Data Connection] 拡張機能をアンインストールするには、[ モジュールのアンインストール ](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/tutorials/uninstall-modules.html?lang=ja) を参照してください。
