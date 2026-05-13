---
title: User Context
feature: REST API
description: Learn how to enable and use Marketo RTP User Context API to set custom variables, read user data across visits, and track viewed and clicked campaigns.
exl-id: b8daace2-07a5-4621-aa3a-03fa9f66ea73
TQID: https://experienceleague.adobe.com/Ph0Tw-C9jzWaR4bYyUIXyzzoa2yjHQk2gt6tNA8H2mA
product_v2:
  - id: b27e5950-9033-45ac-9f86-eb22e567f615
    internal-label: Marketo Engage
feature_v2:
  - id: e2290edd-b061-4880-9d79-dee306cf5aa9
    internal-label: Implementation
  - id: ed6be6bb-75bb-4ea9-9a42-3bcaa65e1bcc
    internal-label: Personalization
subfeature_v2:
  - id: a1d50dda-6d94-4e16-8c30-5eb7181c4650
    internal-label: Segmentation
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
    internal-label: Personalization
---
# User Context

User Context JavaScript API exposes user and visitor level data across multiple sessions to enable advanced personalization capability using historical user behavior and data. The API goes beyond data read and exposes custom variables that allow you to push meaningful data and events to the RTP backend for advanced segmentation and personalization purposes. Additional capabilities: [Triggers](../javascript-api/triggers.md), [Pattern Match](../javascript-api/pattern-match.md).

- You must become a Web Personalization customer and have the [RTP tag deployed](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/web-personalization/rtp-tag-implementation/deploy-the-rtp-javascript) on your site before using the User Context API.
- The User Context API is a feature that must be enabled by Marketo Support upon request. When the API is enabled, a userContext object under the RTP global object will be exposed.

## User Context Attributes

| Name | Type | Description |
| --- | --- | --- |
| `customVar[1-5]` | String | Custom data saved on user context. |
| `viewedCampaigns` | Campaign IDs as comma-separated string | Viewed campaigns in current or previous visits. |
| `clickedCampaigns` | Campaign IDs as comma-separated string | Clicked through campaigns in current or previous visits. |

## Set Custom Variables

Adding custom data to User Context.

### Usage

`rtp('set', 'customVar'[1-5], my_custom_value);`

| Parameter | Optional/Required | Type | Description |
| --- | --- | --- | --- |
| `'set'` | Required | String | Method action. |
| `customVar` | Required | String | Custom variable name. |
| `my_custom_value` | Required | String | Custom value to save on custom variable in index 1-5. |

Note: Custom variables are sent to RTP only in view call, so it is recommended to set custom variables before view is called. Otherwise, it will be sent only in next view call.

Custom Var Restrictions

- Custom variable length cannot be longer than 100 characters.
- Campaign data is limited to the last ten visits with ten campaigns per visit.

### Usage

`rtp('set', 'customVar', 'A');`

```javascript
// Set and get customVars
rtp('set', 'customVar1', 'foo');

// Read location
if (rtp.userContext.location.state == 'CA')  {
    // Do something
}

// Check if user viewed campaign id 45:
// The campaign id is exposed in the RTP UI when hovering over a campaign name.
if (rtp.userContext.viewedCampaign('45')) {
    // Do something
}
```
