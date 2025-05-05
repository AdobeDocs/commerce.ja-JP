---
title: インストール  [!DNL Payment Services]
description: 支払いサービス拡張機能をインストールします。
role: Admin
feature: Payments, Checkout, Install, Upgrade
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '494'
ht-degree: 0%

---

# [!DNL Payment Services] のインストール

[!DNL Adobe Commerce] と [!DNL Magento Open Source] の支払いサービスの使用を開始するには、いくつかのオンボーディング手順を完了する必要があります。

>[!INFO]
>
> 詳しくは、[Adobe Commerce用の設定  [!DNL Payment Services]  ビデオ ](https://experienceleague.adobe.com/ja/docs/commerce-learn/tutorials/admin/adobe-commerce-services/configure-adobe-payment-services) 参照してください。

[!DNL Adobe Commerce] および [!DNL Magento Open Source] 用の [!DNL Payment Services] 拡張機能をダウンロードしてインストールすることは、[!DNL Payment Services] を使用するための前提条件の手順です。

## 拡張機能のダウンロード

インストールする前に、まず [&#128279;](https://experienceleague.adobe.com/docs/commerce-admin/start/resources/commerce-marketplace.html?lang=ja)0&rbrace;Commerce Marketplace&rbrace; から拡張機能をダウンロードする必要があります。

1. [Commerce Marketplaceの支払いサービス拡張機能 ](https://commercemarketplace.adobe.com/magento-payment-services.html) に移動します。
1. エディションとバージョンを選択するには、**[!UICONTROL Edition]** と **[!UICONTROL Your store version]** を希望の選択項目に切り替えます。
1. 「**[!UICONTROL Add to Cart]**」をクリックします。
1. チェックアウトを完了し、「**[!UICONTROL Place Order]**」をクリックします。
1. 注文の確認と詳細については、Marketplace のダウンロードに関連するメールを確認してください。

>[!NOTE]
>
> Adobe Commerce バージョン 2.4.7 以降 [!DNL Payment Services] 場合は、すぐに使用できます。

## 拡張機能のインストール

[!DNL Payment Services] 拡張機能は、クラウドインフラストラクチャー上のインスタンスとオンプレミスインスタンスの両方に対してイ [!DNL Adobe Commerce] ストールできます。これらのインスタンスは、登録プロセスで提供されるCommerce アカウント [mageid](https://developer.adobe.com/commerce/marketplace/guides/sellers/profile-information/#access-keys) にリンクされています。
オンプレミスの手順を使用するお客様は [!DNL Magento Open Source] とんどいません。

Composer は、[!DNL Adobe Commerce] の初期インストール時、または Composer のキーが以前に `auth.json` ファイルに保存されていなかった場合に、これらのキーを使用します。

Composer キーの取得の詳細については、[ 認証キーの取得 ](https://experienceleague.adobe.com/ja/docs/commerce-operations/installation-guide/prerequisites/authentication-keys) を参照してください。

拡張機能をダウンロードしてインストールする前に考慮すべき事項について詳しくは、[ 拡張機能のインストール ](https://experienceleague.adobe.com/ja/docs/commerce-operations/installation-guide/tutorials/extensions) を参照してください。

### クラウドインフラストラクチャー上の [!DNL Adobe Commerce]

この手法は、Commerce Cloud インスタンスの [!DNL Payment Services] 拡張機能をインストールするために使用されます。

1. `composer.json` ファイルを更新します。

   ```bash
   composer require magento/payment-services --no-update
   ```

1. 依存関係を更新し、拡張機能をインストールします。

   ```bash
   composer update magento/payment-services --with-dependencies
   ```

   `composer update` コマンドを使用して、すべてのルート依存関係を更新します。

1. 変更をコミットし、プッシュします。

### オンプレミスおよびその他の設定

この方法は、オンプレミスのインスタンスおよび [!DNL Magento Open Source] のお客様の [!DNL Payment Services] 拡張機能をインストールする場合に使用します。

1. 拡張機能を取得するには、次のコマンドを実行します。

   ```bash
   composer require magento/payment-services --no-update
   ```

1. 依存関係を更新し、拡張機能をインストールします。

   ```bash
   composer update magento/payment-services --with-dependencies
   ```

   `composer update` コマンドを使用して、すべてのルート依存関係を更新します。

1. インスタンスをアップグレード：

   ```bash
   bin/magento setup:upgrade
   ```

1. キャッシュをクリアする：

   ```bash
   bin/magento cache:clean
   ```

1. 変更をコミットします。
1. コミットされたコードが確実にデプロイされるように、インスタンスを更新します。

>[!NOTE]
>
> [!DNL Payment Services] 1.6.1 は、PHP バージョン 7.x と互換性があります。ただし、[!DNL Payment Services] の最新バージョンにアップデートすることを強くお勧めします。

## 拡張機能のアップグレード

新しいバージョンの [!DNL Payment Services] がリリースされると、拡張機能を簡単にアップグレードできます。

1. パッケージの最新バージョンを取得するには：

   ```bash
   composer update magento/payment-services --with-dependencies
   ```

   `composer update` コマンドを使用して、すべてのルート依存関係を更新します。

1. コンポーザーを更新した後、次のコマンドを実行します。

   ```bash
   bin/magento setup:upgrade
   ```

1. 変更をコミットし、プッシュします。

## トラブルシューティング

[!DNL Payment Services] 拡張機能をインストールしようとすると、エラーが発生することがあります。 次のトラブルシューティング方法を使用して、エラーを解決します。

### リポジトリーのリスト

リポジトリーのリストに `repo.magento.com` が存在することを確認します。

### コンポーザーのキーが正しくありません

Composer キーが正しくないことを示す次のエラーが表示される場合：

```
Could not find a matching version of package magento/payment-services. Check the package spelling, your version constraint and that the package is available in a stability which matches your minimum-stability (stable).
```

Composer キーが有効で、他のMagento パッケージにアクセスできることを確認します。

設定されている Composer キーを確認するには：

1. `auth.json` ファイルの場所を見つけます。

   ```bash
   composer config --global home
   ```

1. `auth.json` ファイルを表示します。

   ```bash
   cat /path/to/auth.json
   ```

1. 詳しくは [Commerce アカウントに関連付けられているキ `MageID`](https://experienceleague.adobe.com/ja/docs/commerce-operations/installation-guide/prerequisites/authentication-keys) を参照してください。

### PHP に必要なメモリが不足しています

PHP 用のメモリが足りないことを示す次のエラーが表示された場合：

```
Fatal error: Allowed memory size of 2146435072 bytes exhausted (tried to allocate 4096 bytes) in phar:///usr/local/bin/composer/src/Composer/DependencyResolver/RuleWatchGraph.php on line 52
```

[ メモリ制限を増やす ](https://experienceleague.adobe.com/ja/docs/commerce-cloud-service/user-guide/configure/app/php-settings#increase-php-memory-limit) ご使用の環境の PHP の場合は、`php.ini` を使用します。

または、次のコマンドを使用してメモリ制限を指定できます：`php -d memory_limit=-1 [path to composer]/composer require magento/payment-services`。

例：

```bash
php -d memory_limit=-1 vendor/bin/composer require magento/payment-services
```
