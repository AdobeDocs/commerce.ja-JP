---
title: ' [!DNL Commerce]  サービスによるプライバシー要求の処理方法'
description: データへのアクセスと削除の要求を [!DNL Commerce] servicesが処理する方法について説明します。
role: Admin, Leader
feature: Security, Compliance
exl-id: 1408ca77-6956-4519-93a6-bc9be9bffeff
TQID: https://experienceleague.adobe.com/KhsveSMPR0tKmNzViEaWWHDu8fWve0GZjwsl2oyvx1k
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b5f00040-57a0-4a6d-a39e-383b1936c2c9
  - id: ba9e5be9-7de1-4f71-a5d2-baead0e425ee
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
subfeature_v2:
  - id: bcbf87e7-9b75-4596-bffe-0f376b4c73a7
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
topic_v2:
  - id: d00e9f03-e50b-4162-b143-0c0817c937c2
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
  - id: f4e6943a-c91a-4134-a2c7-f4f20cfff2f0
source-git-commit: 2362159cd352d812f60838b42ade1e98bab5a0d3
workflow-type: tm+mt
source-wordcount: 598
ht-degree: 1%

---

# [!DNL Commerce] サービスでのプライバシー要求の処理方法

Adobe Experience Platform Privacy Serviceには、顧客データリクエストの管理に役立つRESTful APIとユーザーインターフェイスが用意されています。 Privacy Serviceなら、Adobe Experience Cloud アプリケーションから顧客の個人データにアクセスして削除するリクエストを送信でき、法的および組織のプライバシー規制への自動コンプライアンスを促進できます。

Privacy Serviceとプライバシーリクエストの作成および管理方法について詳しくは、Adobe Experience Platformのドキュメントを参照してください。

* [Privacy Serviceの概要](https://experienceleague.adobe.com/ja/docs/experience-platform/privacy/home)
* [Privacy Service UIでのプライバシージョブの管理](https://experienceleague.adobe.com/ja/docs/experience-platform/privacy/ui/user-guide)

## 個々のデータプライバシー要求の管理

[!DNL Commerce]から消費者データにアクセスして削除する個々のリクエストを送信するには、次の2つの方法があります。

* **Privacy Service UI**&#x200B;を使用します。 ドキュメント [こちら](https://experienceleague.adobe.com/ja/docs/experience-platform/privacy/ui/user-guide#_blank)を参照してください。
* **Privacy Service API**&#x200B;を使用します。 ドキュメント [ここ](https://developer.adobe.com/experience-platform-apis/references/privacy-service/#_blank)およびAPI情報[ここ](https://developer.adobe.com/experience-platform-apis/#_blank)を参照してください。

Privacy Serviceでは、**データアクセス**&#x200B;と&#x200B;**データ削除**&#x200B;の2種類のリクエストをサポートしています。

>[!NOTE]
>
>この記事では、[!DNL Commerce]に対するプライバシーリクエストの作成に焦点を当てています。 [Platform データレイク &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-platform/catalog/privacy)、[&#x200B; リアルタイム顧客プロファイル &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-platform/profile/privacy)または[ID サービス &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-platform/identity/privacy)に対してプライバシー要求を行う予定がある場合は、それぞれのユーザーガイドを参照してください。 Commerceへのプライバシーリクエストは、これらのシステムのデータすべてを削除するものではないため、各システムに対して個別に削除およびアクセスのリクエストを行う必要があります。

## データアクセス

**アクセス要求**&#x200B;に対して、UIから「Commerce （Personalization）」を指定します（または`commerceMarketingData`をAPIの製品コードとして指定します）。

## データ削除

削除要求の場合、Privacy Serviceはマーケティング目的でCommerce SaaS サービスに保存されている[!DNL Commerce]個のデータを削除します。つまり、データ主体のプロファイルと注文は、キャンペーンやカスタマージャーニーで使用するためにAdobe マーケティングアプリケーションに送信されなくなります。 ただし、Privacy Serviceは、マーチャントのトランザクションニーズに必要な場合があるため、[!DNL Commerce] アプリケーションのデータを削除しません。 加盟店は、[!DNL Commerce] アプリケーション内のデータ削除/アクセス要求に対して責任を負います。 詳しくは、[責任セキュリティと運用モデルの共有](https://experienceleague.adobe.com/ja/docs/commerce-operations/security-and-compliance/shared-responsibility)を参照してください。

[!DNL Commerce]は、特定のデータの削除を要求するデータ主体の情報を送信することで、削除リクエストについて販売者に通知します。

## アクセス要求と削除要求の作成方法

### 前提条件

Adobe [!DNL Commerce]のデータへのアクセスと削除をリクエストするには、次の条件が必要です。

* ims組織ID
* アクションを実行するユーザーと対応する名前空間のID。 Adobe [!DNL Commerce]およびExperience PlatformのID名前空間について詳しくは、[ID名前空間の概要](https://experienceleague.adobe.com/ja/docs/experience-platform/identity/features/namespaces)を参照してください。

### GDPR要求/削除アクセスの例：

**アクセスリクエスト**&#x200B;に対して、UIから「Commerce （Personalization）」（またはAPIの商品コードとして「commerceMarketingData」）を指定します。

**削除要求**&#x200B;の場合は、「Commerce（Personalization）」チェックボックスが有効になっていることを確認します。 さらに、顧客プロファイルと注文データが既に[!DNL Commerce]からAdobe Experience Platformに送信されている場合は、次のダウンストリームサービスに削除リクエストを送信する必要があります。

* プロファイル （製品コード：&quot;profileService&quot;）
* AEP Data Lake （製品コード：「AdobeCloudPlatform」）
* ID （製品コード：「ID」）

Privacy APIを介してアクセス要求と削除要求を送信するには、Privacy Serviceの権限を認証および管理する必要があります。

* [Privacy Service APIの認証とアクセス](https://experienceleague.adobe.com/ja/docs/experience-platform/privacy/api/getting-started)
* [Privacy Serviceの権限の管理](https://experienceleague.adobe.com/ja/docs/experience-platform/privacy/permissions)

**必須ヘッダー**

```bash
curl --location --request POST 'https://platform.adobe.io/data/core/privacy/jobs' \
--header 'Content-Type: application/json' \
--header 'x-api-key: {{CLIENT_ID}}' \
--header 'x-gw-ims-org-id: {{IMS_ORGID}}' \
--header 'Authorization: Bearer {{ACCESS_TOKEN}}' \
```

**リクエスト**

```json
{
    "companyContexts": [
      {
        "namespace": "imsOrgID",
        "value": "{{IMS_ORGID}}"
      }
    ],
    "users": [
      {
        "key": "sampleUserKey1",
        "action": ["access"],
        "userIDs": [
          {
            "namespace": "email",
            "value": "dsmith@sample.com",
            "type": "standard"
          }
        ]
      },
      {
        "key": "sampleUserKey2",
        "action": ["access","delete"],
        "userIDs": [
          {
            "namespace": "email",
            "value": "ajones@sample.com",
            "type": "standard"
          }
        ]
      }
    ],
    "include": ["commerceMarketingData"],
    "expandIds": false,
    "priority": "normal",
    "regulation": "gdpr"
}
```

**応答**

```json
{
    "requestId": "17284033173196154RX-223",
    "totalRecords": 3,
    "jobs": [
        {
            "jobId": "a52ca032-858e-11ef-bbb4-27391388a0a6",
            "customer": {
                "user": {
                    "key": "sampleUserKey1",
                    "action": [
                        "access"
                    ],
                    "userIDs": [
                        {
                            "namespace": "email",
                            "value": "dsmith@sample.com",
                            "type": "standard",
                            "namespaceId": 6,
                            "isDeletedClientSide": false
                        }
                    ]
                }
            }
        },
        {
            "jobId": "a52ca034-858e-11ef-bbb4-d5d952d69769",
            "customer": {
                "user": {
                    "key": "sampleUserKey2",
                    "action": [
                        "delete"
                    ],
                    "userIDs": [
                        {
                            "namespace": "email",
                            "value": "ajones@sample.com",
                            "type": "standard",
                            "namespaceId": 6,
                            "isDeletedClientSide": false
                        }
                    ]
                }
            }
        },
        {
            "jobId": "a52ca033-858e-11ef-bbb4-8361a5022341",
            "customer": {
                "user": {
                    "key": "sampleUserKey2",
                    "action": [
                        "access"
                    ],
                    "userIDs": [
                        {
                            "namespace": "email",
                            "value": "ajones@sample.com",
                            "type": "standard",
                            "namespaceId": 6,
                            "isDeletedClientSide": false
                        }
                    ]
                }
            }
        }
    ]
}
```
