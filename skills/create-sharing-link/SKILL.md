# Create Sharing Link

Generate an anonymous or organizational sharing link for a PowerPoint file with configurable type, scope, optional password, and expiration date.

## API Details

- **API**: Microsoft PowerPoint API
- **Method**: POST
- **Path**: `/me/drive/items/{item-id}/createLink`
- **Operation ID**: `createSharingLink`
- **Tag**: Permissions
- **OpenAPI**: [microsoft-powerpoint-api.yaml](../../openapi/microsoft-powerpoint-api.yaml)

## Sandbox

Mock server URL: `http://localhost:8080/rest/microsoft-powerpoint-api/1.0.0/me/drive/items/{item-id}/createLink`

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

## Request Body

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `type` | string | Yes | The type of sharing link: `view`, `edit`, or `embed` |
| `scope` | string | No | The scope of the link: `anonymous`, `organization`, or `users` |
| `password` | string | No | Optional password to protect the sharing link |
| `expirationDateTime` | string (date-time) | No | Optional expiration date and time for the sharing link |

## Example Request

```bash
curl -X POST \
  "http://localhost:8080/rest/microsoft-powerpoint-api/1.0.0/me/drive/items/{item-id}/createLink" \
  -H "Authorization: Bearer {access-token}" \
  -H "Content-Type: application/json" \
  -d '{
    "type": "view",
    "scope": "anonymous",
    "expirationDateTime": "2025-07-15T00:00:00Z"
  }'
```

## Example Response

```json
{
  "id": "perm-link-004",
  "roles": ["read"],
  "link": {
    "type": "view",
    "scope": "anonymous",
    "webUrl": "https://contoso-my.sharepoint.com/:p:/g/personal/jane_smith/EaBcDeFgHiJkLmNoPqRsTu",
    "preventsDownload": false
  },
  "expirationDateTime": "2025-07-15T00:00:00Z",
  "hasPassword": false
}
```

## Instructions

When the user wants to create a shareable link for a PowerPoint file, use this operation. Make a POST request to `/me/drive/items/{item-id}/createLink` with the link type (view, edit, or embed), scope, and optional password or expiration. Returns 201 with the sharing link details.
