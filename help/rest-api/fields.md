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

The REST API and SOAP API use different naming conventions for lead fields. Use the field-name convention required by each integration feature.

## Retrieve the List of Field Names

Use the REST 'Describe Lead' endpoint to retrieve all supported field names for lead records.

## Where to Use Which Field Name Type?

The required field-name type depends on the integration feature. The following table identifies whether each feature uses REST or SOAP field names.

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

The `sfdcId` field is a formula field that was included in the original field map for the REST API. Records retrieved through the REST API do not compute formula field values, so `sfdcId` always returns null.

To retrieve the SFDC ID, use the `sfdcLeadId` and `sfdcContactId` fields.
