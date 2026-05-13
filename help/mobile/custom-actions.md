---
title: Custom Actions
feature: Mobile Marketing
description: Learn to send and report custom actions with the Marketo Mobile SDK for iOS and Android, queue offline, trigger Smart Campaigns, and meet the 20-character…
exl-id: 8c2698ce-4e39-4b2b-9d36-0864c55be17a
TQID: https://experienceleague.adobe.com/yZKzdm-dH0cYPGGKE-Z-4KcbhGIwyFl0Z9vEqcv1QXI
product_v2:
  - id: b27e5950-9033-45ac-9f86-eb22e567f615
    internal-label: Marketo Engage
feature_v2:
  - id: a7170d27-32ab-462b-a333-269abc654483
    internal-label: Smart Campaigns
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
    internal-label: Metadata
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
    internal-label: Troubleshooting
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
    internal-label: Security
---
# Custom Actions

You can track user interaction by sending custom actions. When your mobile app calls into the Marketo SDK to send a custom action, the custom action is initially saved to the device. The Marketo SDK then checks to see if there is adequate internet connectivity before sending out the custom action. As a result, there can be a delay between the time the custom action is sent, and the time it is received by Marketo.

Custom actions can be used as triggers and filters in Smart Campaigns. For more information, see [Mobile App Activity](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/core-marketo-concepts/smart-campaigns/flow-actions/triggers-and-filters-for-mobile-smart-campaigns).

## Sending Custom Actions on iOS

Send custom action.

>[!BEGINTABS]

>[!TAB Objective C]

```objectivec
Marketo *sharedInstance = [Marketo sharedInstance];
[sharedInstance reportAction:@"Login" withMetaData:nil];
```

>[!TAB Swift]

```swift
sharedInstance.reportAction("Login", withMetaData:nil);
```

>[!ENDTABS]

Send custom action with metadata.

>[!BEGINTABS]

>[!TAB Objective C]

```objectivec
MarketoActionMetaData *meta = [[MarketoActionMetaData alloc] init];
[meta setType:@"Shopping"];
[meta setDetails:@"RedShirt"];
[meta setLength:20];
[meta setMetric:30];

[sharedInstance reportAction:@"Bought Shirt" withMetaData:meta];
```

>[!TAB Swift]

```swift
let meta = MarketoActionMetaData()
meta.setType("Shopping");
meta.setDetails("RedShirt");
meta.setLength(20);
meta.setMetric(30);

sharedInstance.reportAction("Bought Shirt", withMetaData:meta);
```

>[!ENDTABS]

Report all actions immediately (send all saved actions).

>[!BEGINTABS]

>[!TAB Objective C]

```objectivec
[sharedInstance reportAll];
```

>[!TAB Swift]

```swift
sharedInstance.reportAll();
```

>[!ENDTABS]

## Sending Custom Actions on Android

1. Send custom action.

    ```
    Marketo.reportAction("Login", null);
    ```

1. Send custom action with metadata.

    ```
    MarketoActionMetaData meta = new MarketoActionMetaData();
    meta.setActionType("Shopping");
    meta.setActionDetails("RedShirt");
    meta.setActionLength("20");
    meta.setActionMetric("30");

    Marketo.reportAction("Bought Shirt", meta);
    ```

1. Report all custom actions immediately (send all saved actions).

    ```
    Marketo.reportAll();
    ```

## Troubleshooting Custom Actions

Setting up mobile custom actions is straightforward, but there are restrictions as to the number characters you can send from the Mobile SDK to Marketo. Ensure that all of your custom actions that report back to Marketo through the mobile SDK are fewer than 20 characters long.

**Note on multi-user use cases on a shared device:** When a user logs into a mobile app integrated with Marketo SDK, the first call is made to associate the lead with the app install. After this call successfully completes, further user activities in the app can be seen in the lead's activity log. Note, as this is an asynchronous call if there are any custom actions logged immediately after login they may get associated with the user that was previously logged in until the associate call succeeds.
