# Delete PowerPoint File

Soft-delete a PowerPoint file or folder by moving it to the OneDrive recycle bin, where it can be restored within the retention period.

## API Details

- **API**: Microsoft PowerPoint API
- **Method**: DELETE
- **Path**: `/me/drive/items/{item-id}`
- **Operation ID**: `deleteDriveItem`
- **Tag**: Metadata
- **OpenAPI**: [microsoft-powerpoint-api.yaml](../../openapi/microsoft-powerpoint-api.yaml)

## Sandbox

Mock server URL: `http://localhost:8080/rest/microsoft-powerpoint-api/1.0.0/me/drive/items/{item-id}`

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
curl -X DELETE \
  "http://localhost:8080/rest/microsoft-powerpoint-api/1.0.0/me/drive/items/01ABCDEF12345678" \
  -H "Authorization: Bearer {access-token}"
```

## Example Response

```
204 No Content

(empty response body)
```

## Instructions

When the user wants to delete a PowerPoint file, use this operation. Make a DELETE request to `/me/drive/items/{item-id}`. The file is moved to the recycle bin (soft delete) and can be restored within the retention period. Returns 204 on success.
