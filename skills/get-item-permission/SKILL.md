# Get Specific Permission

Retrieve details for a single sharing permission on a PowerPoint file by its permission ID.

## API Details

- **API**: Microsoft PowerPoint API
- **Method**: GET
- **Path**: `/me/drive/items/{item-id}/permissions/{permission-id}`
- **Operation ID**: `getItemPermission`
- **Tag**: Permissions
- **OpenAPI**: [microsoft-powerpoint-api.yaml](../../openapi/microsoft-powerpoint-api.yaml)

## Sandbox

Mock server URL: `http://localhost:8080/rest/microsoft-powerpoint-api/1.0.0/me/drive/items/{item-id}/permissions/{permission-id}`

## Required Headers

- `Authorization: Bearer {access-token}`

## OAuth Scopes

- `Files.Read`
- `Files.Read.All`

## Path Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `item-id` | string | Yes | Unique ID of the drive item |
| `permission-id` | string | Yes | Unique ID of the permission entry |

## Example Request

```bash
curl -X GET \
  "http://localhost:8080/rest/microsoft-powerpoint-api/1.0.0/me/drive/items/{item-id}/permissions/{permission-id}" \
  -H "Authorization: Bearer {access-token}"
```

## Example Response

```json
{
  "id": "perm-002-write",
  "roles": ["write"],
  "grantedTo": {
    "user": {
      "id": "user-def-456",
      "displayName": "John Doe",
      "email": "john.doe@contoso.com"
    }
  },
  "grantedToV2": {
    "user": {
      "id": "user-def-456",
      "displayName": "John Doe"
    }
  }
}
```

## Instructions

When the user needs details about a specific permission on a PowerPoint file, use this operation. Make a GET request to `/me/drive/items/{item-id}/permissions/{permission-id}`.
