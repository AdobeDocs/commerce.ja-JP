---
title: IDとアクセス管理
description: Adobe Commerce as a Cloud ServiceのIDおよびアクセス管理機能について説明します。
role: Admin, Developer, Leader
badgeSaas: label="SaaSのみ" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud ServiceおよびAdobe Commerce Optimizer プロジェクト（Adobeが管理するSaaS インフラストラクチャ）にのみ適用されます。"
source-git-commit: feb48068137c6a63e6594167fe969c3aa4b044c4
workflow-type: tm+mt
source-wordcount: '419'
ht-degree: 0%

---


# IDとアクセス管理

[!DNL Adobe Commerce as a Cloud Service]は、Adobeのエンタープライズ向けID インフラストラクチャを活用して、すべての環境で安全でスケーラブルかつ一元化されたアクセス制御を実現します。 [!DNL Adobe Commerce as a Cloud Service]のIDとアクセス管理（IAM）は、ユーザープロビジョニングを簡素化し、最小権限アクセスを適用し、グローバル セキュリティ標準への準拠をサポートするように設計されています。

- **[!DNL Adobe Identity Management Services (IMS)]**: [!DNL Adobe Commerce as a Cloud Service]は、[Adobe Identity Management サービス （IMS） &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-admin/start/admin/ims/adobe-ims-integration-overview)を使用して、ユーザーの認証と使用権限の管理を行います。 これには、フェデレーション ID プロバイダーと[役割ベースのアクセス制御](../user-management.md)のサポートが含まれます。

- **管理コンソールのガバナンス**：管理者は、[!DNL Adobe Admin Console]を通じてストアフロントとバックエンドへのアクセスを管理します。 権限は特定の機能や役割に限定でき、最小権限のアクセスが保証されます。

## Adobe Identity Management Services （IMS）

[!DNL Adobe Commerce as a Cloud Service]は[!DNL Adobe Identity Management Services (IMS)]を使用して、プラットフォーム全体でユーザーを認証し、使用権限を管理します。 IMSの提供：

- **フェデレーション ID サポート**: SAMLまたはOIDCを使用して、Azure ADやOktaなどのエンタープライズ ID プロバイダーと統合します。
- **シングルサインオン （SSO）**: [!DNL Adobe Commerce]およびその他[!DNL Adobe Experience Cloud]製品へのシームレスなアクセス。
- **多要素認証（MFA）**：セキュリティを強化するために、組織レベルで適用されます。
- **グローバル冗長性**:ID データは、複数の地域で負荷分散されたクラウド インフラストラクチャに保存されます。

## Admin Console アクセス制御

[!DNL Adobe Admin Console]は、[!DNL Adobe Commerce as a Cloud Service]へのユーザーアクセスを管理するための中央ハブです：

- **役割ベースのアクセス制御（RBAC）**：開発者、管理者、アナリストなどの役割に基づいて、詳細な権限をユーザーに割り当てます。
- **製品プロファイル**: ステージングや実稼動環境など、様々な環境のアクセス範囲を定義します。
- **委任された管理**: システム管理者と製品管理者は、IT部門の関与がなくてもユーザーアクセスを管理できます。

詳しくは、[&#x200B; ユーザー管理](https://experienceleague.adobe.com/en/docs/commerce/cloud-service/user-management)を参照してください。

## API認証と統合のセキュリティ

[!DNL Adobe Commerce as a Cloud Service]のREST API認証は、標準化されたOAuth 2 プロトコルを使用してAdobeの[!DNL Adobe Identity Management Services (IMS)]を通じて処理されます。 この認証システムは、インタラクティブなユーザーベースのワークフローと、サーバー間の自動化された統合の両方をサポートし、様々なユースケースに対する安全で適切なアクセスを保証します。

>[!NOTE]
>
>SaaS環境では、PaaS バージョン [!DNL Adobe Commerce]の管理および統合トークン生成メソッドはサポートされていません。 代わりに、OAuth認証を通じてIMS管理トークンを取得する必要があります。

- **OAuth 2.0のサポート**：統合とサードパーティサービスに対するトークンベースの安全な認証。
- **スコープ付きAPI アクセス**：特定のリソースと操作へのAPI アクセスを制限します。
- **監査ログ**：認証イベントを追跡し、コンプライアンスとトラブルシューティングのために変更にアクセスします。

詳しくは、[REST認証](https://developer.adobe.com/commerce/webapi/rest/authentication/)を参照してください。
