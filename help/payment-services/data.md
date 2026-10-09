---
title: 利用可能なデータ
description: 財務報告データを使用して、レポートとCommerce以外のシステムを連携させる。
role: User
level: Intermediate
exl-id: dbf41ce9-01f9-45d0-b651-e4c499e83822
feature: Payments, Checkout, Data Import/Export, Paas, Saas
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 3dcbfa9e-51f8-569c-a0e4-7f59098f730f
    internal-label: Payments
  - id: 8cd50456-5eb0-5364-922a-f14161feb828
    internal-label: Checkout
  - id: 601e4abe-d9bf-58de-a779-32ed6794dcbe
    internal-label: Data Import/Export
  - id: 00451af3-7b97-5414-9992-3a6c269e413f
    internal-label: Paas
  - id: d3b92bef-63fa-5031-a925-d04d9362d616
    internal-label: Saas
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
source-git-commit: 76e77db86adecdbd3be76040970c0d0899c34cdc
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 0%
---
# 利用可能なデータ

一部の注文データと支払いデータを使用して、外部システム間でAdobe Commerce financial reportingを調整できます。

## ERPとの連携

特定の注文に関連付けられた増分IDを使用して、Adobe Commerce財務報告をAdobe以外のERP （エンタープライズリソースプランニング）システムと照合できます。

Payment ServicesがCommerce注文をPayPalに送信すると、増分IDは`custom_id` _および_&#x200B;として`invoice_id`に含まれます（これには`increment_id`の後のランダムな文字列も含まれます）。

IDは、支払いの加盟店アクティビティの詳細とPayPalのWebhookの両方から簡単にアクセスできます。

`invoice_id`と`custom_id`は、支払いの加盟店アクティビティの詳細の下部に表示されます。

加盟店アクティビティの詳細![&#128279;](assets/merchant-activity-ids.png){width="600" zoomable="yes"}の`custom_id`

PayPalのWebhookの詳細の`custom_id`と`invoice_id`:

```json
   ...
   {
    "id": "4E855005GK253170H",
    "intent": "AUTHORIZE",
    "status": "COMPLETED",
    "payment_source": {
        ...
    },
    "purchase_units": [
        {
            ...
            "custom_id": "000001322",
            "invoice_id": "000001322-c01bd7c3-920f-4542-a900-738082177e92",
            ...
            "payments": {
                "authorizations": [
                    {
                       ...
                        "invoice_id": "000001322-c01bd7c3-920f-4542-a900-738082177e92",
                        "custom_id": "000001322",
                        ...
                    }
                ],
                "captures": [
                    {
                        ...
                        "invoice_id": "000001322-c01bd7c3-920f-4542-a900-738082177e92",
                        "custom_id": "000001322",
                        ...
                    }
                ]
            }
        }
    ],
    "payer": {
        ...
    },
    "create_time": "2022-09-12T14:59:01Z",
    "update_time": "2022-09-12T14:59:45Z",
    "links": [
        ...
    ]
}
   ...
```

詳しくは、PayPalのREST API ドキュメントを参照してください。

* [`purchase_unit` （`custom_id`および`invoice_id`が格納）](https://developer.paypal.com/docs/api/orders/v2/#definition-purchase_unit)
* [注文の詳細を表示](https://developer.paypal.com/docs/api/orders/v2/#orders_get)
