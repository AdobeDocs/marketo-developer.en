---
title: Pattern Match
description: Use the RTP rtp.checkPattern utility to test string patterns with percent wildcards, see sync limitations, usage and URL examples, and required RTP tag setup.
feature: Javascript
exl-id: 4ebd13e3-375b-449b-850f-3b18f570ca75
TQID: https://experienceleague.adobe.com/-HopUg6-2EchL9kJrPDbz62mRlrqYaXYdufILjkvP1Y
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
# Pattern Match

RTP exposes a utility function to check if the pattern matches certain string. The utility can not be used in async because it returns an indication if there is a match or not.

You must become a Web Personalization customer and have the [RTP tag deployed](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/web-personalization/rtp-tag-implementation/deploy-the-rtp-javascript) on your site prior to using the User Context API.

## Usage

> rtp.checkPattern(check_against, pattern);

| Parameter | Optional/Required | Type | Description |
| --- | --- | --- | --- |
| check_against | Required | String | String to match the pattern against. For example: current page url, product name. |
| pattern | Required | String | Add % for wildcard. The pattern can be:start withend withcontainsfull match |

## Examples

Set custom variable in index 1 if current page URL ends with "productA".

```javascript
if (rtp.checkPattern(window.location.href, '%productA')) {
    rtp('set', 'custom1', 'productA');
}
```

The current URL path is '/products/productB'. This example checks if path contains "products" and set custom variable.

```javascript
var currentURLPath = '/products/productB';
if (rtp.checkPattern(currentURLPath, '%products%')) {
    rtp('set', 'custom1', 'products');
}
```
