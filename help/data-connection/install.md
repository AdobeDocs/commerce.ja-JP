---
title: ' [!DNL Data Connection]をインストール'
description: Adobe Commerceから [!DNL Data Connection] 拡張機能をインストール、更新、アンインストールする方法について説明します。
role: Admin, Developer
feature: Install
exl-id: 853ef2d1-85cb-41a8-9b07-887a758ed401
source-git-commit: 14c4178338859d55a7391139033d51d1aa6f7678
workflow-type: tm+mt
source-wordcount: '448'
ht-degree: 0%

---

# [!DNL Data Connection]をインストール

拡張機能をインストールする前に、[前提条件を確認してください](overview.md#prerequisites)。

## 拡張機能のインストール

[!DNL Data Connection]拡張機能は、[Adobe Marketplace](https://commercemarketplace.adobe.com/magento-experience-platform-connector.html)から入手できます。 この拡張機能をサーバーのコマンドラインからインストールすると、Adobe Commerce インストールに[ サービス ](../landing/saas.md)として接続されます。 プロセスが完了すると、Commerce **[!DNL Data Connection]**&#x200B;管理者&#x200B;**の** サービス **の** システム **メニューに**&#x200B;と&#x200B;_Commerce サービス コネクタ_&#x200B;が表示されます。

![[!DNL Data Connection]拡張機能の管理者ビュー](assets/epc-adminui.png)

>[!IMPORTANT]
>
>拡張機能の名前がExperience Platform コネクタから[!DNL Data Connection]に変更されましたが、パッケージ名は後方互換性をサポートするために`experience-platform-connector`のままです。

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

1. （オプション） [!DNL Live Search]検索イベント [を含む](events.md#search-events) データを含めるには、[[!DNL Live Search]](../live-search/install.md)拡張機能をインストールします。

1. （オプション） [要件イベント ](events.md#b2b-events)を含むB2B データを含めるには、[B2B拡張機能](#install-the-b2b-extension)をインストールします。

1. （オプション）ヘルスケア販売者の場合は、[のバックオフィスデータがHIPAA対応となるように、](#install-the-data-services-hipaa-extension)Data Services HIPAA[!DNL Commerce]拡張機能をインストールします。

### Adobe I/O Eventsをインストールし、customers-connector モジュールを設定します

`experience-platform-connector`拡張機能をインストールした後、Adobe Commerce用Adobe I/O Eventsをインストールし、`customers-connector` モジュールを設定する必要があります。

次の手順は、Adobe Commerce on cloud インフラストラクチャとオンプレミスの両方のインストールに適用されます。

1. Commerce 2.4.4または2.4.5を実行している場合は、次のコマンドを使用してイベントモジュールを読み込みます。

   ```bash
   composer require magento/commerce-eventing=^1.0 --no-update
   ```

   Commerce 2.4.6以降では、これらのモジュールが自動的に読み込まれます。

1. プロジェクトの依存関係を更新します。

   ```bash
   composer update
   ```

1. 新しいモジュールを有効にします。

   ```bash
   bin/magento module:enable Magento_AdobeCommerceEventsClient Magento_AdobeCommerceEventsGenerator Magento_AdobeIoEventsClient Magento_AdobeCommerceOutOfProcessExtensibility
   ```

デプロイメントタイプに基づいて、インストールを最終化します。Adobe Commerce on Cloud インフラストラクチャまたはオンプレミス。

#### オンクラウドのインフラ

Adobe Commerce on Cloud インフラストラクチャで、`ENABLE_EVENTING`で`.magento.env.yaml` グローバル変数を有効にします。 [学習を増やす](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure/env/stage/variables-global.html#enable_eventing)。

```bash
stage:
   global:
      ENABLE_EVENTING: true
```

更新されたファイルをコミットしてクラウド環境にプッシュします。 デプロイメントが完了したら、次のコマンドを使用してイベントの送信を有効にします。

```bash
bin/magento config:set adobe_io_events/eventing/enabled 1
```

#### オンプレミス

オンプレミス環境では、コード生成とAdobe Commerce Eventsを手動で有効にする必要があります。

```bash
bin/magento events:generate:module
bin/magento module:enable Magento_AdobeCommerceEvents
bin/magento setup:upgrade
bin/magento setup:di:compile
bin/magento config:set adobe_io_events/eventing/enabled 1
```

### B2B拡張機能のインストール

B2B マーチャントの場合は、次の拡張機能をインストールして、[要求リスト ](events.md#b2b-events)のイベントデータを含めます。

コマンドラインから次を実行して、`magento/experience-platform-connector-b2b`拡張機能をダウンロードします。

```bash
composer require magento/experience-platform-connector-b2b
```

### Data Services HIPAA拡張機能のインストール

ヘルスケア業界のマーチャントは、次の拡張機能をインストールして、バックオフィスのイベントデータがHIPAA対応であることを確認する必要があります。

コマンドラインから次を実行して、`magento/module-data-services-hipaa`拡張機能をダウンロードします。

```bash
composer require magento/module-data-services-hipaa
```

## [!DNL Data Connection]拡張機能を更新 {#update}

[!DNL Data Connection]拡張機能を更新するには、コマンドラインから次のコマンドを実行します。

```bash
composer update magento/experience-platform-connector --with-dependencies
```

B2B マーチャントの場合：

```bash
composer update magento/experience-platform-connector-b2b --with-dependencies
```

2.0.0から3.0.0などのメジャーバージョンに更新するには、プロジェクトのルート [!DNL Composer] `.json` ファイルを次のように編集します。

1. ルート `composer.json` ファイルを開き、`magento/experience-platform-connector`を検索します。

1. 「`require`」セクションで、バージョン番号を次のように更新します。

   ```json
   "require": {
      ...
      "magento/experience-platform-connector": "^3.0",
      ...
    }
   ```

1. **保存** `composer.json`。 次に、コマンドラインから次のコマンドを実行します。

   ```bash
   composer update magento/experience-platform-connector –-with-dependencies
   ```

   B2B マーチャントの場合：

   ```bash
   composer update magento/experience-platform-connector-b2b --with-dependencies
   ```

## [!DNL Data Connection]拡張機能のアンインストール {#uninstall}

[!DNL Data Connection]拡張機能をアンインストールするには、[ モジュールのアンインストール ](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/tutorials/uninstall-modules.html)を参照してください。
