---
title: SOAP FAQ
feature: SOAP
description: Learn how to list programs with getMObjects, optimize getMultipleLeads, create opportunities, and send or schedule personalized emails via the Marketo SOAP API.
exl-id: a2d8f144-cd5f-41bc-8231-29c42af935b8
TQID: https://experienceleague.adobe.com/AWgJgPdDXmapXqvG-J93utvXGV8-zLnKO-DvWFzOYoI
product_v2:
  - id: b27e5950-9033-45ac-9f86-eb22e567f615
    internal-label: Marketo Engage
feature_v2:
  - id: e64968b2-4ee5-47f9-8cae-0588f184b9eb
    internal-label: Programs
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
---
# SOAP FAQ

As of July 31st, 2026, SOAP functionality has been removed.
Use the [REST API](rest-api/list-of-standard-fields.md) to communicate with Marketo.

## Migrating from `syncMObjects`

SOAP `syncMObjects` supported adding or updating tags and the channel for an existing program. The REST replacement is the [Update Program Metadata](https://developer.adobe.com/marketo-apis/api/asset#operation/updateProgramUsingPOST) endpoint, which updates a program's channel, tags, and period costs in a single call.

Pass the `channel` parameter to update the program's channel. This updates both the Program Settings Channel and the Channel tag, keeping them in sync. The channel must be valid for the program's type, and the update is rejected with error code `1173` when a child campaign uses a Change Program Status flow step, matching the validation enforced by the Marketo UI.

See the [Programs update section](rest-api/programs.md#update) and [Tags update section](rest-api/tags.md#update) for request examples.

