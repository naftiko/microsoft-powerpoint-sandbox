# Remove Permission

Revoke a specific sharing permission from a PowerPoint file or folder by its permission ID.

## API Details

- **API**: Microsoft PowerPoint API
- **Method**: DELETE
- **Path**: `/me/drive/items/{item-id}/permissions/{permission-id}`
- **Operation ID**: `deleteItemPermission`
- **Tag**: Permissions
- **OpenAPI**: [microsoft-powerpoint-api.yaml](../../openapi/microsoft-powerpoint-api.yaml)

## Sandbox

Mock server URL: `http://localhost:8080/rest/microsoft-powerpoint-api/1.0.0/me/drive/items/{item-id}/permissions/{permission-id}`

## Required Headers

- `Authorization: Bearer {access-token}`

## OAuth Scopes

- `Files.ReadWrite`
- `Files.ReadWrite.All`

## Path Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `item-id` | string | Yes | Unique ID of the drive item |
| `permission-id` | string | Yes | Unique ID of the permission entry |

## Example Request

```bash
curl -X DELETE \
  "http://localhost:8080/rest/microsoft-powerpoint-api/1.0.0/me/drive/items/{item-id}/permissions/{permission-id}" \
  -H "Authorization: Bearer {access-token}"
```

## Example Response

```
204 No Content
```

## Instructions

When the user wants to revoke someone's access to a PowerPoint file, use this operation. Make a DELETE request to `/me/drive/items/{item-id}/permissions/{permission-id}`. Returns 204 on success.
