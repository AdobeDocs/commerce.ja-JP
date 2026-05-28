---
title: プロファイルへのカスタム属性の追加
description: 顧客プロファイルにカスタム属性を追加する方法について説明します。
role: Admin, Developer
feature: Personalization, Integration
exl-id: ad786572-9158-429a-b4dd-5f15efc0f624
TQID: https://experienceleague.adobe.com/yCA2EjsIzzx7AEOQubLMW4Ib3v8Bbad1Wsq3RsgvCXM
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: c1256247-af4b-46d8-9dca-0c654ecfa157id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: bce87dde-a4ab-44c9-8a18-ad66e4ddb377id: c1579802-ddd4-4214-8a91-97b2066abe11id: df401a2a-327d-468c-a5e4-b7b7ccd071a0id: e0eb8757-182f-49f3-94a4-1587d16f5094id: fd2e3797-f2ea-4b36-a9af-52acf5e90513
source-git-commit: 33cd0e217447351b690646ec8d230f76060a74da
workflow-type: tm+mt
source-wordcount: 473
ht-degree: 0%

---

# プロファイルへのカスタム属性の追加

カスタムプロファイル属性を使用すると、デフォルトの`customerId`および`emailId`以外のIDを使用して、Experience Platformでの顧客プロファイルのIDを強化できます。 これらのIDを追加することで、より正確なカスタマーマッチングと、CommerceプラットフォームとExperience Platform間のデータ統合の向上が可能になります。

>[!NOTE]
>
>注文にカスタム属性](custom-attributes.md)を[追加する方法について説明します。

## Adobe Workfrontの利点

- 複数のIDを使用して顧客とのマッチングを向上。
- ビジネスニーズにもとづいて、カスタムフィールドをID属性にマッピングできます。
- 重複するプロファイルを減らし、顧客データの精度を向上させます。
- 的を絞った顧客体験を実現。

## 前提条件

カスタム ID属性を実装する前に、次のことを確認してください。

- [Data Connection拡張機能のインストール](install.md)
- [Adobe Experience Platformに接続](connect-data.md)
- [顧客プロファイルデータの送信](connect-data.md#send-customer-profile-data)

## 手順1:Experience Platform スキーマの設定

1. Adobe Experience Platformにログインし、Commerce スキーマを選択します。
1. [ ルートレベルでカスタム ID フィールド ](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/ui/resources/schemas?lang=en#custom-fields-for-standard-groups)を追加：
   - `hashedPID` （文字列） - プライマリ ID ハッシュ
   - `hashedSID` （文字列） -セカンダリID ハッシュ
   - `primaryID` （文字列） - プライマリ ID フィールド名
   - `secondaryID` （文字列） -セカンダリID フィールド名

![Experience Platform Schema Configuration](./assets/aep-schema-configuration.png)

>[!NOTE]
>
>必要に応じて、フィールド名を正確にカスタマイズできます。 この例では、ID フィールドとして`hashedPID`と`hashedSID`を使用しています。

## 手順2：プロセッサクラスの作成

カスタムモジュールに次のPHP プロセッサクラスを作成します。

### AddressCustomHashedId クラス

このプロセッサーは、顧客アドレスに対して`parent_id`と`entity_id`をハッシュします。

```php
<?php declare(strict_types=1);

namespace Magento\AepCustomerCustomAttributes\Event;
use Magento\AdobeCommerceEventsClient\Event\Event;
use Magento\AdobeCommerceEventsClient\Event\Processor\EventDataProcessorInterface;

class AddressCustomHashedId implements EventDataProcessorInterface
{
    public function process(Event $event, array $eventData): array
    {
        $pid = $eventData['parent_id'] ?? '';
        $sid = $eventData['entity_id'] ?? '';

        $eventData['profileAttributes']['hashedPID'] = hash('sha256', (string)$pid);
        $eventData['profileAttributes']['hashedSID'] = hash('sha256', (string)$sid);
        return $eventData;
    }
}
```

### AddressCustomId クラス

このプロセッサーは、アドレスイベントのプライマリ ID フィールド名とセカンダリ ID フィールド名を設定します。

```php
<?php declare(strict_types=1);

namespace Magento\AepCustomerCustomAttributes\Event;
use Magento\AdobeCommerceEventsClient\Event\Event;
use Magento\AdobeCommerceEventsClient\Event\Processor\EventDataProcessorInterface;

class AddressCustomId implements EventDataProcessorInterface
{
    public function process(Event $event, array $eventData): array
    {
        $eventData['profileAttributes']['primaryID'] = 'hashedPID';
        $eventData['profileAttributes']['secondaryID'] = 'hashedSID';

        // Ensure both IDs are present, otherwise, Commerce will default primary to customerId and secondary to emailId
        if (empty($eventData['profileAttributes']['primaryID']) || empty($eventData['profileAttributes']['secondaryID'])) {
            $eventData['profileAttributes']['primaryID'] = $eventData['customerId'] ?? '';
            $eventData['profileAttributes']['secondaryID'] = $eventData['email'] ?? '';
        }

        return $eventData;
    }
}
```

### CustomHashedId クラス

このプロセッサーは、顧客プロファイルに対して`entity_id`と`email`をハッシュします。

```php
<?php declare(strict_types=1);

namespace Magento\AepCustomerCustomAttributes\Event;
use Magento\AdobeCommerceEventsClient\Event\Event;
use Magento\AdobeCommerceEventsClient\Event\Processor\EventDataProcessorInterface;

class CustomHashedId implements EventDataProcessorInterface
{
    public function process(Event $event, array $eventData): array
    {
        $pid = $eventData['entity_id'] ?? '';
        $sid = $eventData['email'] ?? '';

        $eventData['profileAttributes']['hashedPID'] = hash('sha256', (string)$pid);
        $eventData['profileAttributes']['hashedSID'] = hash('sha256', (string)$sid);
        return $eventData;
    }
}
```

### CustomId クラス

このプロセッサーは、プロファイルイベントのプライマリ ID フィールド名とセカンダリ ID フィールド名を設定します。

```php
<?php declare(strict_types=1);

namespace Magento\AepCustomerCustomAttributes\Event;
use Magento\AdobeCommerceEventsClient\Event\Event;
use Magento\AdobeCommerceEventsClient\Event\Processor\EventDataProcessorInterface;

class CustomId implements EventDataProcessorInterface
{
    public function process(Event $event, array $eventData): array
    {
        $eventData['profileAttributes']['primaryID'] = 'hashedPID';
        $eventData['profileAttributes']['secondaryID'] = 'hashedSID';

        // Ensure both IDs are present, otherwise, Commerce will default primary to customerId and secondary to emailId
        if (empty($eventData['profileAttributes']['primaryID']) || empty($eventData['profileAttributes']['secondaryID'])) {
            $eventData['profileAttributes']['primaryID'] = $eventData['customerId'] ?? '';
            $eventData['profileAttributes']['secondaryID'] = $eventData['email'] ?? '';
        }

        return $eventData;
    }
}
```

>[!NOTE]
>`primaryID`と`secondaryID`の両方がイベントデータで送信されていることを確認してください。 いずれかのオプションがない場合、Commerceのデフォルトは次のようになります。
>
>- primaryID = customerId
>- secondaryID = emailId

>[!BEGINSHADEBOX]

次の2つの手順を完了した後：

- Experience PlatformのCommerce スキーマは、プロファイルイベントデータのカスタム IDを適切に取り込むことができます。
- CommerceのPHP コード内のプロセッサークラスは、プロファイルイベントからカスタム ID情報を収集します。

Commerceから送信されるプロファイルイベントデータには、カスタム ID情報が含まれます。

>[!ENDSHADEBOX]

## データ形式の例

次の例では、プロファイル属性と完全な顧客プロファイルデータ形式の両方で、カスタム ID属性に期待されるJSON構造を示します。

### プロファイル属性形式

```json
{
  "profileAttributes": {
    "hashedPID": "d80eae6e96d148b3b2abbbc6760077b66c4ea071f847dab573d507a32c4d99a5",
    "hashedSID": "fa7359e288ce3104bd4317a4fb75f08c4a5feec472de2e415b8260fb3567ebe6",
    "warehousecode": "1256",
    "method": "ina2354",
    "source": "commerce",
    "primaryID": "hashedPID",
    "secondaryID": "hashedSID"
  }
}
```

### 顧客プロファイルの全体構造

```json
{
  "id": 137,
  "entity_id": "137",
  "created_at": "2025-02-10 20:10:30",
  "updated_at": "2022-02-10 20:10:31",
  "email": "customer@example.com",
  "firstname": "John",
  "lastname": "Doe",
  "dob": "2007-10-01 00:00:00",
  "profileAttributes": {
    "hashedPID": "d80eae6e96d148b3b2abbbc6760077b66c4ea071f847dab573d507a32c4d99a5",
    "hashedSID": "fa7359e288ce3104bd4317a4fb75f08c4a5feec472de2e415b8260fb3567ebe6",
    "primaryID": "137",
    "secondaryID": "customer@example.com"
  },
  "_metadata": {
    "commerceEdition": "Adobe Commerce",
    "commerceVersion": "2.4.6",
    "eventsClientVersion": "1.9.0",
    "storeId": "1",
    "websiteId": "1",
    "storeGroupId": "1",
    "websiteCode": "base",
    "storeCode": "default",
    "storeViewCode": "main_website_store"
  }
}
```

## トラブルシューティング

### primaryIDまたはsecondaryIDがありません

- **症状：** データは、カスタム値の代わりにcustomerId/emailIdにデフォルトで設定されます。
- **解決策：** `primaryID`と`secondaryID`の両方が`profileAttributes` オブジェクトに設定されていることを確認します。

### 無効なハッシュ値

- **症状：** ハッシュ値が空であるか、形式が正しくありません。
- **解決策：** ソースフィールド （`parent_id`、`entity_id`、`email`）に有効なデータが含まれていることを確認してからハッシュします。

### プロセッサーが実行されない

- **症状：** カスタム属性がイベントデータに表示されません。
- **解決策：** プロセッサが`events.xml`に正しく登録され、モジュールが有効になっていることを確認してください。

### Experience Platform スキーマの不一致

- **現象：** データがExperience Platformまたはスキーマ検証エラーに表示されません。
- **解決策：** Experience Platform スキーマに、正しいデータタイプを持つカスタム ID フィールドが含まれていることを確認します。
