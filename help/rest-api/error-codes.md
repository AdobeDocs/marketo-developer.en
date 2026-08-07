---
title: Error Codes
feature: REST API
description: Learn Marketo REST API error handling with HTTP 413 and 414, response 6xx 7xx, record-level statuses, logging best practices, retries, and limits.
exl-id: a923c4d6-2bbc-4cb7-be87-452f39b464b6
TQID: https://experienceleague.adobe.com/-bV6fjqJ8RkIBGX6gpVKMjGX1qYXR2g7VK3efpEQLDM
product_v2:
  - id: b27e5950-9033-45ac-9f86-eb22e567f615
    internal-label: Marketo Engage
feature_v2:
  - id: b13bd2ad-8e65-49e5-9691-2a0d31067b35
    internal-label: Integrations
  - id: c5f60233-d5ea-4453-a799-0ad258b4d399
    internal-label: Database
  - id: d1d0a9cd-295d-4976-8c39-ddae266f240e
    internal-label: Administration
  - id: e64968b2-4ee5-47f9-8cae-0588f184b9eb
    internal-label: Programs
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
    internal-label: Metadata
  - id: cc72dcf1-72e1-48cc-b434-e7c27d62d67c
    internal-label: Accessibility
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
    internal-label: Administration
---
# Error Codes

Marketo REST APIs return errors at the HTTP, response, or record level. This page explains each error type and lists the associated error codes.

## Handling and Logging Exceptions

Log requests and responses when your integration encounters an unexpected exception. Some exceptions, such as expired authentication, can be handled by re-authenticating. Other exceptions can require assistance from Support, which will request the associated request and response details.

## Error Types

The Marketo REST API can return three types of errors during normal operation:

- **HTTP-Level:** Indicated by a `4xx` code.
- **Response-Level:** Included in the "errors" array of the JSON response.
- **Record-Level:** Included in the "result" array of the JSON response and indicated for each record by the "status" field and "reasons" array.

Response-Level and Record-Level errors return HTTP status code 200. For all error types, do not evaluate the HTTP reason phrase because it is optional and subject to change.

### HTTP-Level errors

During normal operation, Marketo returns two HTTP status code errors: `413 Request Entity Too Large` and `414 Request URI Too Long`. To recover from either error, modify the request and retry it. You can prevent these errors by checking request sizes before submission.

Marketo returns 413 when the request payload exceeds 1MB, or 10MB for Import Lead. Check the request size before submission. If records cause the request to exceed the limit, move those records to another request.

Marketo returns 414 when the URI of a GET request exceeds 8KB. Check the query-string length before submission. If it exceeds the limit, change the request method to POST, put the query string in the request body, and add the `_method=GET` parameter. Long URIs are most common when retrieving large record batches with long filter values, such as a GUID.

The [Identity](https://developer.adobe.com/marketo-apis/api/identity/) endpoint can return a 401 Unauthorized error, typically because the Client Id or Client Secret is invalid. The following table lists HTTP-Level error codes.

<table>
  <thead>
    <tr>
      <th> Response Code </th>
      <th> Description </th>
      <th colspan="1"> Comment </th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><a name="413"></a>413</td>
      <td>Request Entity Too Large</td>
      <td>The payload exceeded the 1MB limit.</td>
    </tr>
    <tr>
      <td><a name="414"></a>414</td>
      <td>Request-URI Too Long</td>
      <td>The URI of the request exceeded 8k. The request should be retried as a POST with param `_method=GET` in the URL, and the rest of the query string in the body of the request.</td>
    </tr>
  </tbody>
</table>

#### Response-Level errors

Response-Level errors occur when the response sets the `success` parameter to false. They use the following structure:

```json
{
    "requestId": "e42b#14272d07d78",
    "success": false,
    "errors": [
        {
            "code": "601",
            "message": "Unauthorized"
        }
    ]
}
```

Each object in the "errors" array contains two members:

- `code`: A quoted integer from 601 to 799.
- `message`: The plain-text reason for the error.

A 6xx code indicates that the entire request failed and was not executed. For example, recover from a 601 "Access token invalid" error by re-authenticating and passing the new access token with the request.

A 7xx code indicates that the request failed because no data was returned or the request parameters were invalid. Causes include an invalid date or a missing required parameter.

#### Response-Level Error Codes

>[!NOTE]
>
>An API call that returns this response code is not counted against your daily quota, or your rate limit.

<table>
  <thead>
    <tr>
      <th> Response Code </th>
      <th> Description </th>
      <th> Comment </th>
    </tr>
  </thead>
  <tbody>
  <tr>
      <td><a name="500"></a>500</td>
      <td>Internal Server error</td>
      <td>The server encountered an unexpected condition that prevented it from fulfilling the request.  Within Marketo, this may include improperly formed REST API request URLs.</td>
    </tr>
    <tr>
      <td><a name="502"></a>502</td>
      <td>Bad Gateway</td>
      <td>The remote server returned an error. Likely a timeout. The request should be retried with exponential backoff.</td>
    </tr>
    <tr>
      <td><a name="601"></a>601*</td>
      <td>Access token invalid</td>
      <td>An Access Token parameter was included in the request, but the value was not a valid access token.</td>
    </tr>
    <tr>
      <td><a name="602"></a>602*</td>
      <td>Access token expired</td>
      <td>The Access Token included in the call is no longer valid due to expiration.</td>
    </tr>
    <tr>
      <td><a name="603"></a>603</td>
      <td>Access denied</td>
      <td>Authentication is successful but the user does not have sufficient permission to call this API. [Additional permissions](custom-services.md) may need to be assigned to the user role, or <a href="https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/administration/additional-integrations/create-an-allowlist-for-ip-based-api-access">Allowlist for IP-Based API Access</a> may be enabled.</td>
    </tr>
    <tr>
      <td><a name="604"></a>604*</td>
      <td>Request time-out</td>
      <td>The request was running for too long (for example, encountered database contention), or exceeded the time-out period specified in the header of the call.</td>
    </tr>
    <tr>
      <td><a name="605"></a>605*</td>
      <td>HTTP Method not supported</td>
      <td>GET is not supported for the Sync Leads endpoint. POST must be used.</td>
    </tr>
    <tr>
      <td><a name="606"></a>606</td>
      <td>Max rate limit `%s`; exceeded with in `%s` secs</td>
      <td>The number of calls in the past 20 seconds was greater than 100</td>
    </tr>
    <tr>
      <td><a name="607"></a>607</td>
      <td>Daily quota reached</td>
      <td>The number of calls today exceeded the subscription's quota (resets daily at 12:00AM CST).>Your quota can be found in your Admin->Web Services menu. You can increase your quota through your account manager.</td>
    </tr>
    <tr>
      <td><a name="608"></a>608*</td>
      <td>API Temporarily Unavailable</td>
      <td></td>
    </tr>
    <tr>
      <td><a name="609"></a>609</td>
      <td>Invalid JSON</td>
      <td>The body included in the request is not valid JSON.</td>
    </tr>
    <tr>
      <td><a name="610"></a>610</td>
      <td>Requested resource not found</td>
      <td>The URI in the call did not match a REST API resource type. This is often due to an incorrectly spelled or incorrectly formatted request URI</td>
    </tr>
    <tr>
      <td><a name="611"></a>611*</td>
      <td>System error</td>
      <td>All unhandled exceptions</td>
    </tr>
    <tr>
      <td><a name="612"></a>612</td>
      <td>Invalid Content Type</td>
      <td>If you see this error, add a content type header specifying JSON format to your request. For example, try using `content type: application/json`. <a href="https://stackoverflow.com/questions/28181325/why-invalid-content-type">See this StackOverflow question</a> for more details.</td>
    </tr>
    <tr>
      <td><a name="613"></a>613</td>
      <td>Invalid Multipart Request</td>
      <td>The multipart content of the POST was not formatted correctly</td>
    </tr>
    <tr>
      <td><a name="614"></a>614</td>
      <td>Invalid Subscription</td>
      <td>The destination subscription cannot be found or is unreachable. This usually indicates temporary inaccessibility.</td>
    </tr>
    <tr>
      <td><a name="615"></a>615</td>
      <td>Concurrent access limit reached</td>
      <td>At most, requests are processed by any subscription 10 at a time. This is returned if there are already 10 ongoing requests.</td>
    </tr>
    <tr>
      <td><a name="616"></a>616</td>
      <td>Invalid subscription type</td>
      <td>The appropriate Marketo subscription type is required to access the Custom Object Metadata API. Consult your CSM for details.</td>
    </tr>
    <tr>
      <td><a name="701"></a>701</td>
      <td>%s cannot be blank</td>
      <td>The reported field must not be empty in the request</td>
    </tr>
    <tr>
      <td><a name="702"></a>702</td>
      <td>No data found for a given search scenario</td>
      <td>No records matched the given search parameters.
        Note: Many failed search operations return `success = true` and no errors and set a warnings informational string.</td>
    </tr>
    <tr>
      <td><a name="703"></a>703</td>
      <td>The feature is not enabled for the subscription</td>
      <td>A beta feature that has not been in enabled in a user's subscription</td>
    </tr>
    <tr>
      <td><a name="704"></a>704</td>
      <td>Invalid date format</td>
      <td><ul>
          <li>A date was specified that was not in the correct format</li>
          <li>An invalid dynamic content id was specified</li>
        </ul></td>
    </tr>
    <tr>
      <td><a name="709"></a>709</td>
      <td>Business Rule Violation</td>
      <td>The call cannot be fulfilled because it violates a requirement to create or update an asset, for example, trying to create an email without a template. It is also possible to get this error when trying to:
        <ul>
          <li>Retrieve content for landing pages that contain social content.</li>
          <li>Clone a program that contains certain asset types (see <a href="programs.md#clone">Program Clone</a> for more information).</li>
          <li>Approve an asset that has no draft (that is, has already been approved).</li>
        </ul></td>
    </tr>
    <tr>
      <td><a name="710"></a>710</td>
      <td>Parent Folder Not Found</td>
      <td>The specified parent folder could not be found</td>
    </tr>
    <tr>
      <td><a name="711"></a>711</td>
      <td>Incompatible Folder Type</td>
      <td>The specified folder was not of the correct type to fulfill the request</td>
    </tr>
    <tr>
      <td><a name="712"></a>712</td>
      <td>Merge to person Account operation is invalid</td>
      <td>A Merge Leads call failed because of an attempt to merge leads that are Salesforce Person Accounts.  Salesforce Person Accounts must be merged in Salesforce.</td>
    </tr>
    <tr>
      <td><a name="713"></a>713</td>
      <td>Transient Error</td>
      <td>A system resource was temporarily unavailable at the time of the API call. When this error is encountered, it is advised to wait for time and then retry the request.</td>
    </tr>
    <tr>
      <td><a name="714"></a>714</td>
      <td>Unable to find the default record type</td>
      <td>A Merge Leads call failed because it was unable to find a default record type.</td>
    </tr>
    <tr>
      <td><a name="718"></a>718</td>
      <td>ExternalSalesPersonID not found</td>
      <td>A Sync Opportunities call was made with a non-existent `ExternalSalesPersonID` value.</td>
    </tr>
    <tr>
      <td>719</td>
      <td>Lock wait timeout exception</td>
      <td>A Clone Program call was made and timed out waiting for a lock.</td>
    </tr>
  </tbody>
</table>

### Record-Level {#record_level_errors}

Record-Level errors indicate that the request was valid but the operation could not be completed for an individual record. A response with Record-Level errors follows this pattern:

#### Response

```json
{
   "requestId":"e42b#14272d07d78",
   "success":true,
   "result":[
      {
         "id":50,
         "status":"created"
      },
      {
         "id":51,
         "status":"created"
      },
      {
         "status":"skipped",
         "reasons":[
            {
               "code":"1005",
               "message":"Lead already exists"
            }
         ]
      }
   ]
}
```

Records in the result array appear in the same order as records in the request input array. Each record can succeed or fail independently, as indicated by its status field.

For a failed record, the "status" field is "skipped" and the record includes a "reasons" array. Each reason contains a "code" member and a "message" member. The code is always 1xxx, and the message explains why the record was skipped.

For example, if a Sync Leads request sets "action" to "createOnly" and a lead already exists for one of the submitted keys, the response returns code 1005 and the message "Lead already exists," as shown above.

#### Record-Level Error Codes

>[!NOTE]
>
><table>
  <tbody>
    <tr>
      <td>Response Code</td>
      <td>Description</td>
      <td>Comment</td>
    </tr>
    <tr>
      <td><a name="1001"></a>1001</td>
      <td>Invalid value &#8216;%s'. Required of type &#8216;%s'</td>
      <td>Error is generated whenever a parameter value has a type mismatch. For example the string value specified for an integer parameter.</td>
    </tr>
    <tr>
      <td><a name="1002"></a>1002</td>
      <td>Missing value for the required parameter &#8216;%s'</td>
      <td>Error is generated when a required parameter is missing from the request</td>
    </tr>
    <tr>
      <td><a name="1003"></a>1003</td>
      <td>Invalid data</td>
      <td>When the data submitted is not a valid type for the given endpoint or mode; such as when id is submitted for a lead with action designated as createOnly or when using Request Campaign on a batch campaign.</td>
    </tr>
    <tr>
      <td><a name="1004"></a>1004</td>
      <td>Lead not found</td>
      <td>For syncLead, when action is &#8220;updateOnly&#8221; and if lead is not found</td>
    </tr>
    <tr>
      <td><a name="1005"></a>1005</td>
      <td>Lead already exists</td>
      <td>For syncLead, when action is &#8220;createOnly&#8221; and if a lead already exists</td>
    </tr>
    <tr>
      <td><a name="1006"></a>1006</td>
      <td>Field &#8216;%s' not found</td>
      <td>An included field in the call is not a valid field.</td>
    </tr>
    <tr>
      <td><a name="1007"></a>1007</td>
      <td>Multiple leads match the lookup criteria</td>
      <td>Multiple leads match the lookup criteria. Updates can only be performed when the key matches a single record</td>
    </tr>
    <tr>
      <td><a name="1008"></a>1008</td>
      <td>Access denied to partition &#8216;%s'</td>
      <td>The user for the custom service does not have access to a workspace with the partition where the record exists.</td>
    </tr>
    <tr>
      <td><a name="1009"></a>1009</td>
      <td>Partition name must be specified</td>
      <td></td>
    </tr>
    <tr>
      <td><a name="1010"></a>1010</td>
      <td>Partition update not allowed</td>
      <td>The specified record already exists in a separate lead partition.</td>
    </tr>
    <tr>
      <td><a name="1011"></a>1011</td>
      <td>Field &#8216;%s' not supported</td>
      <td>When lookup field or `filterType` specified with unsupported standard fields (ex: firstName, lastName)</td>
    </tr>
    <tr>
      <td><a name="1012"></a>1012</td>
      <td>Invalid cookie value &#8216;%s'</td>
      <td>Can occur when calling the <a href="https://developer.adobe.com/marketo-apis/api/mapi#operation/associateLeadUsingPOST">Associate Lead</a> with an invalid value for the `cookie` parameter.
        This also occurs when calling <a href="https://developer.adobe.com/marketo-apis/api/mapi#operation/getLeadsByFilterUsingGET">Get Leads by Filter Type</a> with `filterType=cookies` and an invalid value for the `filterValues` parameter.</td>
    </tr>
    <tr>
      <td><a name="1013"></a>1013</td>
      <td>Object not found</td>
      <td>Get object (list, campaign) by id returns this error code</td>
    </tr>
    <tr>
      <td><a name="1014"></a>1014</td>
      <td>Failed to create Object</td>
      <td>Failed to create Object (list)</td>
    </tr>
    <tr>
      <td><a name="1015"></a>1015</td>
      <td>Lead not in list</td>
      <td>The designated lead is not a member of the target list</td>
    </tr>
    <tr>
      <td><a name="1016"></a>1016</td>
      <td>Too many imports</td>
      <td>There are too many imports queued. A maximum of 10 is allowed</td>
    </tr>
    <tr>
      <td><a name="1017"></a>1017</td>
      <td>Object already exists</td>
      <td>Creation failed because the record already exists</td>
    </tr>
    <tr>
      <td><a name="1018"></a>1018</td>
      <td>CRM Enabled</td>
      <td>The action could not be carried out, because the instance has a native CRM integration enabled.</td>
    </tr>
    <tr>
      <td><a name="1019"></a>1019</td>
      <td>Import in progress</td>
      <td>The target list is already being imported to</td>
    </tr>
    <tr>
      <td><a name="1020"></a>1020</td>
      <td>Too many clones to program</td>
      <td>The subscription has reached the allotted use of `cloneToProgramName` in the Schedule Program for the day</td>
    </tr>
    <tr>
      <td><a name="1021"></a>1021</td>
      <td>Company update not allowed</td>
      <td>Company update not allowed during syncLead</td>
    </tr>
    <tr>
      <td><a name="1022"></a>1022</td>
      <td>Object in use</td>
      <td>Delete is not allowed when an object is in use by another object</td>
    </tr>
    <tr>
      <td><a name="1025"></a>1025</td>
      <td>Program status not found</td>
      <td>A status was specified to Change Lead Program Status that did not match a status available for the program's channel.</td>
    </tr>
    <tr>
      <td><a name="1026"></a>1026</td>
      <td>Custom object not enabled</td>
      <td>The action could not be carried out, because the instance does not have custom objects integration enabled.</td>
    </tr>
    <tr>
      <td><a name="1027"></a>1027</td>
      <td>Max Activity Type Limit Reached</td>
      <td>The subscription has reached the maximum number of available custom activity types.</td>
    </tr>
    <tr>
      <td><a name="1028"></a>1028</td>
      <td>Max field limit reached</td>
      <td>Custom activities have a maximum of 20 secondary attributes.</td>
    </tr>
    <tr>
      <td><a name="1029"></a>1029</td>
      <td><ul>
          <li>Too many jobs in queue</li>
          <li>Export daily quota exceeded</li>
          <li>Job already queued</li>
        </ul></td>
      <td><ul>
          <li>Subscriptions are allowed a maximum of 10 bulk extract jobs in the queue at any given time.</li>
          <li>By default extract jobs are limited to 500MB per day (resets daily at 12:00AM CST).</li>
          <li>The export id has already been queued.</li>
        </ul></td>
    </tr>
    <tr>
      <td><a name="1035"></a>1035</td>
      <td>Unsupported filter type</td>
      <td>In some subscriptions, the following Bulk Lead Extract filter types are not supported:  updatedAt, smartListId, smartListName.</td>
    </tr>
    <tr>
      <td><a name="1036"></a>1036</td>
      <td>Duplicate object found in input</td>
      <td>A call was made to update two or more records using the same foreign key. For example,  a Sync Companies call using the same externalCompanyId for more than one company.</td>
    </tr>
    <tr>
      <td><a name="1037"></a>1037</td>
      <td>Lead was skipped</td>
      <td>The Lead was skipped because it is already in or past this status.</td>
    </tr>
    <tr>
      <td><a name="1042"></a>1042</td>
      <td>Invalid runAt date</td>
      <td>The runAt date specified for Schedule Campaign was too far into the future (the maximum is 2 years).</td>
    </tr>
    <tr>
      <td><a name="1048"></a>1048</td>
      <td>Custom Object Discard Draft Failed</td>
      <td>A call was made to discard the draft version of a custom object.</td>
    </tr>
    <tr>
      <td><a name="1049"></a>1049</td>
      <td>Failed to Create Activity</td>
      <td>Attributes array too long.
        The array of attributes passed to the record exceeded the max length of 65536 bytes</td>
    </tr>
    <tr>
      <td><a name="1076"></a>1076</td>
      <td><a href="https://developer.adobe.com/marketo-apis/api/mapi#operation/mergeLeadsUsingPOST">Merge Leads</a> call with mergeInCRM flag is 4.</td>
      <td>You are creating a duplicate record. It is recommended that you use an existing record instead.
        This is the error msg, which Marketo receives when merging in Salesforce.</td>
    </tr>
    <tr>
      <td><a name="1077"></a>1077</td>
      <td><a href="https://developer.adobe.com/marketo-apis/api/mapi#operation/mergeLeadsUsingPOST">Merge Leads</a> call failed due to `SFDC Field` length</td>
      <td>A Merge Leads call with mergeInCRM set to true failed due to `SFDC Field` exceeding the limit of allowed characters. To correct, reduce the length of `SFDC Field`, or set mergeInCRM to false.</td>
    </tr>
    <tr>
      <td><a name="1078"></a>1078</td>
      <td><a href="https://developer.adobe.com/marketo-apis/api/mapi#operation/mergeLeadsUsingPOST">Merge Leads</a> call failed due to deleted entity, not a lead/contact, or field filter criteria does not match.</td>
      <td>Merge failure, unable to perform merge operation in natively synced CRM
        This is the error msg, which Marketo receives when merging in Salesforce.</td>
    </tr>
    <tr>
      <td><a name="1079"></a>1079</td>
      <td><a href="https://developer.adobe.com/marketo-apis/api/mapi#operation/mergeLeadsUsingPOST">Merge Leads</a>  call failed due to Personalized URL conflict in duplicate records</td>
      <td>A Merge Leads call specified many Leads with the same Personalized URL. To resolve use Marketo Engage user interface to merge these records.</td>
    </tr>
  </tbody>
</table>
