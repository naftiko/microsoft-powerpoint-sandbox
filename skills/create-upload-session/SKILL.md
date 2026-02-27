# Create Upload Session for Large PowerPoint Files

Initiate a resumable upload session for large PowerPoint files (greater than 4 MB) to enable reliable chunked byte-range transfers. The response contains an uploadUrl to which subsequent byte-range PUT requests should be sent.

## API Details

- **API**: Microsoft PowerPoint API
- **Method**: POST
- **Path**: `/me/drive/items/{parent-id}:/{filename}:/createUploadSession`
- **Operation ID**: `createUploadSession`
- **Tag**: Uploads
- **OpenAPI**: [microsoft-powerpoint-api.yaml](../../openapi/microsoft-powerpoint-api.yaml)

## Sandbox

Mock server URL: `http://localhost:8080/rest/microsoft-powerpoint-api/1.0.0/me/drive/items/{parent-id}:/{filename}:/createUploadSession`

## Required Headers

- `Authorization: Bearer {access-token}`

## OAuth Scopes

- `Files.ReadWrite`
- `Files.ReadWrite.All`

## Path Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `parent-id` | string | Yes | Unique ID of the parent folder |
| `filename` | string | Yes | Desired file name including extension e.g. All-Hands-Meeting.pptx |

## Request Body

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `item` | object | No | Object containing optional item properties |
| `item.@microsoft.graph.conflictBehavior` | string | No | Conflict resolution: `rename`, `replace`, or `fail` |
| `item.name` | string | No | Desired file name |
| `item.description` | string | No | Description of the file |

## Example Request

```bash
curl -X POST \
  "http://localhost:8080/rest/microsoft-powerpoint-api/1.0.0/me/drive/items/01PARENT00000001:/All-Hands-Meeting.pptx:/createUploadSession" \
  -H "Authorization: Bearer {access-token}" \
  -H "Content-Type: application/json" \
  -d '{
    "item": {
      "@microsoft.graph.conflictBehavior": "rename",
      "name": "All-Hands-Meeting.pptx"
    }
  }'
```

## Example Response

```json
{
  "uploadUrl": "https://contoso-my.sharepoint.com/_api/v2.0/upload/01PARENT00000001/All-Hands-Meeting.pptx",
  "expirationDateTime": "2025-06-16T14:30:00Z",
  "nextExpectedRanges": ["0-"]
}
```

## Instructions

When the user needs to upload a large PowerPoint file (over 4 MB), use this operation to create a resumable upload session. Make a POST request to the createUploadSession endpoint, then use the returned uploadUrl to send the file in byte-range chunks via PUT requests.
