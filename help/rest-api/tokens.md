---
title: Tokens
feature: REST API, Tokens
description: Manage Marketo My Tokens with Asset REST API. See supported data types, get by folder or program, create or update via form-encoded POST, and delete by name.
exl-id: 4f8d87d7-ba2a-4c90-8b39-4d20679d404a
TQID: https://experienceleague.adobe.com/uqOpu2vDuiQiZhILKuxZJQGadd0K14zwIaAdmNfK1-I
product_v2:
  - id: b27e5950-9033-45ac-9f86-eb22e567f615
    internal-label: Marketo Engage
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
---
# Tokens

[Token Endpoint Reference](https://developer.adobe.com/marketo-apis/api/asset#tag/Tokens)

Tokens are strings that Marketo replaces with other data at run time. The API can edit only My Tokens, which are child tokens local to a folder or program.

Use the Tokens API to read, create, update, and delete My Tokens.

## Data Type

Tokens can be created with the following data types:

| Type | Description |
| --- | --- |
| date | Date value of the form "yyyy-MM-dd" |
| number | An integer or floating point number |
| rich text | An HTML string |
| score | A signed 32-bit integer |
| sfdc campaign | Used in Salesforce campaign management integration |
| text | A text string |

The API supports only these data types when creating a token.

## Query

[Get Tokens by Folder ID](https://developer.adobe.com/marketo-apis/api/asset#tag/Tokens/operation/getTokensByFolderIdUsingGET) takes the ID of a program or folder as a path parameter. Use the `folderType` parameter to specify the type.

```http
GET /rest/asset/v1/folder/{id}/tokens.json?folderType=Folder
```

```json
{
    "success": true,
    "warnings": [],
    "errors": [],
    "requestId": "4fbe#14e27fc9bbf",
    "result": [
        {
            "folder": {
                "type": "Folder",
                "value": 416
            },
            "tokens": [
                {
                    "name": "AprilFool - deverly",
                    "type": "date",
                    "value": "2015-04-01",
                    "computedUrl": "https://app-abm.marketo.com/#MF1047C3"
                }
            ]
        }
    ]
}

```

## Create and Update

The [Create Token](https://developer.adobe.com/marketo-apis/api/asset#tag/Tokens/operation/addTokenTOFolderUsingPOST) endpoint creates a token or updates an existing token with the submitted values. Tokens belong to a folder or program.

The `id` path parameter identifies the parent folder. The `name`, `type`, `value`, and `folderType` parameters are required. Pass the data as POST `x-www-form-urlencoded`, not as JSON. The token `name` cannot exceed 50 characters.

```http
POST /rest/asset/v1/folder/{id}/tokens.json
```

```text
Content-Type: application/x-www-form-urlencoded
```

```text
name=April Fools&type=date&value=2015-04-01&folderType=Folder
```

```json
{
    "success": true,
    "warnings": [],
    "errors": [],
    "requestId": "e3c2#14e280db5dc",
    "result": [
        {
            "folder": {
                "type": "Folder",
                "value": 416
            },
            "tokens": [
                {
                    "name": "April Fools",
                    "type": "date",
                    "value": "2015-04-01",
                    "computedUrl": "https://app-abm.marketo.com/#MF1047C3"
                }
            ]
        }
    ]
}

```

## Delete

[Delete Token by Name](https://developer.adobe.com/marketo-apis/api/asset#tag/Tokens/operation/deleteTokenByNameUsingPOST) takes the ID of a program or folder as a path parameter. Use `folderType` to specify the type.

The parent folder, token `name`, and token `type` are required. Pass the data as POST `x-www-form-urlencoded`, not as JSON.

```http
POST /rest/asset/v1/folder/{id}/tokens/delete.json
```

```text
Content-Type: application/x-www-form-urlencoded
```

```text
name=AprilFool - deverly&type=date&folderType=Program
```

```json
{
    "success": true,
    "warnings": [],
    "errors": [],
    "requestId": "12ed2#14e2800f89c",
    "result": [
        {
            "id": 416
        }
    ]
}

```
