---
title: Adobe Commerce パッケージのインストール
description: Adobe Commerce インスタンスにAEM Assets Integration for Adobe Commerce拡張機能をインストールする方法について説明します。 この拡張機能は、Adobe Commerceで製品ビジュアルを使用するために必要です。
feature: CMS, Media
badgePaas: label="PaaS のみ" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce on Cloud プロジェクト（Adobeが管理する PaaS インフラストラクチャ）およびオンプレミスプロジェクトにのみ適用されます。"
source-git-commit: 3ecc429003490235211a812af064d1b10d053e38
workflow-type: tm+mt
source-wordcount: '1460'
ht-degree: 0%

---

# Adobe Commerce パッケージのインストール

Commerceのこの統合により、Adobe CommerceとAdobe Experience Manager Assets（AEM Assets）間のアセットを同期できます。 この拡張機能は、両方のプラットフォームで製品画像、ビデオ、その他のメディアアセットを管理するための一連のツールとサービスを提供します。

`aem-assets-integration` PHP 拡張機能をインストールすることにより、この拡張機能をCommerce環境に追加します。 また、Adobe CommerceのAdobe I/O Eventsを有効にして、CommerceとAdobe Experience Manager Assets間の通信およびワークフローに必要な資格情報を生成する必要があります。

**アクセス要件**

CommerceとAEM Assetsの統合を有効にするには、以下の役割と権限が必要です。

- [Commerce クラウドプロジェクト管理者 ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/project/user-access) – 必要な拡張機能をインストールして、管理者またはコマンドラインからCommerce アプリケーションサーバーを設定します。

   - [repo.magento.com](https://repo.magento.com/admin/dashboard) にアクセスして拡張機能をインストールします。

     キーの生成と必要な権限の取得については、[ 認証キーの取得 ](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/prerequisites/authentication-keys) を参照してください。 クラウドインストールについては、[Commerce on Cloud Infrastructure ガイドを参照してください ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/authentication-keys)

- [Commerce管理者 ](https://experienceleague.adobe.com/en/docs/commerce-admin/start/guide-overview) - ストア設定を更新し、Commerce ユーザーアカウントを管理します。

>[!TIP]
>
> Adobe Commerceは、[Adobe IMS認証 ](https://experienceleague.adobe.com/en/docs/commerce-admin/start/admin/ims/adobe-ims-config) を使用するように設定できます。

## インストールと設定のワークフロー

Adobe Commerce パッケージをインストールし、次のタスクを実行してCommerce環境を準備します。

1. [AEM Assets Integration for Commerce拡張機能（`aem-assets-integration`）をインストールします ](#install-the-aem-assets-integration-extension)。

1. [Commerce サービスコネクタを設定 ](#configure-the-commerce-services-connector) して、Adobe Commerce インスタンスと、Adobe CommerceとAEM Assets間でデータを転送できるサービスを接続します。

1. [Commerce用のAdobe I/O Eventsの設定](#configure-adobe-io-events-for-commerce)

1. [API アクセスの認証資格情報の取得](#get-authentication-credentials-for-api-access)

## `aem-assets-integration` 拡張機能のインストール

Adobe Commerce 2.4.5 以降のバージョンのAdobe Commerce インスタンスに、製品ビジュアル用の最新バージョンのAEM Assets統合拡張機能（`aem-assets-integration`）をインストールします。 拡張機能は、[repo.magento.com](https://repo.magento.com/admin/dashboard) リポジトリからコンポーザメタパッケージとして提供されます。

>[!BEGINTABS]

>[!TAB  クラウドインフラストラクチャ ]

Commerce Cloud インスタンスに [!DNL AEM Assets Integration] 拡張機能をインストールするには、この方法を使用します。

1. ローカルワークステーションで、Adobe Commerce on cloud infrastructure プロジェクトのプロジェクトディレクトリに移動します。

   >[!NOTE]
   >
   >Commerce Adobe Commerce プロジェクト環境のローカル管理について詳しくは、_クラウドインフラストラクチャユーザーガイドの [CLI を使用したブランチの管理 ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/cli-branches) を参照してください_。

1. Adobe Commerce Cloud CLI を使用して更新する環境ブランチを確認します。

   ```shell
   magento-cloud environment:checkout <environment-id>
   ```

1. AEM Assets Integration for Commerce拡張機能を追加します。

   ```shell
   composer require "magento/aem-assets-integration" "<version-tbd>" --no-update
   ```

1. パッケージの依存関係を更新します。

   ```shell
   composer update "magento/aem-assets-integration"
   ```

1. `composer.json` ファイルと `composer.lock` ファイルのコード変更をコミットしプッシュします。

1. `composer.json` ファイルと `composer.lock` ファイルのコード変更を追加、コミットし、クラウド環境にプッシュします。

   ```shell
   git add -A
   git commit -m "Install AEM Assets Integration extension for Adobe Commerce"
   git push origin <branch-name>
   ```

   更新をプッシュすると、[Commerce クラウドデプロイメントプロセス ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/deploy/process) が開始され、変更が適用されます。 [ デプロイメントログ ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/test/log-locations#deploy-log) からデプロイメントステータスを確認します。

>[!TAB  オンプレミス ]

オンプレミスのインスタンスに [!DNL AEM Assets Integration] 拡張機能をインストールするには、この方法を使用します。

1. Composer を使用して、AEM Assets Integration for Commerce拡張機能をプロジェクトに追加します。

   ```shell
   composer require "magento/aem-assets-integration" --no-update
   ```

1. 依存関係を更新し、拡張機能をインストールします。

   ```shell
   composer update  "magento/aem-assets-integration"
   ```

1. Adobe Commerceをアップグレード :

   ```shell
   bin/magento setup:upgrade
   ```

1. キャッシュをクリアする：

   ```shell
   bin/magento cache:clean
   ```

>[!TIP]
>
>実稼動環境にデプロイする場合は、時間を節約するために、コンパイル済みのコードをクリアしないことを検討します。 変更を行う前に、必ずシステムをバックアップしてください。

>[!ENDTABS]

## Commerce サービスコネクタの設定

>[!NOTE]
>
>Commerce Services Connector のセットアップは、[Adobe Commerce SaaS サービス ](https://experienceleague.adobe.com/en/docs/commerce/user-guides/integration-services/saas#availableservices) を使用するために必要な 1 回限りのプロセスです。 別のサービス用にコネクタを既に設定している場合は、Commerce管理で **[!UICONTROL Systems]** > [!UICONTROL Services] > **[!UICONTROL Commerce Services Connector]** を選択すると、既存の設定を表示できます。

Adobe Commerce インスタンスとAEM Assets統合を有効にするサービスの間でデータを転送するには、管理者（**[!UICONTROL System]**/[!UICONTROL Services]/**[!UICONTROL Commerce Services Connector]**）からCommerce サービスコネクタを設定します。

![AEM Assets統合用の SaaS プロジェクトおよびデータ空間 ID](../assets/aem-saas-project-config.png){width="600" zoomable="yes"}

設定で次の値を指定します

- 認証用の実稼働およびサンドボックスの API キー
- セキュリティで保護されたクラウドストレージのデータ領域名（SaaS 識別子）
- CommerceとAEM Assets環境がプロビジョニングされる IMS 組織 ID

手順について詳しくは、[Commerce サービスコネクタ ](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/admin/adobe-commerce-services/configure-adobe-commerce-services-connector#configuration-faqs) のドキュメントの [Commerce サービスコネクタ設定のビデオをご覧くだ ](../../landing/saas.md#organizationid) い。

設定を保存すると、システムによって環境の SaaS プロジェクトとデータベース ID が生成されます。 これらの値は、Adobe CommerceとAEM Assets間のアセット同期を有効にするために必要です。

## Commerce用のAdobe I/O Eventsの設定

AEM Assets統合では、Adobe I/O Events サービスを使用して、Commerce インスタンスとExperience Cloudの間でカスタムイベントデータを送信します。 イベントデータは、AEM Assets統合のワークフローを調整するために使用されます。

Adobe I/O Eventsを設定する前に、Commerce プロジェクトの RabbitMQ と cron ジョブ設定を確認します。

- RabbitMQ が有効になっていて、イベントをリッスンしていることを確認します。
   - [Adobe Commerce オンプレミス用の RabbitMQ のセットアップ ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/configure/service/rabbitmq)
   - [ クラウドインフラストラクチャー上のAdobe Commerce用の RabbitMQ のセットアップ ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/configure/service/rabbitmq)
   - [cron ジョブが有効 ](https://developer.adobe.com/commerce/extensibility/events/configure-commerce/#check-cron-and-message-queue-configuration) であることを確認します。 Cron ジョブは、AEM Assets統合のための通信およびワークフローに必要です。

>[!NOTE]
>
> Commerce バージョン 2.4.5 のプロジェクトの場合、[Adobe I/O モジュールをインストール ](https://developer.adobe.com/commerce/extensibility/events/installation/#install-adobe-io-modules-on-commerce) する必要があります。 Commerce バージョン 2.4.6 以降では、これらのモジュールは自動的に読み込まれます。 CommerceのAEM Assets統合の場合は、モジュールをインストールするだけで済みます。 App Builderの設定は不要です。


### Commerce イベントフレームワークの有効化

Commerce Admin からイベントフレームワークを有効にします。

>[!NOTE]
>
>App Builderの設定が必要になるのは、CommerceとAEM Assetsの間でアセットを同期するためにカスタムのマッチング方法を使用する予定がある場合のみです。

1. 管理者から、**[!UICONTROL Stores]**/[!UICONTROL Settings]/**[!UICONTROL Configuration]**/**[!UICONTROL Adobe Services]**/**Adobe I/O Events** に移動します。

1. **[!UICONTROL Commerce events]** を展開します。

1. **[!UICONTROL Enabled]** を `Yes` に設定します。

   ![Adobe I/O Events Commerceの管理者設定 – Commerce イベントを有効にする ](../assets/aem-enable-io-event-admin-config.png){width="600" zoomable="yes"}

1. **[!UICONTROL Merchant ID]** に商社の名前を入力し、**[!UICONTROL Environment ID]** のフィールドに環境名を入力します。 これらの値を設定する場合は、英数字とアンダースコアのみを使用します。

>[!BEGINSHADEBOX]

**ブロックリクエスト用のカスタム VCL の設定**

カスタム VCL スニペットを使用して、不明な受信リクエストをブロックする場合は、HTTP ヘッダー `X-Ims-Org-Idheader` を含めて、Commerce サービスのAEM Assets Integration からの着信接続を許可する必要がある可能性があります。

>[!TIP]
>
> Fastly CDN モジュールを使用し、ブロックする IP アドレスのリストを含んだEdge ACL を作成できます。

次のカスタム VCL スニペットコード（JSON 形式）は、`X-Ims-Org-Id` リクエストヘッダーを持つ例を示しています。

```json
{
  "name": "blockbyuseragent",
  "dynamic": "0",
  "type": "recv",
  "priority": "5",
  "content": "if ( req.http.X-ims-org ~ \"<YOUR-IMS-ORG>\" ) {error 405 \"Not allowed\";}"
}
```

この例に基づいてスニペットを作成する前に、値を確認して、変更が必要かどうかを判断してください。

- `name`: VCL スニペットの名前。 この例では、`blockbyuseragent` という名前を使用します。

- `dynamic`: スニペットのバージョンを設定します。 この例では、`0` を使用します。 詳細なデータモデル情報については、[Fastly VCL スニペット ](https://www.fastly.com/documentation/reference/api/vcl-services/snippet/) を参照してください。

- `type`: VCL スニペットのタイプを指定します。このスニペットは、生成された VCL コード内のスニペットの場所を決定します。 この例では、`recv` を使用します。 スニペットタイプのリストについては、[Fastly VCL スニペットリファレンス ](https://www.fastly.com/documentation/reference/api/#api-section-snippet) を参照してください。

- `priority`: VCL スニペットを実行するタイミングを指定します。 この例では、優先度 `5` を使用してすぐに実行し、許可された IP アドレスからの管理リクエストであるかどうかを確認します。

- `content`：実行する VCL コードのスニペット。クライアントの IP アドレスを確認します。 IP がEdgeの ACL に含まれている場合は、web サイト全体に対して `405 Not allowed` エラーが発生して IP のアクセスがブロックされます。 その他すべてのクライアント IP アドレスへのアクセスが許可されます。

VCL スニペットを使用して受信リクエストをブロックする方法については、『クラウドインフラストラクチャー上の _Commerceガイド ](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/cdn/custom-vcl-snippets/fastly-vcl-blocking) の [Custom VCL for blocking requests_ を参照してください。

>[!ENDSHADEBOX]

## API アクセスの認証資格情報の取得

CommerceのAEM Assets統合では、Commerce インスタンスへの API アクセスを許可するために、OAuth 認証資格情報が必要です。 これらの資格情報は、AEM Assets統合を使用してアセットを管理する際に API リクエストの認証に必要です。

資格情報を生成するには、統合をCommerce インスタンスに追加し、インスタンスをアクティベートします。

### Commerce環境への統合の追加

1. 管理者で、**システム**/拡張機能/**統合** に移動し、「**新規統合を追加**」をクリックします。

1. 統合に関する情報を入力します。

   「**一般**」セクションでは、統合 **名前** と **メール** のみを指定します。 CommerceとExperience Manager Assetsがデプロイされている組織にアクセスできるAdobe IMSアカウントのメールを使用します。

   ![Commerce管理者設定用のAEM Assets統合 ](../assets/aem-add-commerce-integration.png){width="600" zoomable="yes"}

1. **ID を確認** をクリックして ID を確認します。

   Adobe ID を使用してExperience Cloudの認証を行うことで、ID が検証されます。

1. API リソースを設定します。

   1. 左側のパネルから、「**[!UICONTROL API]**」をクリックします。

   1. 外部メディア リソース **[!UICONTROL Catalog > Inventory > Products > External Media]** を選択します。

      ![API リソースの管理統合設定 ](../assets/aem-commerce-integration-api-resources.png){width="600" zoomable="yes"}

1. 「**[!UICONTROL Save]**」をクリックします。

### OAuth 認証情報の生成

統合ページで、Assets統合の「**アクティブ化**」をクリックして、OAuth 認証資格情報を生成します。 Commerce プロジェクトをAssets Rule Engine サービスに登録し、Adobe CommerceとAEM Assetsの間でアセットを管理するための API リクエストを送信するには、これらの資格情報が必要です。

1. 統合ページで、「**[!UICONTROL Activate]**」をクリックして資格情報を生成します。

   ![Assets統合用のCommerce設定のアクティブ化 ](../assets/aem-activate-commerce-integration.png){width="600" zoomable="yes"}

1. API を使用する場合は、コンシューマーキーとアクセストークンの資格情報を保存して、API クライアントで認証を設定します。

   ![API リクエストを認証するための OAuth 資格情報 ](../assets/aem-commerce-integration-credentials.png){width="600" zoomable="yes"}

1. 「**[!UICONTROL Done]**」をクリックします。

>[!NOTE]
>
>また、Adobe Commerce API を使用して認証資格情報を生成することもできます。 このプロセスの詳細と、Adobe Developerの OAuth ベースの認証の詳細については、Adobe Commerce ドキュメントの [OAuth ベースの認証 ](https://developer.adobe.com/commerce/webapi/get-started/authentication/gs-authentication-oauth/) を参照してください。

## 次の手順

- [Commerce管理者からの統合の設定](setup-synchronization.md)
