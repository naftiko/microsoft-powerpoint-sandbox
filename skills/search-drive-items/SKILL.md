# Search OneDrive for Presentations

Search file names, metadata, and indexed content within the signed-in user's OneDrive to find PowerPoint presentations and other files.

## API Details

- **API**: Microsoft PowerPoint API
- **Method**: GET
- **Path**: `/me/drive/root/search(q='{search-text}')`
- **Operation ID**: `searchDriveItems`
- **Tag**: Search
- **OpenAPI**: [microsoft-powerpoint-api.yaml](../../openapi/microsoft-powerpoint-api.yaml)

## Sandbox

Mock server URL: `http://localhost:8080/rest/microsoft-powerpoint-api/1.0.0/me/drive/root/search(q='{search-text}')`

## Required Headers

- `Authorization: Bearer {access-token}`

## OAuth Scopes

- `Files.Read`
- `Files.Read.All`

## Path Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `search-text` | string | Yes | The search query text |

## Query Parameters

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `$select` | string | No | Comma-separated list of properties to include in the response |
| `$top` | integer | No | Maximum number of results to return (default 25) |

## Example Request

```bash
curl -X GET \
  "http://localhost:8080/rest/microsoft-powerpoint-api/1.0.0/me/drive/root/search(q='product roadmap')?\$select=id,name,webUrl&\$top=10" \
  -H "Authorization: Bearer {access-token}"
```

## Example Response

**Status: 200 OK**

```json
{
  "value": [
    {
      "id": "01ABCDEF12345678",
      "name": "Product-Roadmap-Q2.pptx",
      "size": 4194304,
      "webUrl": "https://onedrive.live.com/redir?resid=01ABCDEF12345678",
      "createdDateTime": "2025-04-01T08:00:00Z",
      "lastModifiedDateTime": "2025-06-14T17:45:00Z",
      "file": {
        "mimeType": "application/vnd.openxmlformats-officedocument.presentationml.presentation"
      }
    },
    {
      "id": "01XYZABC98765432",
      "name": "Product-Roadmap-Q1.pptx",
      "size": 3670016,
      "webUrl": "https://onedrive.live.com/redir?resid=01XYZABC98765432",
      "createdDateTime": "2025-01-15T10:00:00Z",
      "lastModifiedDateTime": "2025-03-30T12:00:00Z",
      "file": {
        "mimeType": "application/vnd.openxmlformats-officedocument.presentationml.presentation"
      }
    }
  ]
}
```

## Instructions

When the user wants to find PowerPoint files in their OneDrive, use this operation. Make a GET request to `/me/drive/root/search(q='{search-text}')` with the search query. Use `$select` to limit returned fields and `$top` to control result count.
