# Create File or Folder Entry

Create a new empty file placeholder or folder as a child item under a specified OneDrive parent folder. This is useful for creating folder structures or reserving file names before uploading content.

## API Details

- **API**: Microsoft PowerPoint API
- **Method**: POST
- **Path**: `/me/drive/items/{parent-id}/children`
- **Operation ID**: `createChildItem`
- **Tag**: Uploads
- **OpenAPI**: [microsoft-powerpoint-api.yaml](../../openapi/microsoft-powerpoint-api.yaml)

## Sandbox

Mock server URL: `http://localhost:8080/rest/microsoft-powerpoint-api/1.0.0/me/drive/items/{parent-id}/children`

## Required Headers

- `Authorization: Bearer {access-token}`
- `Content-Type: application/json`

## OAuth Scopes

- `Files.ReadWrite`
- `Files.ReadWrite.All`

## Path Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `parent-id` | string | Yes | Unique ID of the parent folder |

## Request Body

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `name` | string | Yes | Name of the new file or folder |
| `file` | object | No | Empty object `{}` to indicate the item is a file |
| `folder` | object | No | Empty object `{}` to indicate the item is a folder |
| `@microsoft.graph.conflictBehavior` | string | No | Conflict resolution: `rename`, `replace`, or `fail` |

## Example Request

```bash
curl -X POST \
  "http://localhost:8080/rest/microsoft-powerpoint-api/1.0.0/me/drive/items/01PARENT00000001/children" \
  -H "Authorization: Bearer {access-token}" \
  -H "Content-Type: application/json" \
  -d '{
    "name": "Product-Launch-Slides.pptx",
    "file": {},
    "@microsoft.graph.conflictBehavior": "rename"
  }'
```

## Example Response

```json
{
  "id": "01CHILD0099887766",
  "name": "Product-Launch-Slides.pptx",
  "size": 0,
  "webUrl": "https://onedrive.live.com/redir?resid=01CHILD0099887766",
  "createdDateTime": "2025-06-15T15:00:00Z",
  "lastModifiedDateTime": "2025-06-15T15:00:00Z",
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
    "mimeType": "application/vnd.openxmlformats-officedocument.presentationml.presentation"
  }
}
```

## Instructions

When the user wants to create a new empty file placeholder or folder in OneDrive, use this operation. POST to `/me/drive/items/{parent-id}/children` with a JSON body containing the name and either a `file` or `folder` empty object to indicate the item type. Returns 201 on success or 409 if a name conflict occurs.
