---
title: 使用可能なデータ
description: Financial reporting データを使用して、レポートをCommerce以外のシステムと調整します。
role: User
level: Intermediate
exl-id: dbf41ce9-01f9-45d0-b651-e4c499e83822
feature: Payments, Checkout, Data Import/Export, Paas, Saas
source-git-commit: 5271668c99e7a66fbe857cd3ae26edfa54211621
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 0%

---

# 使用可能なデータ

一部の注文および支払いデータは、外部システム間でAdobe Commerceの財務レポートを調整できるように使用できます。

## ERP システムとの調整

特定の注文に関連付けられた増分 ID を使用して、Adobe Commerceの財務レポートをAdobe以外の Enterprise Resource Planning （ERP）システムと紐付けることができます。

支払いサービスがCommerceの注文を PayPal に送信すると、増分 ID が `custom_id` _および_ として `invoice_id` に含まれます（`increment_id` の後にランダムな文字列も含まれます）。

ID には、支払いのマーチャントアクティビティの詳細と PayPal Webhook の両方で簡単にアクセスできます。

`invoice_id` と `custom_id` は、支払いに関するマーチャントアクティビティの詳細の下部付近に表示されます。

マーチャントアクティビティの詳細で ![`custom_id` 明する &#x200B;](assets/merchant-activity-ids.png){width="600" zoomable="yes"}

PayPal の Webhook の詳細で `custom_id` と `invoice_id` を参照してください。

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

詳しくは、PayPal の REST API ドキュメントを参照してください。

* `custom_id` と `invoice_id` が存在する [`purchase_unit`](https://developer.paypal.com/docs/api/orders/v2/#definition-purchase_unit)
* [&#x200B; 注文の詳細を表示 &#x200B;](https://developer.paypal.com/docs/api/orders/v2/#orders_get)
