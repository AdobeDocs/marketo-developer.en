---
title: Get Lead API Updates
feature: REST API
description: Learn changes to the limits for Get Lead Activities and Get Lead Changes endpoints.

---
# Get Lead API Updates

Beginning 30 September 2026 calls to the [Get Lead Activities](https://developer.adobe.com/marketo-apis/api/mapi#operation/getLeadActivitiesUsingGET) or [Get Lead Changes](https://developer.adobe.com/marketo-apis/api/mapi#operation/getLeadChangesUsingGET) endpoints which include the `listId` parameter will fail if the target lists contain 10,000 or more leads with a 1003 Error Code indicating that the target static list has too many records. One or more API calls have recently been made which would be affected by this change. To avoid service disruptions, you may need to update the way your applications integrate with Marketo by 30 September 2026.

These types of queries often create searches which either have no potential results, or time out before any results are found. Limiting the size of the set improves the responsiveness of these types of queries and ensures that a search of the dataset can be completed in a timely manner. 

## How Can I Tell If I'm Affected? 

This change will only affect a small number of Marketo Engage instances. Administrators of affected subscriptions will be notified within the application before the change is applied. 

## What Do I Need to Do? 

You should share this document with the persons or team responsible for your Marketo Engage integrations. 

Depending on your use case, there are two basic options to migrate your application to: 

* Limit static lists from which you extract activities to a maximum of 10,000 members. You can split any of your existing lists into smaller lists to continue polling the same audience for activities. 
* Extract your Activities or Data Value Changes using Bulk Activity Extract or Data Streams, and join those results to static list membership with [getLeadByListId](https://developer.adobe.com/marketo-apis/api/mapi#operation/getLeadsByListIdUsingGET_1) or [Bulk Lead Extract](https://experienceleague.adobe.com/en/docs/marketo-developer/marketo/rest/bulk-extract/bulk-lead-extract)

## What Will Happen If I Do Nothing? 

You may experience interruptions in the function of your API integrations due to unhandled errors when querying for activities from static lists with large numbers of members.
