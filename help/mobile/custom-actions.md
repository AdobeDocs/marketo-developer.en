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

Custom actions track user interactions in your mobile app. When the app calls the Marketo SDK to send a custom action, the SDK first saves the action to the device. The SDK sends the action after it detects adequate internet connectivity, so Marketo might receive the action after a delay.

Custom actions can be used as triggers and filters in Smart Campaigns. For more information, see [Mobile App Activity](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/core-marketo-concepts/smart-campaigns/flow-actions/triggers-and-filters-for-mobile-smart-campaigns).

## Sending Custom Actions on iOS

Send a custom action.

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

Send a custom action with metadata.

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

Report all saved actions immediately.

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

1. Send a custom action.

    ```
    Marketo.reportAction("Login", null);
    ```

1. Send a custom action with metadata.

    ```
    MarketoActionMetaData meta = new MarketoActionMetaData();
    meta.setActionType("Shopping");
    meta.setActionDetails("RedShirt");
    meta.setActionLength("20");
    meta.setActionMetric("30");

    Marketo.reportAction("Bought Shirt", meta);
    ```

1. Report all saved custom actions immediately.

    ```
    Marketo.reportAll();
    ```

## Troubleshooting Custom Actions

Custom action names sent from the Mobile SDK to Marketo must be fewer than 20 characters.

**Multi-user use cases on a shared device:** When a user logs in to a mobile app that uses the Marketo SDK, the first call associates the lead with the app installation. After the call succeeds, subsequent user activities appear in the lead's activity log.

The association call is asynchronous. Custom actions logged immediately after login might be associated with the previously logged-in user until the call succeeds.
