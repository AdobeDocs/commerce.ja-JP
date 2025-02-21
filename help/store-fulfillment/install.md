---
title: インストール
description: Composer for PHP を使用して、Adobe Commerce ストアフロント用に  [!DNL Store Fulfillment solution]  をインストールします。
role: Admin, Developer
level: Intermediate
feature: Shipping/Delivery, Install
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '666'
ht-degree: 0%

---


# インストール

非実稼動環境で [!DNL Store Fulfillment for Adobe Commerce by Walmart Commerce Technologies] 拡張機能の最初のインストールを完了します。キューマネージャーを実行し、例外処理ができるようにキャッシュを設定します。 Adobe Commerce インスタンスを運用および保守するためのベストプラクティスを確実に実施するための開発ツールが、お使いの開発環境に含まれていることを確認してください。

>[!TIP]
>
>[2}Adobe Commerceアップグレードガイド } の ](https://experienceleague.adobe.com/docs/commerce-operations/upgrade-guide/modules/upgrade.html) アップグレード手順 _に従って、オンプレミスのAdobe Commerceのストアフルフィルメント拡張機能をアップグレードします。_&#x200B;クラウドインフラストラクチャー上のAdobe Commerceについては、{2](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure-store/extensions.html#upgrade-an-extension) クラウドインフラストラクチャー上のCommerce ガイドの [ 拡張機能のアップグレード *を参照してください。*

## 前提条件

Store Fulfillment ソリューションの [ 要件 ](solution-requirements.md) を確認し、Adobe Commerce用の [!DNL Store Fulfillment] 拡張機能をインストールまたはアップグレードする前に、必要な情報を収集します。

プレリリース版またはベータ版の Store Fulfillment for Adobe Commerce拡張機能をインストールしている場合は、現在のバージョンをインストールする前に、次のコマンドを使用して削除します。

```bash
rm -rf composer.lock vendor/walmart &&
composer require walmart/magento-bopis-metapackage:1.0.0
```

## インストール要件

- **Walmart Commerce Technologies ソフトウェアアーカイブ（.zip ファイル）によるストアフルフィルメントへのアクセス** - オンボーディングおよび有効化プロセス中は、担当のアカウントマネージャーと協力して、ストアフルフィルメント拡張機能のインストールファイルにアクセスできます。

- **Adobe Commerce アカウント情報** - [!DNL Store Fulfillment] ソリューションをインストールするには、[[!DNL Commerce]  アカウント ](https://experienceleague.adobe.com/en/docs/commerce-admin/start/commerce-account/commerce-account-create){target="_blank"} が必要です。 [!DNL Adobe Commerce] プロジェクトへの所有者または管理者アクセス権を持つアカウント ID と資格情報が必要です。

- クラウドインフラストラクチャプロジェクトに [!DNL Adobe Commerce] いては、ソフトウェアインストーラーがクラウドプロジェクトへの管理者アクセス権を持っている必要があります。 [ ユーザーアクセスの管理 ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/project/user-access) を参照してください。

- **Composer と[!DNL Commerce CLI]** の使用経験 – これらのツールを使用して [!DNL Adobe Commerce] プラットフォームで拡張機能をインストールおよび管理する方法については、[ 一般的な CLI のインストール ](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/tutorials/extensions){target="_blank"} を参照してください。

- **Adobe Commerceにサードパーティの拡張機能をインストールした経験** – 詳しくは、Adobe Commerceのドキュメントを参照してください。

   - [ クラウドインフラストラクチャインスタンス上のAdobe Commerceの拡張機能をインストール ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/configure-store/extensions#install-an-extension)。

   - [Adobe Commerce オンプレミスインスタンスの拡張機能をインストールします ](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/tutorials/extensions)。

### 手順 1：拡張機能バンドルをダウンロードする

アカウント担当者の指示に従って、Store Fulfillment Services 拡張機能をインストールするための Composer パッケージを含むアーカイブ ファイルをダウンロードします。

### 手順 2：拡張機能アーティファクトをアプリケーションに抽出する

統合バンドルを含むアーカイブファイルを抽出して、Store Fulfillment Services 拡張機能をインストールします。

1. 抽出したファイルのターゲットディレクトリを作成します。

   - コマンドラインから、web サーバーの doc ルートディレクトリに移動します。

   - `artifacts` ディレクトリを作成します。

1. アーカイブ・ファイルを新しいディレクトリに解凍します。

1. ファイルのリストを確認して、ファイルが正常に抽出されたことを確認します。

   ```
   ../var/www/html/artifacts]$ ls -a
   .
   ..
   bopis-sdk.zip
   module-magento-bopis-alternate-pickup-contact-admin-ui.zip
   module-magento-bopis-alternate-pickup-contact-api.zip
   ```

### 手順 3:Composer を使用したアプリケーションの設定

Composer を使用して、インストールのソース ディレクトリを設定し、Store Fulfillment Services 拡張機能をインストールします。

1. Composer インストールのソース リポジトリを設定します。

   ```bash
   composer config repositories.artifacts artifact artifacts/
   ```

1. Store Fulfillment Services 拡張機能を `composer.json` に追加します。

   ```bash
   composer require walmart/magento-bopis-metapackage:1.0.0
   ```

>[!NOTE]
>
>Adobe Commerceのオンプレミスインスタンスのパフォーマンスを向上させるには、[ 自動ロード設定を更新する ](https://experienceleague.adobe.com/docs/commerce-operations/performance-best-practices/deployment-flow.html#update-the-autoloader) ことができます。`composer dump-autoload --optimize`

### 手順 4：データベーススキーマとデータをアップグレードする

`bin/magento setup:upgrade` を使用してインストールを完了し、ストアフルフィルメントソリューションをサポートするための変更でデータベーススキーマとデータを更新します。

>[!NOTE]
>
>クラウドインフラストラクチャプロジェクトのAdobe Commerceの場合、拡張機能を登録する必要はありません。 代わりに、前のステップで変更したコードをコミットして、環境ブランチにプッシュします。 データベーススキーマとデータを更新するコマンドは、クラウドのビルドおよびデプロイメントプロセス中に自動的に実行されます。

### 手順 5：インストールの完了

1. `setup:upgrade` Magento CLI コマンドを使用して、拡張機能をAdobe Commerceに登録します。

   ```bash
   bin/magento setup:upgrade
   ```

1. プロンプトが表示されたら、[!DNL Commerce] プロジェクトを再コンパイルします。

   ```bash
   bin/magento setup:di:compile
   ```

1. キャッシュをクリーンアップします。

   ```bash
   bin/magento cache:clean
   ```

1. メンテナンスモードを無効にします。

   ```bash
   bin/magento maintenance:disable
   ```

### 手順 6：インストールの確認

Adobe Commerce サーバーで、Store Fulfillment Services 拡張機能のモジュールがインストールされ、有効になっていることを確認します。

1. サーバーにログインします。

   クラウドインフラストラクチャー上のAdobe Commerceにインストールするには、[SSH を使用してリモート環境にログイン ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/secure-connections#ssh) します。

1. Store Fulfillment Services モジュールが有効になっていることを確認します。

   ```bash
   bin/magento module:status  --enabled | grep Walmart
   ```

   出力には、次のモジュールが含まれている必要があります。

   ```
   Walmart_BopisBase
   Walmart_BopisAlternatePickupContact
   Walmart_BopisAlternatePickupContactFrontend
   Walmart_BopisApiConnector
   Walmart_BopisAlternatePickupContactAdminUi
   Walmart_BopisCheckoutPickInStoreApi
   Walmart_BopisInventorySourceAdminUi
   Walmart_BopisCheckoutPickInStore
   Walmart_BopisInventoryCatalogApi
   Walmart_BopisPreferredLocationApi
   Walmart_BopisHomeDeliveryApi
   Walmart_BopisHomeDelivery
   Walmart_BopisPreferredLocation
   Walmart_BopisInventoryCatalog
   Walmart_BopisPreferredLocationFrontend
   Walmart_BopisCheckoutPickInStoreAdminUi
   Walmart_BopisInventorySourceApi
   Walmart_BopisInventorySourceFaasSync
   Walmart_BopisInventorySourceReservation
   Walmart_BopisLocationCheckInApi
   Walmart_BopisLogging
   Walmart_BopisStoreAssociateApi
   Walmart_BopisLocationCheckInFrontend
   Walmart_BopisStoreAssociate
   Walmart_BopisOperationQueue
   Walmart_BopisOperationQueueAdminUi
   Walmart_BopisOperationQueueApi
   Walmart_BopisOrderFaasSync
   Walmart_BopisOrderUpdateApi
   Walmart_BopisLocationCheckIn
   Walmart_BopisInventoryCatalogAdminUi
   Walmart_BopisPreferredLocationAdminUi
   Walmart_BopisDeliverySelection
   Walmart_BopisCheckoutPickInStoreFrontend
   Walmart_BopisLocationCheckInAdminUi
   Walmart_BopisStoreAssociateAdminUi
   Walmart_BopisOrderUpdate
   Walmart_BopisStoreAssociateTfa
   Walmart_BopisStoreAssociateTfaApi
   ```

### その他の手順

必要に応じて、[setup:static-content:deploy](https://experienceleague.adobe.com/en/docs/commerce-operations/tools/cli-reference/commerce-on-premises){target="_blank"} CLI コマンドを使用して、静的ビューファイルを実稼動環境にデプロイします。

```bash
php bin/magento setup:static-content:deploy -f
```

空白のテーマを使用する場合は、`-f` のオプションが必要です。

>[!NOTE]
>
>詳しくは、Adobe Commerce ヘルプセンターの記事 [Adobe Commerceでの静的コンテンツのデプロイのベストプラクティス ](https://experienceleague.adobe.com/docs/commerce-operations/implementation-playbook/best-practices/development/static-content-deployment.html) を参照してください。


