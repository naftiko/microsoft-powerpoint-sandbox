# Check Out PowerPoint File

Lock a PowerPoint presentation for exclusive editing by the current user, making it read-only for others until checked back in.

## API Details

- **API**: Microsoft PowerPoint API
- **Method**: POST
- **Path**: `/me/drive/items/{item-id}/checkout`
- **Operation ID**: `checkoutItem`
- **Tag**: DocumentLocks
- **OpenAPI**: [microsoft-powerpoint-api.yaml](../../openapi/microsoft-powerpoint-api.yaml)

## Sandbox

Mock server URL: `http://localhost:8080/rest/microsoft-powerpoint-api/1.0.0/me/drive/items/{item-id}/checkout`

## Required Headers

- `Authorization: Bearer {access-token}`

## OAuth Scopes

- `Files.ReadWrite`
- `Files.ReadWrite.All`

## Path Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `item-id` | string | Yes | Unique ID of the drive item |

## Example Request

```bash
curl -X POST \
  "http://localhost:8080/rest/microsoft-powerpoint-api/1.0.0/me/drive/items/{item-id}/checkout" \
  -H "Authorization: Bearer {access-token}"
```

## Example Response

**Status: 204 No Content**

*(empty body)*

## Instructions

When the user wants to lock a PowerPoint file for exclusive editing, use this operation. Make a POST request to `/me/drive/items/{item-id}/checkout`. The file becomes read-only for all other users. Returns 204 on success or 423 if the file is already checked out by another user.
