---
title: 移行サービスへのアクセスの確認
description: Commerce Data Migration Service APIへのエンドツーエンドのアクセスを検証し、ネットワークへの到達性、IMS認証、テナント認証を確認する方法について説明します。
feature: Cloud
badgeSaas: label="SaaSのみ" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Adobe Commerce as a Cloud ServiceおよびAdobe Commerce Optimizer プロジェクト（Adobeが管理するSaaS インフラストラクチャ）にのみ適用されます。"
role: Developer
level: Intermediate
autotag-review: '2026-07-22T19:18:53.554Z'
TQID: 'https://experienceleague.adobe.com/csDq2Bbha2IieqxsDDG0iS1IHhAJ02fD-cwd8KFIsSk'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
  - id: f08fa0de-a550-4acd-b570-f81cf1d03aaf
subfeature_v2:
  - id: f8ddfd3b-6194-46e8-a176-0e918039be56
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2:
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: 670b6214b28be93a16130552a226a8cadb487324
workflow-type: tm+mt
source-wordcount: 452
ht-degree: 1%

---

# 移行サービスへのアクセスの確認

{{bulk-data-early-access}}

このガイドでは、Commerce Data Migration Service （CDMS） APIへのエンドツーエンドのアクセスを確認する方法を説明します。 呼び出しが成功すると、エグレス IP （IP 許可リストに加える）、IMS認証、およびテナント認証からのネットワーク到達可能性が同時に検証されます。

このガイドは、[顧客対応チェックリスト &#x200B;](readiness-checklist.md)のすべての項目を完了した後、[移行ガイド &#x200B;](migration-guide.md)で説明されている移行を実行する前に完了してください。

## 前提条件

- [Adobe Developer Console](https://developer.adobe.com/console/)で作成されたOAuth 2.0 サーバー間の資格情報（クライアント IDおよびクライアント秘密鍵）。
- IMS組織ID （形式：`<org>@AdobeOrg`）。 組織がターゲットテナントを所有している必要があります。
- ターゲット `tenantId`、22文字、英数字のIMS テナント ID。
- CDMS ゲートウェイ用にAdobeに送信および許可リストに加えるされたアウトバウンドエグレス IP アドレス。 IP アドレスやそのステータスがわからない場合は、Adobeチームと調整してください。
- 環境および地域[&#128279;](#service-hosts-by-environment-and-region) テーブル別のService ホストからの地域固有のサービス ホスト。

## IMS アクセストークンの生成

`client_credentials`付与を使用して、OAuth 2.0 サーバー間の資格情報を使用してアクセストークンを生成します。 このステップのIMS ホストは、すべてのデータ領域で同じです。 CDMS ホストのみが領域ごとに変更されます。

```bash
curl -X POST "https://ims-na1.adobelogin.com/ims/token/v3" \
  -H "Content-Type: application/x-www-form-urlencoded" \
  -H "x-org-id:<your-org-id>@AdobeOrg" \
  -d "grant_type=client_credentials" \
  -d "client_id=<your-ims-client-id>" \
  -d "client_secret=<your-ims-client-secret>" \
  -d "scope=AdobeID,openid,read_organizations,additional_info.projectedProductContext,additional_info.roles,adobeio_api,read_client_secret,manage_client_secrets"
```

## List Migrations APIの呼び出し

次のリクエストは、テナントの移行のリストを取得し、前の手順のアクセストークンを必要とします。 環境および地域[&#128279;](#service-hosts-by-environment-and-region) テーブルのService ホストから、地域のホストを選択します。 `-i` フラグは、結果を確認できるように、HTTP ステータス行と応答ヘッダーを印刷します。

```bash
curl -i "https://<host>/<tenantId>/v1/migrations" \
  -H "Authorization: Bearer <your IMS access token>"
```

## 応答の解釈

| HTTP コード | 意味 | 応答本文の例 |
| --- | --- | --- |
| 200 | 成功： 接続、認証、テナント認証はすべて合格しました。 応答本文には、テナントの移行のリストが含まれます。 | `{"migrations":[...]}` |
| 401 | ベアラートークンが見つからないか無効です。サービスに到達する前に拒否されました。 [&#x200B; トークンを再生成](#generate-an-ims-access-token)。 | Varies （ゲートウェイ生成） |
| 403 | 認証済みユーザーには、このテナントの移行権限がありません。 | `{"error":"access_denied","message":"You do not have permission to access this tenant"}` |
| 500 | 内部サーバーエラー。 | `{"error":{"message":"Internal Server Error","status":500}}` |

>[!NOTE]
>
>リクエストがタイムアウトするか、接続が拒否され、HTTP ステータスが返されない場合は、エグレス IPが許可リストに加えるされない可能性が高い場合や、誤ったホストを使用している場合があります。 次の表のリージョンホストと許可リストに加えるしたIPを確認します。

## 環境および地域別のサービスホスト

| 地域または環境 | ホスト |
| --- | --- |
| サンドボックスまたはプリプロダクション | `https://na1-sandbox.api.commerce.adobe.com` |
| 北米 | `https://na1.api.commerce.adobe.com` |
| ヨーロッパ | `https://eu1.api.commerce.adobe.com` |
| インド | `https://in1.api.commerce.adobe.com` |
| UK | `https://uk1.api.commerce.adobe.com` |
| オーストラリアおよびニュージーランド | `https://au1.api.commerce.adobe.com` |

## 次のステップ

アクセスを確認したら、[移行ガイド &#x200B;](migration-guide.md)に進み、環境設定と移行の実行を開始します。
