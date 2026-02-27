# Update PowerPoint File Metadata

Update writable properties on a PowerPoint file such as its name, description, or parent folder location for moving the file to a different folder.

## API Details

- **API**: Microsoft PowerPoint API
- **Method**: PATCH
- **Path**: `/me/drive/items/{item-id}`
- **Operation ID**: `updateDriveItem`
- **Tag**: Metadata
- **OpenAPI**: [microsoft-powerpoint-api.yaml](../../openapi/microsoft-powerpoint-api.yaml)

## Sandbox

Mock server URL: `http://localhost:8080/rest/microsoft-powerpoint-api/1.0.0/me/drive/items/{item-id}`

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

| Property | Type | Description |
|----------|------|-------------|
| `name` | string | New name for the file |
| `description` | string | New description for the file |
| `parentReference` | object | Destination folder reference for moving the file |
| `fileSystemInfo` | object | File system timestamps (`createdDateTime`, `lastModifiedDateTime`) |

## Example Request

```bash
curl -X PATCH \
  "http://localhost:8080/rest/microsoft-powerpoint-api/1.0.0/me/drive/items/01ABCDEF12345678" \
  -H "Authorization: Bearer {access-token}" \
  -H "Content-Type: application/json" \
  -d '{
    "name": "Q2-Strategy-Deck-Final.pptx",
    "description": "Q2 2025 corporate strategy presentation — approved"
  }'
```

## Example Response

```json
{
  "id": "01ABCDEF12345678",
  "name": "Q2-Strategy-Deck-Final.pptx",
  "description": "Q2 2025 corporate strategy presentation — approved",
  "size": 3145728,
  "webUrl": "https://onedrive.live.com/redir?resid=01ABCDEF12345678",
  "createdDateTime": "2025-04-01T08:00:00Z",
  "lastModifiedDateTime": "2025-06-15T16:00:00Z",
  "createdBy": {
    "user": {
      "id": "user-abc-123",
      "displayName": "Jane Smith",
      "email": "jane.smith@contoso.com"
    }
  },
  "lastModifiedBy": {
    "user": {
      "id": "user-abc-123",
      "displayName": "Jane Smith",
      "email": "jane.smith@contoso.com"
    }
  },
  "parentReference": {
    "driveId": "b!drive-id-001",
    "driveType": "business",
    "id": "01PARENT00000001",
    "path": "/drive/root:/Decks"
  },
  "file": {
    "mimeType": "application/vnd.openxmlformats-officedocument.presentationml.presentation",
    "hashes": {
      "quickXorHash": "cXlvckhDdHg="
    }
  }
}
```

## Instructions

When the user wants to rename, describe, or move a PowerPoint file, use this operation. Make a PATCH request to `/me/drive/items/{item-id}` with a JSON body containing the properties to update. To move a file, include a `parentReference` object with the destination folder's `id`. Returns 200 on success or 409 on name conflict.
