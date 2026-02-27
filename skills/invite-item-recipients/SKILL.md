# Share via Invitation

Grant permissions and optionally send an email sharing invitation to specified recipients with configurable roles and sign-in requirements.

## API Details

- **API**: Microsoft PowerPoint API
- **Method**: POST
- **Path**: `/me/drive/items/{item-id}/invite`
- **Operation ID**: `inviteItemRecipients`
- **Tag**: Permissions
- **OpenAPI**: [microsoft-powerpoint-api.yaml](../../openapi/microsoft-powerpoint-api.yaml)

## Sandbox

Mock server URL: `http://localhost:8080/rest/microsoft-powerpoint-api/1.0.0/me/drive/items/{item-id}/invite`

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
| `recipients` | array | Yes | Array of objects with `email` property identifying each recipient |
| `message` | string | No | Optional message to include in the sharing invitation email |
| `requireSignIn` | boolean | No | Whether recipients must sign in to access the file (default: `true`) |
| `sendInvitation` | boolean | No | Whether to send an email notification to recipients (default: `true`) |
| `roles` | array | Yes | Permission roles to grant: `read` or `write` |

## Example Request

```bash
curl -X POST \
  "http://localhost:8080/rest/microsoft-powerpoint-api/1.0.0/me/drive/items/{item-id}/invite" \
  -H "Authorization: Bearer {access-token}" \
  -H "Content-Type: application/json" \
  -d '{
    "recipients": [
      {
        "email": "alice.wang@contoso.com"
      }
    ],
    "message": "Please review the presentation",
    "roles": ["write"],
    "requireSignIn": true,
    "sendInvitation": true
  }'
```

## Example Response

```json
{
  "value": [
    {
      "id": "perm-003-invite",
      "roles": ["write"],
      "grantedTo": {
        "user": {
          "id": "user-ghi-789",
          "displayName": "Alice Wang",
          "email": "alice.wang@contoso.com"
        }
      }
    }
  ]
}
```

## Instructions

When the user wants to share a PowerPoint file with others by email, use this operation. Make a POST request to `/me/drive/items/{item-id}/invite` with recipients, roles, and optional invitation message.
