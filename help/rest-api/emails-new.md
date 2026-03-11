---
title: Emails
feature: REST API
description: Learn how to use the new Marketo Asset REST API for email metadata, filtering, create/update, cloning, state transitions, and dependency lookup.
---
# Emails

[Email Endpoint Reference](https://developer.adobe.com/marketo-apis/api/asset/#tag/Emails)

The new email asset endpoints in `swagger-new.json` use `/rest/asset/v2/email*` paths, JSON request bodies, and a required `x-app-type` header. Compared to the older Asset API examples, this spec documents metadata-oriented operations such as create, update, filter, clone, delete, state transition, and `usedby`. 

## Query

The new spec exposes query by `id` and a filter endpoint. It does not define a separate by-name endpoint. To look up an email by name, use the filter endpoint with the `name` query parameter.

All endpoints shown below also require:

```
?access_token=<access_token>
```

and this header:

```
x-app-type: <app-type>
```

### By ID

```
GET /rest/asset/v2/email/{id}
```

```json
{
  "success": true,
  "warnings": [],
  "errors": [],
  "requestId": "7b3c#1900ab12cd3",
  "result": [
    {
      "id": "1017",
      "name": "Spring Launch Email",
      "description": "Main announcement email",
      "status": "draft"
    }
  ]
}
```

### Filter

`workspaceId` is required. The spec also allows `folderId`, repeated `folderIds`, repeated `status`, `pageIndex`, `pageSize`, `createdBy`, `createdAtStart`, `createdAtEnd`, `modifiedBy`, `modifiedAtStart`, `modifiedAtEnd`, `name`, `sortKey`, `sortOrder`, `isCreatedByMe`, `isModifiedByMe`, `templateId`, `scriptEngine`, `isValueNonNullable`, and `includeArchived`.

```
GET /rest/asset/v2/email/filter?workspaceId=1001&name=Spring%20Launch&status=draft&status=approved&pageIndex=0&pageSize=20
```

```json
{
  "success": true,
  "warnings": [],
  "errors": [],
  "requestId": "5dd1#1900ab13011",
  "result": [
    {
      "id": "1017",
      "name": "Spring Launch Email",
      "status": "draft"
    }
  ]
}
```

## Create

Create uses JSON instead of the older form-encoded pattern. `name`, `appData`, and `headers` are required. Per the schema, `appData` must include at least one of `folderId`, `workspaceId`, or `programId`, and `headers.subject` is required.

```
POST /rest/asset/v2/email
Content-Type: application/json
```

```json
{
  "name": "Spring Launch Email",
  "description": "Main announcement email",
  "appData": {
    "workspaceId": "1001",
    "folderId": "2002",
    "editorType": "email"
  },
  "headers": {
    "subject": "Introducing the Spring Launch",
    "fromName": "Marketing Team",
    "fromEmail": "marketing@example.com",
    "replyEmail": "reply@example.com",
    "preheader": "See what changed this quarter",
    "ccEmails": [
      "owner@example.com"
    ]
  },
  "settings": {
    "isOperational": false,
    "isTextOnly": false,
    "isWebPageView": true,
    "enableUrlTracking": true
  },
  "templateId": "3003"
}
```

```json
{
  "success": true,
  "warnings": [],
  "errors": [],
  "requestId": "238c#1900ab1313f",
  "result": [
    {
      "id": "1017",
      "name": "Spring Launch Email",
      "status": "draft"
    }
  ]
}
```

The schema also permits optional `data`, `editorContext`, `themeId`, `appType`, and `status` fields, but the swagger does not further define what values are valid for every environment.

## Update

Update is done by id and accepts a JSON body using the `UpdateEmailRequest` schema. All properties are optional in the schema, so you can send only the fields you need to change.

```
POST /rest/asset/v2/email/{id}/update
Content-Type: application/json
```

```json
{
  "description": "Updated announcement email",
  "headers": {
    "subject": "Spring Launch Is Live",
    "preheader": "Read the latest release notes"
  },
  "settings": {
    "enableUrlTracking": true,
    "isWebPageView": true
  }
}
```

```json
{
  "success": true,
  "warnings": [],
  "errors": [],
  "requestId": "9fd3#1900ab13210",
  "result": [
    {
      "id": "1017"
    }
  ]
}
```

## Approval and Draft State

The new API replaces separate approve, unapprove, and discard endpoints with a single state transition endpoint. Valid actions in the schema are `approve`, `unapprove`, `discard`, and `create_draft`.

```
POST /rest/asset/v2/email/state/transition
Content-Type: application/json
```

```json
{
  "contentId": "1017",
  "action": "approve"
}
```

To unapprove, discard a draft, or create a new draft from an approved asset, change the `action` value accordingly.

## Clone

```
POST /rest/asset/v2/email/clone
Content-Type: application/json
```

```json
{
  "assetId": "1017",
  "newAsset": {
    "name": "Spring Launch Email Copy",
    "description": "Cloned from Spring Launch Email"
  }
}
```

## Delete

```
POST /rest/asset/v2/email/{id}/delete
Content-Type: application/json
```

This takes the asset `id` in the path and does not define a request body in the swagger.

## Used By

Use `usedby` to retrieve assets that reference a given email.

```
POST /rest/asset/v2/email/usedby
Content-Type: application/json
```

```json
{
  "assetId": "1017",
  "pageIndex": 0,
  "pageSize": 20,
  "type": "all"
}
```

