---
title: プロファイルへのカスタム属性の追加
description: 顧客プロファイルにカスタム属性を追加する方法を説明します。
role: Admin, Developer
feature: Personalization, Integration
source-git-commit: 5489910382edc70eea5d7c0ca94da41c653b577d
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 0%

---


# プロファイルへのカスタム属性の追加

カスタムプロファイル属性を使用すると、デフォルトの `customerId` や `emailId` 以外の識別子を使用して、Experience Platformで顧客プロファイルの ID を強化できます。 これらの識別子を追加することで、より正確な顧客マッチングが可能になり、Commerce プラットフォームとExperience Platformの間のデータ統合が向上します。

>[!NOTE]
>
>注文に [ カスタム属性を追加 ](custom-attributes.md) する方法を説明します。

## 利点

- 複数の識別子を使用して、顧客とのマッチングを改善します。
- ビジネスニーズに基づいて、カスタムフィールドを ID 属性にマッピングします。
- 重複プロファイルを減らし、顧客データの精度を向上させます。
- よりターゲットを絞った顧客体験を可能にします。

## 前提条件

カスタム ID 属性を実装する前に、次のことを確認します。

- [データ接続拡張機能のインストール](install.md)
- [Adobe Experience Platformへの接続](connect-data.md)
- [顧客プロファイルデータの送信](connect-data.md#send-customer-profile-data)

## 手順 1:Experience Platform スキーマを設定する

1. Adobe Experience Platformにログインし、Commerce スキーマを選択します。
1. ルートレベルで [ カスタム ID フィールドを追加 ](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/ui/resources/schemas?lang=en#custom-fields-for-standard-groups) します。
   - `hashedPID` （String） - プライマリ ID ハッシュ
   - `hashedSID` （String） -セカンダリID ハッシュ
   - `primaryID` （String） -プライマリID フィールド名
   - `secondaryID` （String） -セカンダリID フィールド名

![Experience Platform スキーマの設定 ](./assets/aep-schema-configuration.png)

>[!NOTE]
>
>必要に応じて、正確なフィールド名をカスタマイズできます。 この例では、`hashedPID` および `hashedSID` を ID フィールドとして使用します。

## 手順 2：プロセッサクラスの作成

次の PHP プロセッサクラスをカスタムモジュールに作成します。

### AddressCustomHashedId クラス

このプロセッサーは、顧客アドレス用に `parent_id` と `entity_id` をハッシュ化します。

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

このプロセッサは、アドレスイベントのプライマリ ID フィールド名とセカンダリ ID フィールド名を設定します。

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

このプロセッサーは、顧客プロファイルの `entity_id` および `email` をハッシュ化します。

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

このプロセッサは、プロファイルイベントのプライマリ ID フィールド名とセカンダリ ID フィールド名を設定します。

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
>`primaryID` と `secondaryID` の両方がイベントデータで送信されていることを確認します。 いずれかが見つからない場合、Commerceのデフォルトでは次のようになります。
>
>- primaryID = customerId
>- secondaryID = emailId

>[!BEGINSHADEBOX]

次の 2 つの手順を完了した後：

- Experience PlatformのCommerce スキーマは、プロファイルイベントデータのカスタム ID を適切に取り込むことができます。
- Commerce PHP コード内のプロセッサクラスは、プロファイルイベントからカスタム ID 情報を収集します。

これで、Commerceから送信されるプロファイルイベントデータに、カスタム ID 情報が含まれるようになりました。

>[!ENDSHADEBOX]

## データ形式の例

次の例は、プロファイル属性と完全な顧客プロファイルデータ形式の両方でカスタム ID 属性に対して期待される JSON 構造を示しています。

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

### 完全な顧客プロファイル構造

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

### プライマリ ID またはセカンダリ ID がありません

- **症状：** データは、デフォルトでカスタム値ではなく customerId/emailId に設定されます。
- **解決策：** `primaryID` と `secondaryID` の両方が `profileAttributes` オブジェクトに設定されていることを確認します。

### 無効なハッシュ値

- **症状：** ハッシュ値が空か、形式が正しくありません。
- **解決策：** ハッシュ化する前に、ソースフィールド（`parent_id`、`entity_id`、`email`）に有効なデータが含まれていることを確認してください。

### プロセッサが実行されていません

- **症状：** カスタム属性がイベントデータに表示されない。
- **解決策：** プロセッサが `events.xml` に正しく登録され、モジュールが有効になっていることを確認してください。

### Experience Platform スキーマの不一致

- **症状：** Experience Platformまたはスキーマ検証エラーで、データが表示されない。
- **解決策：** Experience Platform スキーマに、正しいデータタイプを持つカスタム ID フィールドが含まれていることを確認してください。
