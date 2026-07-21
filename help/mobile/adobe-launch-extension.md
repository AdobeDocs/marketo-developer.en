---
title: Marketo Mobile Extension for [!DNL Adobe Launch]
feature: Mobile Marketing
description: Install and configure the Marketo Mobile SDK extension in Adobe Launch for iOS and Android, including setup for push notifications and in-app messages.
exl-id: 2f8691ff-0442-45a5-aeba-c91c3af5c711
TQID: https://experienceleague.adobe.com/Bk5GTnQjm6NDosl5Iw6TS-NRjH8owNRUKoE0mZ-H3pY
product_v2:
  - id: b27e5950-9033-45ac-9f86-eb22e567f615
    internal-label: Marketo Engage
feature_v2:
  - id: b3b8a63f-51fc-40f6-a7d2-a31c5d49fb45
    internal-label: Configuration
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
topic_v2:
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
    internal-label: Security
---
# Marketo Mobile Extension for [!DNL Adobe Launch]

Install the Marketo Mobile SDK extension in [!DNL Adobe Launch] to send push notifications, in-app messages, or both.

## Prerequisites

- [Add an application in Marketo Admin](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/mobile-marketing/admin/add-a-mobile-app) and obtain the application Secret Key and Munchkin Id.
- Follow the installation instructions in the [!DNL Adobe Launch] portal.
- Optional: [Set up push notifications](push-notifications.md).

## iOS

### Setup Swift Bridging Header

1. Go to File > New > File and select "Header File".
1. Name the file "<_ProjectName_>-Bridging-Header".
1. Go to Project > Target > Build Phases > Swift Compiler > Code Generation.
1. Add the following path to Objective-Bridging Header:

    `$(PODS_ROOT)/<_ProjectName_>-Bridging-Header.h`

For Swift, remove the following import statement because the preceding steps add the bridging header.

`import Marketo/ALMarketo`

### iOS Test Devices

Follow the instructions in [Adding iOS Test Devices](installation.md#ios_test_devices).

### Handle Custom Url Type in AppDelegate

Follow the [custom URL instructions](installation.md#ios_test_devices).

### Set up push notifications on iOS

Follow the [push notification instructions](push-notifications.md). Use the class name "ALMarketo" instead of "Marketo".

## Android

### Configure Permissions

Open `AndroidManifest.xml` and add the following permissions. Your app must request the "INTERNET" and "ACCESS_NETWORK_STATE" permissions. Skip this step if the app already requests them.

```xml
<uses‐permission android:name="android.permission.INTERNET"></uses‐permission>
<uses‐permission android:name="android.permission.ACCESS_NETWORK_STATE"></uses‐permission>
```

### ProGuard Configuration (Optional)

If your app uses ProGuard, add the following lines to the `proguard.cfg` file in your project folder. This configuration excludes the Marketo SDK from obfuscation.

```text
-dontwarn com.marketo.*
-dontnote com.marketo.*
-keep class com.marketo.**{ *; }
```

### Android Test Devices

Follow the instructions in [Android Test Devices](installation.md#android_test_devices).

## Set up push notifications on Android

Follow the [Android Firebase Cloud Messaging instructions](installation.md#android_firebase_cloud_messaging_support). Use the class name "ALMarketo" instead of "Marketo".

To set up user profiles, follow the [user profile instructions](user-profiles.md). To set up custom actions, follow the [custom action instructions](custom-actions.md#android_custom_action). In both sets of instructions, use the class name "ALMarketo" instead of "Marketo".
