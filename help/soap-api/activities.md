---
title: Activities
feature: SOAP
description: Learn how to interact with Activities using SOAP, retrieve lead activities and track lead changes with getLeadActivities and getLeadChanges
exl-id: fd695ab6-e7be-4ced-89c9-c4cd2d4c2ab0
TQID: https://experienceleague.adobe.com/6zUkvoDCqlRmblFDPWzLjdwITsyWxcXrJBKbLux76WI
product_v2:
  - id: b27e5950-9033-45ac-9f86-eb22e567f615
    internal-label: Marketo Engage
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
---
# Activities

The following SOAP calls can be used to interact with Activities.

- [getLeadActivities](getleadactivity.md)
- [getLeadChanges](getleadchanges.md)

>[!CAUTION]
>
>Beginning 2026-12-30, calls to the `Get Lead Activities` and `Get Lead Changes` endpoints which includes the `listId` parameter will fail (error code 1003) if the target lists contain 10,000 or more leads. To avoid service disruptions, ensure that calls are properly scoped to avoid this limit. See the [Migration guide](migration.md).
