# Upload or Replace a PowerPoint File

Upload or replace a PowerPoint presentation in OneDrive using a simple PUT request with raw file bytes. This operation supports files up to 4 MB in size. For larger files, use the Create Upload Session skill instead.

## API Details

- **API**: Microsoft PowerPoint API
- **Method**: PUT
- **Path**: `/me/drive/items/{parent-id}:/{filename}:/content`
- **Operation ID**: `uploadFile`
- **Tag**: Uploads
- **OpenAPI**: [microsoft-powerpoint-api.yaml](../../openapi/microsoft-powerpoint-api.yaml)

## Sandbox

Mock server URL: `http://localhost:8080/rest/microsoft-powerpoint-api/1.0.0/me/drive/items/{parent-id}:/{filename}:/content`

## Required Headers

- `Authorization: Bearer {access-token}`
- `Content-Type: application/vnd.openxmlformats-officedocument.presentationml.presentation`

## OAuth Scopes

- `Files.ReadWrite`
- `Files.ReadWrite.All`

## Path Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `parent-id` | string | Yes | Unique ID of the parent folder |
| `filename` | string | Yes | Desired file name including extension e.g. Keynote-Deck.pptx |

## Query Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `@microsoft.graph.conflictBehavior` | string | No | Conflict resolution: `rename`, `replace` (default), or `fail` |

## Example Request

```bash
curl -X PUT \
  "http://localhost:8080/rest/microsoft-powerpoint-api/1.0.0/me/drive/items/01PARENT00000001:/Keynote-Deck.pptx:/content" \
  -H "Authorization: Bearer {access-token}" \
  -H "Content-Type: application/vnd.openxmlformats-officedocument.presentationml.presentation" \
  --data-binary @Keynote-Deck.pptx
```

## Example Response

```json
{
  "id": "01ABCDEF12345678",
  "name": "Keynote-Deck.pptx",
  "size": 2457600,
  "webUrl": "https://onedrive.live.com/redir?resid=01ABCDEF12345678",
  "createdDateTime": "2025-01-10T09:00:00Z",
  "lastModifiedDateTime": "2025-06-15T14:30:00Z",
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
    "path": "/drive/root:/Presentations"
  },
  "file": {
    "mimeType": "application/vnd.openxmlformats-officedocument.presentationml.presentation",
    "hashes": {
      "quickXorHash": "aXhvckhBc2g="
    }
  },
  "@microsoft.graph.downloadUrl": "https://contoso-my.sharepoint.com/_api/download/01ABCDEF12345678"
}
```

## Instructions

When the user wants to upload or replace a PowerPoint file in OneDrive, use this operation by making a PUT request to `/me/drive/items/{parent-id}:/{filename}:/content` with the raw file bytes as the request body. The parent-id is the ID of the destination folder and the filename includes the `.pptx` extension. Returns 200 if an existing file was replaced or 201 if a new file was created.
