---
title: ' [!DNL Commerce] Services によるプライバシーリクエストの処理方法'
description: データへのアクセス要求  [!DNL Commerce]  データの削除要求をサービスが処理する方法を説明します。
role: Admin, Leader
feature: Security, Compliance
exl-id: 1408ca77-6956-4519-93a6-bc9be9bffeff
source-git-commit: c6725fc524e9d239ccc0f16701e92ad5d2fc7729
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 0%

---

# プライバシーリクエスト

Adobe Experience Platform Privacy Serviceは、カスタマーデータのリクエストの管理に役立つ RESTful API とユーザーインターフェイスを提供します。 Privacy Serviceを使用すると、Adobe Experience Cloud アプリケーションから個人の顧客データへのアクセスおよび削除リクエストを送信でき、法的および組織のプライバシー規制への自動コンプライアンスが容易になります。

Privacy Serviceと、プライバシーリクエストを作成および管理する方法について詳しくは、次のAdobe Experience Platform ドキュメントを参照してください。

* [Privacy Serviceの概要 &#x200B;](https://experienceleague.adobe.com/en/docs/experience-platform/privacy/home)
* [Privacy Service UI でのプライバシージョブの管理 &#x200B;](https://experienceleague.adobe.com/en/docs/experience-platform/privacy/ui/user-guide)

## 個々のデータプライバシーリクエストの管理

個々のリクエストを送信して、[!DNL Commerce] から消費者データにアクセスしたり削除したりするには、次の 2 つの方法があります。

* **Privacy Service UI** を使用する。 ドキュメント [&#x200B; こちら &#x200B;](https://experienceleague.adobe.com/en/docs/experience-platform/privacy/ui/user-guide#_blank) を参照してください。
* **Privacy Service API** を使用する。 ドキュメント [&#x200B; こちら &#x200B;](https://developer.adobe.com/experience-platform-apis/references/privacy-service/#_blank) および API 情報 [&#x200B; こちら &#x200B;](https://developer.adobe.com/experience-platform-apis/#_blank) を参照してください。

Privacy Serviceでは、**データアクセス** と **データ削除** の 2 種類のリクエストがサポートされています。

>[!NOTE]
>
>この記事では、[!DNL Commerce] に対するプライバシーリクエストの実行に焦点を当てます。 [Platform Data Lake](https://experienceleague.adobe.com/en/docs/experience-platform/catalog/privacy)、[&#x200B; リアルタイム顧客プロファイル &#x200B;](https://experienceleague.adobe.com/en/docs/experience-platform/profile/privacy) または [ID サービス &#x200B;](https://experienceleague.adobe.com/en/docs/experience-platform/identity/privacy) のプライバシーリクエストを行う予定がある場合は、それぞれのユーザーガイドを参照してください。 Commerceに対するプライバシーリクエストでは、これらのすべてのシステムからデータが削除されないので、削除リクエストとアクセスリクエストは、各システムに対して個別に行う必要があります。

## データアクセス

**アクセスリクエスト** については、UI から「Commerce （Personalization）」を指定します（または、API のプロダクトコードとして `commerceMarketingData` 定します）。

## データ削除

削除要求の場合、Privacy Serviceは、マーケティング目的 [!DNL Commerce]Commerce SaaS サービスに保存されているデータを削除します。つまり、データ主体のプロファイルと注文は、キャンペーンやカスタマージャーニーで使用するためにAdobe マーケティングアプリケーションに送信されなくなります。 ただし、マーチャントトランザクションのニーズに必要な可能性があるので、Privacy Serviceは [!DNL Commerce] アプリケーション内のデータを削除しません。 マーチャントは、[!DNL Commerce] アプリケーション内のすべてのデータ削除/アクセスリクエストに対して責任を負います。 詳しくは、[&#x200B; 共有責任のセキュリティと運用モデル &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-operations/security-and-compliance/shared-responsibility) を参照してください。

[!DNL Commerce] は、特定のデータの削除をリクエストするデータ主体の情報を送信することで、削除要求についてマーチャントに通知します。

## アクセスリクエストと削除リクエストの作成方法

### 前提条件

Adobe [!DNL Commerce] のデータへのアクセスおよび削除をリクエストするには、次の情報が必要です。

* ims 組織 ID
* 操作の対象となるユーザーの ID 識別子と、対応する名前空間。 Adobe [!DNL Commerce] およびExperience Platformの ID 名前空間について詳しくは、[ID 名前空間の概要 &#x200B;](https://experienceleague.adobe.com/ja/docs/experience-platform/identity/features/namespaces) を参照してください。

### GDPR リクエスト/削除アクセスの例：

**アクセスリクエスト** については、UI から「Commerce （Personalization）」を指定します（または、API の商品コードとして「commerceMarketingData」を指定します）。

**削除リクエスト** については、「Commerce （Personalization）」チェックボックスが有効になっていることを確認します。 さらに、顧客プロファイルと注文データが既に [!DNL Commerce] からAdobe Experience Platformに送信されている場合は、次のダウンストリームサービスに削除リクエストを送信する必要があります。

* プロファイル（製品コード：「profileService」）
* AEP Data Lake （製品コード：「AdobeCloudPlatform」）
* ID （製品コード：「ID」）

プライバシー API を使用してアクセスリクエストと削除リクエストを送信するには、Privacy Serviceに対する権限を認証および管理する必要があります。

* [Privacy Service API の認証とアクセス &#x200B;](https://experienceleague.adobe.com/en/docs/experience-platform/privacy/api/getting-started)
* [Privacy Serviceの権限の管理 &#x200B;](https://experienceleague.adobe.com/en/docs/experience-platform/privacy/permissions)

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
