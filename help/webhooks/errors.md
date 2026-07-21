---
title: Errors
feature: Webhooks
description: Learn Marketo webhook error codes, why 2xx responses are required to update lead fields, and how to catch and handle errors with Webhook is Called.
exl-id: adce40c3-87b1-4f31-8995-eb64e8a72b55
TQID: https://experienceleague.adobe.com/N2jNA4EUMMTUFL9uJHZhOor6Tlz4-EXWciwoXrPml48
product_v2:
  - id: b27e5950-9033-45ac-9f86-eb22e567f615
    internal-label: Marketo Engage
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
---
# Errors

This page describes error response codes for Marketo webhooks and explains how to handle webhook errors.

Marketo generates error codes 1000 and 1001. The system called by the Marketo webhook returns 2xx through 5xx response codes.

Marketo maps response values to a field only when the web service returns a 2xx response code. If a webhook response is intended to change values in a Marketo lead record, all other response codes cause Marketo to ignore the response for field updates.

| Response Code | Description |
| --- | --- |
| 1000 | This indicates that the 'Call Webhook' flow action is being housed within a Batch Campaign. Webhooks can only be fired from trigger campaigns. |
| 1001 | This indicates that the web service emitted an empty response body. |

## Catching a Webhook Error

Use the **[!UICONTROL Webhook is Called]** trigger to catch and handle webhook errors:

![Webhook is Called](assets/webhook-called.png)

* **Response** - The literal response payload received by the request.
* **Error Type** - The Reason-Phrase of the HTTP status message.

Use these values to respond to predictable errors and exceptions. Depending on the integrated service, you can automatically recover from some error classes and create alerts for unexpected errors.
