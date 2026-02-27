# Get PowerPoint File Metadata

Retrieve metadata for a specific PowerPoint file or folder by its OneDrive item ID, including name, size, timestamps, author, and download URL.

## API Details

- **API**: Microsoft PowerPoint API
- **Method**: GET
- **Path**: `/me/drive/items/{item-id}`
- **Operation ID**: `getDriveItem`
- **Tag**: Metadata
- **OpenAPI**: [microsoft-powerpoint-api.yaml](../../openapi/microsoft-powerpoint-api.yaml)

## Sandbox

Mock server URL: `http://localhost:8080/rest/microsoft-powerpoint-api/1.0.0/me/drive/items/{item-id}`

## Required Headers

- `Authorization: Bearer {access-token}`

## OAuth Scopes

- `Files.Read`
- `Files.Read.All`

## Path Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `item-id` | string | Yes | Unique ID of the drive item |

## Query Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `$select` | string | No | Comma-separated list of properties to return |
| `$expand` | string | No | Relationships to expand inline |

## Example Request

```bash
curl -X GET \
  "http://localhost:8080/rest/microsoft-powerpoint-api/1.0.0/me/drive/items/01ABCDEF12345678?$select=id,name,size,lastModifiedDateTime" \
  -H "Authorization: Bearer {access-token}"
```

## Example Response

```json
{
  "id": "01ABCDEF12345678",
  "name": "Q2-Strategy-Deck.pptx",
  "description": "Q2 2025 corporate strategy presentation",
  "size": 3145728,
  "webUrl": "https://onedrive.live.com/redir?resid=01ABCDEF12345678",
  "createdDateTime": "2025-04-01T08:00:00Z",
  "lastModifiedDateTime": "2025-06-14T17:45:00Z",
  "createdBy": {
    "user": {
      "id": "user-abc-123",
      "displayName": "Jane Smith",
      "email": "jane.smith@contoso.com"
    }
  },
  "lastModifiedBy": {
    "user": {
      "id": "user-def-456",
      "displayName": "John Doe",
      "email": "john.doe@contoso.com"
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
  },
  "@microsoft.graph.downloadUrl": "https://contoso-my.sharepoint.com/_api/download/01ABCDEF12345678"
}
```

## Instructions

When the user wants to retrieve metadata about a PowerPoint file, use this operation. Make a GET request to `/me/drive/items/{item-id}`. Use `$select` to limit the returned properties and `$expand` to include relationships like thumbnails.
