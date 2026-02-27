# List File Permissions

Retrieve all sharing permissions currently applied to a PowerPoint file or folder, including roles for users, groups, and links.

## API Details

- **API**: Microsoft PowerPoint API
- **Method**: GET
- **Path**: `/me/drive/items/{item-id}/permissions`
- **Operation ID**: `listItemPermissions`
- **Tag**: Permissions
- **OpenAPI**: [microsoft-powerpoint-api.yaml](../../openapi/microsoft-powerpoint-api.yaml)

## Sandbox

Mock server URL: `http://localhost:8080/rest/microsoft-powerpoint-api/1.0.0/me/drive/items/{item-id}/permissions`

## Required Headers

- `Authorization: Bearer {access-token}`

## OAuth Scopes

- `Files.Read`
- `Files.Read.All`

## Path Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `item-id` | string | Yes | Unique ID of the drive item |

## Example Request

```bash
curl -X GET \
  "http://localhost:8080/rest/microsoft-powerpoint-api/1.0.0/me/drive/items/{item-id}/permissions" \
  -H "Authorization: Bearer {access-token}"
```

## Example Response

```json
{
  "value": [
    {
      "id": "perm-001-owner",
      "roles": ["owner"],
      "grantedTo": {
        "user": {
          "id": "user-abc-123",
          "displayName": "Jane Smith",
          "email": "jane.smith@contoso.com"
        }
      }
    },
    {
      "id": "perm-002-write",
      "roles": ["write"],
      "grantedTo": {
        "user": {
          "id": "user-def-456",
          "displayName": "John Doe",
          "email": "john.doe@contoso.com"
        }
      }
    }
  ]
}
```

## Instructions

When the user wants to see who has access to a PowerPoint file, use this operation. Make a GET request to `/me/drive/items/{item-id}/permissions` to retrieve the full list of sharing permissions including owners, editors, and viewers.
