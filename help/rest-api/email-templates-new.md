---
title: Email Templates
feature: REST API
description: Learn how to use the new Marketo Asset REST API for email templates, including filtering, create/update, clone, delete, state transitions, and dependency lookup.
---
# Email Templates

[Email Template Endpoint Reference](https://developer.adobe.com/marketo-apis/api/asset/#tag/Email-Templates)

All endpoints shown below also require:

```
?access_token=<access_token>
```

and this header:

```
x-app-type: <app-type>
```

## Query

The new spec exposes query by id and a filter endpoint. It does not define a separate by-name endpoint, so name lookups should use `filter?name=...`.

### By ID

```
GET /rest/asset/v2/emailtemplate/{id}
```

```json
{
  "success": true,
  "warnings": [],
  "errors": [],
  "requestId": "14f9e#1900ab14001",
  "result": [
    {
      "id": "19",
      "name": "Base Newsletter Template",
      "description": "Core responsive template",
      "status": "draft"
    }
  ]
}
```

### Filter

`workspaceId` is required. The swagger also permits `folderId`, repeated `folderIds`, repeated `status`, `pageIndex`, `pageSize`, `createdBy`, `createdAtStart`, `createdAtEnd`, `modifiedBy`, `modifiedAtStart`, `modifiedAtEnd`, `name`, `sortKey`, `sortOrder`, `isCreatedByMe`, `isModifiedByMe`, `scriptEngine`, `isValueNonNullable`, and `includeArchived`.

```
GET /rest/asset/v2/emailtemplate/filter?workspaceId=1001&name=Newsletter&pageIndex=0&pageSize=20
```

```json
{
  "success": true,
  "warnings": [],
  "errors": [],
  "requestId": "33c4#1900ab1402f",
  "result": [
    {
      "id": "19",
      "name": "Base Newsletter Template",
      "status": "draft"
    }
  ]
}
```

## Create

Create uses JSON. `name` and `appData` are required. Per the schema, `appData` must include at least `folderId` or `workspaceId`.

```
POST /rest/asset/v2/emailtemplate
Content-Type: application/json
```

```json
{
  "name": "Base Newsletter Template",
  "description": "Core responsive template",
  "appData": {
    "workspaceId": "1001",
    "folderId": "15",
    "editorType": "emailTemplate"
  },
  "themeId": "42"
}
```

```json
{
  "success": true,
  "warnings": [],
  "errors": [],
  "requestId": "a99f#1900ab1407e",
  "result": [
    {
      "id": "1022",
      "name": "Base Newsletter Template",
      "status": "draft"
    }
  ]
}
```

The schema also allows `data`, `editorContext`, `appType`, and `status`, but the swagger does not define concrete examples for those fields.

## Update

```
POST /rest/asset/v2/emailtemplate/{id}/update
Content-Type: application/json
```

```json
{
  "name": "Base Newsletter Template v2",
  "description": "Updated responsive template",
  "appData": {
    "folderId": "15"
  }
}
```

```json
{
  "success": true,
  "warnings": [],
  "errors": [],
  "requestId": "cf10#1900ab140b3",
  "result": [
    {
      "id": "1022"
    }
  ]
}
```

## Approval and Draft State

The new swagger uses a single state transition endpoint for draft and approval operations. Valid actions are `approve`, `unapprove`, `discard`, and `create_draft`.

```
POST /rest/asset/v2/emailtemplate/state/transition
Content-Type: application/json
```

```json
{
  "contentId": "1022",
  "action": "approve"
}
```

## Delete

```
POST /rest/asset/v2/emailtemplate/{id}/delete
Content-Type: application/json
```

This endpoint takes the template id in the path and does not define a request body in the swagger.

## Clone

```
POST /rest/asset/v2/emailtemplate/clone
Content-Type: application/json
```

```json
{
  "assetId": "1022",
  "newAsset": {
    "name": "Base Newsletter Template Copy",
    "description": "Cloned template"
  }
}
```

## Query Dependencies

Use `usedby` to retrieve assets that reference a given template.

```
POST /rest/asset/v2/emailtemplate/usedby
Content-Type: application/json
```

```json
{
  "assetId": "1022",
  "pageIndex": 0,
  "pageSize": 20,
  "type": "all"
}
```
