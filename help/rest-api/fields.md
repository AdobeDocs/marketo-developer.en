---
title: Fields
feature: REST API, Field Management
description: Learn REST and SOAP lead field naming, list fields via REST Describe Lead, feature mapping, why sfdcId is null, and use sfdcLeadId or sfdcContactId.
exl-id: 9033f32a-c7cb-4bbf-abcf-38ca4112139f
TQID: https://experienceleague.adobe.com/H2Bvhy-67U8JJ1V3JwYJ0O0vj4i11fwUCyYQtjxm8u0
product_v2:
  - id: b27e5950-9033-45ac-9f86-eb22e567f615
    internal-label: Marketo Engage
feature_v2:
  - id: b0bb9048-d951-48d8-8232-45cf248a7e27
    internal-label: Forms
  - id: c5f60233-d5ea-4453-a799-0ad258b4d399
    internal-label: Database
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
---
# Fields

The REST API and SOAP API use different naming conventions for lead fields.

## Retrieve the List of Field Names

Retrieve the list of all supported field names available on your lead records by using the REST 'Describe Lead' endpoint.

## Where to Use Which Field Name Type?

Sometimes it is difficult to know which field name type that you must use when leveraging a particular integration-related feature. The following is a quick reference for which features use REST or SOAP field name types.

| Feature | Field Name Type to Use |
| --- | --- |
| Lead Tracking API (Munchkin) | SOAP |
| Forms 2.0 API | SOAP |
| List Import (UI) | SOAP |
| List Import (REST API) | REST |
| Webhook Response Mappings | SOAP |
| Email Scripting (Velocity) | SOAP |
| SOAP API | SOAP |
| REST API | REST |

### Why does the REST API field sfdcId always return a value of null?

The field `sfdcId` is a formula field which was erroneously included in the original field map for the REST API. Records retrieved via the REST API do not compute the value of formula fields, so the value will always be null. To capture the real SFDC ID, you should use the fields called `sfdcLeadId` and `sfdcContactId`.
