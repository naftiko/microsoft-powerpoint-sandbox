# Update Permission Role

Change the role of an existing sharing permission, such as downgrading a collaborator from write to read access.

## API Details

- **API**: Microsoft PowerPoint API
- **Method**: PATCH
- **Path**: `/me/drive/items/{item-id}/permissions/{permission-id}`
- **Operation ID**: `updateItemPermission`
- **Tag**: Permissions
- **OpenAPI**: [microsoft-powerpoint-api.yaml](../../openapi/microsoft-powerpoint-api.yaml)

## Sandbox

Mock server URL: `http://localhost:8080/rest/microsoft-powerpoint-api/1.0.0/me/drive/items/{item-id}/permissions/{permission-id}`

## Required Headers

- `Authorization: Bearer {access-token}`
- `Content-Type: application/json`

## OAuth Scopes

- `Files.ReadWrite`
- `Files.ReadWrite.All`

## Path Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `item-id` | string | Yes | Unique ID of the drive item |
| `permission-id` | string | Yes | Unique ID of the permission entry |

## Request Body

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `roles` | array of strings | Yes | The new permission roles to assign (`read`, `write`, `owner`) |

## Example Request

```bash
curl -X PATCH \
  "http://localhost:8080/rest/microsoft-powerpoint-api/1.0.0/me/drive/items/{item-id}/permissions/{permission-id}" \
  -H "Authorization: Bearer {access-token}" \
  -H "Content-Type: application/json" \
  -d '{
    "roles": ["read"]
  }'
```

## Example Response

```json
{
  "id": "perm-002-write",
  "roles": ["read"],
  "grantedTo": {
    "user": {
      "id": "user-def-456",
      "displayName": "John Doe",
      "email": "john.doe@contoso.com"
    }
  }
}
```

## Instructions

When the user wants to change the access level of a permission on a PowerPoint file, use this operation. Make a PATCH request to `/me/drive/items/{item-id}/permissions/{permission-id}` with a JSON body containing the new `roles` array.
