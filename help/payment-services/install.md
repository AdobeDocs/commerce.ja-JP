---
title: ' [!DNL Payment Services]をインストール'
description: Payments Services拡張機能をインストールします。
exl-id: babaa91a-9376-4acb-b934-a89f9df52016
role: Admin
feature: Payments, Checkout, Install, Upgrade, Paas
badgePaas: label="PaaSのみ" type="Informative" url="https://experienceleague.adobe.com/ja/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce on Cloud プロジェクト（Adobeで管理されるPaaS インフラストラクチャ）とオンプレミス プロジェクトにのみ適用されます。"
source-git-commit: 5271668c99e7a66fbe857cd3ae26edfa54211621
workflow-type: tm+mt
source-wordcount: '606'
ht-degree: 0%

---

# [!DNL Payment Services]をインストール

[!DNL Adobe Commerce]および[!DNL Magento Open Source]の決済サービスを使い始めるには、いくつかのオンボーディング手順を完了する必要があります。

>[!INFO]
>
> 詳しくは、[Adobe Commerce](https://experienceleague.adobe.com/ja/docs/commerce-learn/tutorials/admin/adobe-commerce-services/configure-adobe-payment-services)の設定 [!DNL Payment Services] のビデオを参照してください。

[!DNL Adobe Commerce]および[!DNL Magento Open Source]の[!DNL Payment Services]拡張機能をダウンロードしてインストールすることは、[!DNL Payment Services]を使用するための前提条件です。

## 拡張機能をダウンロード

拡張機能をインストールするには、まず[Commerce Marketplace](https://experienceleague.adobe.com/docs/commerce-admin/start/resources/commerce-marketplace.html?lang=ja)からダウンロードする必要があります。

1. Commerce Marketplace[&#128279;](https://commercemarketplace.adobe.com/magento-payment-services.html)のPayment Services拡張機能に移動します。
1. エディションとバージョンを選択するには、**[!UICONTROL Edition]**&#x200B;と&#x200B;**[!UICONTROL Your store version]**&#x200B;を任意の選択範囲に切り替えます。
1. **[!UICONTROL Add to Cart]**&#x200B;をクリックします。
1. チェックアウトを完了し、**[!UICONTROL Place Order]**&#x200B;をクリックします。
1. Marketplaceのダウンロードに関連付けられているメールで、注文確認と詳細をご確認ください。

>[!NOTE]
>
> Adobe Commerce バージョン 2.4.7以降の場合[!DNL Payment Services]は、すぐに使用できます。

## 拡張機能のインストール

[!DNL Payment Services]拡張機能は、クラウドインフラストラクチャとオンプレミスの両方の[!DNL Adobe Commerce]にインストールできます。これらのインスタンスは、サインアッププロセスで提供されたCommerce アカウント [mageid](https://developer.adobe.com/commerce/marketplace/guides/sellers/profile-information/#access-keys)にリンクされています。
[!DNL Magento Open Source]人のお客様がオンプレミスの指示を使用しています。

Composerは、最初の[!DNL Adobe Commerce]のインストール中、またはComposer キーが以前に`auth.json` ファイルに保存されていなかった状況で、これらのキーを使用します。

Composer キーの取得について詳しくは、[認証キーの取得](https://experienceleague.adobe.com/ja/docs/commerce-operations/installation-guide/prerequisites/authentication-keys)を参照してください。

拡張機能をダウンロードしてインストールする前に考慮すべき点について詳しくは、[拡張機能をインストール &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-operations/installation-guide/tutorials/extensions)を参照してください。

### クラウド インフラストラクチャ上の[!DNL Adobe Commerce]

このメソッドは、Commerce Cloud インスタンスの[!DNL Payment Services]拡張機能のインストールに使用されます。

1. `composer.json` ファイルを更新します。

   ```bash
   composer require magento/payment-services --no-update
   ```

1. 依存関係を更新し、拡張機能をインストールします。

   ```bash
   composer update magento/payment-services --with-dependencies
   ```

   すべてのルート依存関係を更新するには、`composer update` コマンドを使用します。

1. 変更をコミットしてプッシュします。

### オンプレミスおよびその他の設定

この方法は、オンプレミス インスタンスと[!DNL Magento Open Source]のお客様に[!DNL Payment Services]拡張機能をインストールするために使用されます。

1. 拡張機能を取得するには、次のコマンドを実行します。

   ```bash
   composer require magento/payment-services --no-update
   ```

1. 依存関係を更新し、拡張機能をインストールします。

   ```bash
   composer update magento/payment-services --with-dependencies
   ```

   すべてのルート依存関係を更新するには、`composer update` コマンドを使用します。

1. インスタンスをアップグレードします。

   ```bash
   bin/magento setup:upgrade
   ```

1. キャッシュをクリアします。

   ```bash
   bin/magento cache:clean
   ```

1. 変更をコミットします。
1. コミットされたコードがデプロイされていることを確認するには、インスタンスを更新します。

>[!NOTE]
>
> [!DNL Payment Services] 1.6.1はPHP バージョン 7.xと互換性があります。 ただし、最新の[!DNL Payment Services] バージョンに更新することを強くお勧めします。

## 拡張機能のアップグレード

新しいバージョンの[!DNL Payment Services]がリリースされると、拡張機能を簡単にアップグレードできます。

1. パッケージの最新バージョンを取得するには：

   ```bash
   composer update magento/payment-services --with-dependencies
   ```

   すべてのルート依存関係を更新するには、`composer update` コマンドを使用します。

1. コンポーザーの更新後、以下を実行します。

   ```bash
   bin/magento setup:upgrade
   ```

1. 変更をコミットしてプッシュします。

## トラブルシューティング

[!DNL Payment Services]拡張機能をインストールしようとすると、エラーが表示される場合があります。 次のトラブルシューティング方法を使用して、エラーを解決します。

### リポジトリのリスト

リポジトリのリストに`repo.magento.com`が存在することを確認します。

### Composer キーが正しくありません

次のエラーが表示された場合は、間違ったコンポーザーキーがあることを示しています。

```
Could not find a matching version of package magento/payment-services. Check the package spelling, your version constraint and that the package is available in a stability which matches your minimum-stability (stable).
```

Composer キーが有効であり、他のMagento パッケージにアクセスできることを確認します。

設定されているコンポーザーのキーを確認するには：

1. `auth.json` ファイルの場所を検索します。

   ```bash
   composer config --global home
   ```

1. `auth.json` ファイルを表示：

   ```bash
   cat /path/to/auth.json
   ```

1. Commerce アカウント `MageID`[&#128279;](https://experienceleague.adobe.com/ja/docs/commerce-operations/installation-guide/prerequisites/authentication-keys)に関連付けられているキーはを参照してください。

### PHPに十分なメモリがありません

次のエラーが表示された場合は、PHP用のメモリが不足していることを示しています。

```
Fatal error: Allowed memory size of 2146435072 bytes exhausted (tried to allocate 4096 bytes) in phar:///usr/local/bin/composer/src/Composer/DependencyResolver/RuleWatchGraph.php on line 52
```

[環境上のPHPのメモリ制限](https://experienceleague.adobe.com/ja/docs/commerce-cloud-service/user-guide/configure/app/php-settings#increase-php-memory-limit)を`php.ini`に増やします。

または、次のコマンドを使用してメモリ制限を指定できます：`php -d memory_limit=-1 [path to composer]/composer require magento/payment-services`。

例：

```bash
php -d memory_limit=-1 vendor/bin/composer require magento/payment-services
```
