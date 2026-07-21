---
title: Custom Data Events
description: Send custom events with the RTP JavaScript API for Web Personalization, with parameters, string or array data up to four items, and click-based triggers.
feature: Javascript
exl-id: ef7cab9c-3bd0-450e-9247-9324b1e6f9ab
TQID: https://experienceleague.adobe.com/oWDmtMF94xG5HYXeTwkx5zF9PWo98bpwoVB6kAKLYDo
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
# Custom Data Events

Use this method to send custom events for tracking and real-time personalization. You can send third-party data or trigger a custom event based on visitor behavior.

Each custom data event is counted once during a visitor's session.

You must be a Web Personalization customer and have the [RTP tag deployed](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/web-personalization/rtp-tag-implementation/deploy-the-rtp-javascript) on your site before using the User Context API.

| Parameter | Optional/Required | Type | Description |
| --- | --- | --- | --- |
| `send` | Required | String | Method action. |
| `event` | Required | String | Method name. |
| `customData` | Required | String or Array | Custom data. |

## Examples

### Send Event using String for Custom Data

```javascript
var customData = {value: 'MyEvent'};
rtp('send', 'event', customData);
```

### Send Event using Array of Strings for Custom Data

The custom data array can contain up to four elements. To send more than four elements, call the Send Event API repeatedly with no more than four items in each call.

```javascript
var customData = {value: ['MyEvent', 'download - example whitepaper']};
rtp('send', 'event', customData);
```

### Send Event Based on Button Click

This example sends a custom data event when a visitor selects the button to download a specific white paper. RTP can use the event to segment those visitors in real time.

The website can then display a personalized campaign after two more clicks. For example, the campaign can present another piece of content related to the downloaded white paper.

```html
<button id="download-whitepaper" onclick="rtp('send', 'event', {value :'download - example whitepaper'})">Download</button>
```
