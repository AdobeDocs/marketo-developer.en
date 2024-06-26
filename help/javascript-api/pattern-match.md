---
title: Pattern Match
description: Pattern Match
feature: Javascript
exl-id: 4ebd13e3-375b-449b-850f-3b18f570ca75
---
# Pattern Match

RTP exposes a utility function to check if the pattern matches certain string. The utility can not be used in async because it returns an indication if there is a match or not.

You must become a Web Personalization customer and have the [RTP tag deployed](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/web-personalization/rtp-tag-implementation/deploy-the-rtp-javascript) on your site prior to using the User Context API.

## Usage

> rtp.checkPattern(check_against, pattern);

| Parameter | Optional/Required | Type | Description |
|---|---|---|---|
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
