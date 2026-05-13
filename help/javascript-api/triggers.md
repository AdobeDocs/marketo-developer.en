---
title: Triggers
description: Use RTP triggers in Web Personalization to run functions on rtp state, including userContextReady, with syntax, parameters, and a location example.
feature: Javascript
exl-id: 588836fa-1e4d-41f3-aec5-5cd17eb16071
TQID: https://experienceleague.adobe.com/yTz9i4bnD4I0PDAmpnjdD1okYJzd40wriA-2ZzO5OMM
product_v2:
  - id: b27e5950-9033-45ac-9f86-eb22e567f615
    internal-label: Marketo Engage
feature_v2:
  - id: e2290edd-b061-4880-9d79-dee306cf5aa9
    internal-label: Implementation
  - id: ed6be6bb-75bb-4ea9-9a42-3bcaa65e1bcc
    internal-label: Personalization
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
    internal-label: Personalization
---
# Triggers

Adds the capability to trigger functions on certain state of the global rtp object.

You must be a Web Personalization customer and have the [RTP tag deployed](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/web-personalization/rtp-tag-implementation/deploy-the-rtp-javascript) on your site before using the User Context API.

## Usage

`rtp('triggerName', function_to_trigger);`

| Parameter | Optional/Required | Type | Description |
| --- | --- | --- | --- |
| 'triggerName' | Required | String | Method name. |
| function_to_trigger | Required | Function | Function to trigger. |

### User Context Ready Trigger

Sets a custom variable based on user location. This function is called when the "rtpUserContext" global object is ready.

```javascript
rtp('userContextReady', function() {
    if (rtpUserContext.location.state == 'CA') {
        rtp('set', 'custom1', 'productA');
    }
});
```
