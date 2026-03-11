---
title: Fragments
feature: REST API, Fragments
description: Marketo Asset REST API for the fragments, covering query by id, filtering, create/update, clone, delete, state transitions, and dependency lookup.
---
# Fragments

All endpoints shown below also require:

```
?access_token=<access_token>
```

and this header:

```
x-app-type: <app-type>
```

## Query

The new fragment API exposes query by id and filtering. There is no separate by-name endpoint in the swagger.

### By ID

```
GET /rest/asset/v2/fragment/{id}
```

```json
{
  "success": true,
  "warnings": [],
  "errors": [],
  "requestId": "fa0f#1900ab15001",
  "result": [
    {
      "id": "83",
      "name": "Hero Banner Fragment",
      "description": "Reusable hero block",
      "status": "approved"
    }
  ]
}
```

### Filter

`workspaceId` is required. The swagger also allows `folderId`, repeated `folderIds`, repeated `status`, `pageIndex`, `pageSize`, `createdBy`, `createdAtStart`, `createdAtEnd`, `modifiedBy`, `modifiedAtStart`, `modifiedAtEnd`, `name`, `fragmentType`, `sortKey`, `sortOrder`, `isCreatedByMe`, `isModifiedByMe`, `scriptEngine`, `isValueNonNullable`, and `includeArchived`.

```
GET /rest/asset/v2/fragment/filter?workspaceId=1001&fragmentType=email&pageIndex=0&pageSize=20
```

```json
{
  "success": true,
  "warnings": [],
  "errors": [],
  "requestId": "f9cc#1900ab1504a",
  "result": [
    {
      "id": "83",
      "name": "Hero Banner Fragment",
      "status": "approved"
    }
  ]
}
```

## Create

Create uses JSON. `name`, `appData`, and `settings` are required. Per the schema, `settings` must include `fragmentType` and `supportedChannels`.

```
POST /rest/asset/v2/fragment
Content-Type: application/json
```

```json
{
  "name": "Hero Banner Fragment",
  "description": "Reusable hero block",
  "appData": {
    "workspaceId": "1001",
    "folderId": "395",
    "editorType": "fragment"
  },
  "settings": {
    "fragmentType": "email",
    "fragmentSubType": "html",
    "supportedChannels": [
      "email"
    ]
  }
}
```

```json
{
  "success": true,
  "warnings": [],
  "errors": [],
  "requestId": "bd57#1900ab1509d",
  "result": [
    {
      "id": "13",
      "name": "Hero Banner Fragment",
      "status": "draft"
    }
  ]
}
```

The schema also allows `data`, `editorContext`, `themeId`, `appType`, and `status`, but the swagger does not define concrete values for each environment.

## Update

```
POST /rest/asset/v2/fragment/{id}/update
Content-Type: application/json
```

```json
{
  "name": "Hero Banner Fragment v2",
  "description": "Updated reusable hero block",
  "settings": {
    "fragmentSubType": "html",
    "supportedChannels": [
      "email"
    ]
  }
}
```

```json
{
  "success": true,
  "warnings": [],
  "errors": [],
  "requestId": "73d9#1900ab150f0",
  "result": [
    {
      "id": "13"
    }
  ]
}
```

## Approval and Draft State

The new swagger uses one state transition endpoint. Valid actions are `approve`, `unapprove`, `discard`, and `create_draft`.

```
POST /rest/asset/v2/fragment/state/transition
Content-Type: application/json
```

```json
{
  "contentId": "13",
  "action": "approve"
}
```

## Clone

```
POST /rest/asset/v2/fragment/clone
Content-Type: application/json
```

```json
{
  "assetId": "13",
  "newAsset": {
    "name": "Hero Banner Fragment Copy",
    "description": "Cloned fragment"
  }
}
```

## Delete

```
POST /rest/asset/v2/fragment/{id}/delete
Content-Type: application/json
```

This endpoint takes the fragment id in the path and does not define a request body in the swagger.

## Used By

Use `usedby` to retrieve assets that reference a given fragment.

```
POST /rest/asset/v2/fragment/usedby
Content-Type: application/json
```

```json
{
  "assetId": "13",
  "pageIndex": 0,
  "pageSize": 20,
  "type": "all"
}
```
