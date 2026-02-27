# Download PowerPoint File Content

Download the binary content of a PowerPoint presentation, with optional server-side conversion to PDF, HTML, JPG, or PNG format using the format query parameter.

## API Details

- **API**: Microsoft PowerPoint API
- **Method**: GET
- **Path**: `/me/drive/items/{item-id}/content`
- **Operation ID**: `getFileContent`
- **Tag**: Content
- **OpenAPI**: [microsoft-powerpoint-api.yaml](../../openapi/microsoft-powerpoint-api.yaml)

## Sandbox

Mock server URL: `http://localhost:8080/rest/microsoft-powerpoint-api/1.0.0/me/drive/items/{item-id}/content`

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
| `format` | string | No | Target format for server-side conversion: `pdf`, `html`, `jpg`, `png` |

## Example Request

```bash
curl -X GET \
  "http://localhost:8080/rest/microsoft-powerpoint-api/1.0.0/me/drive/items/01ABCDEF12345678/content?format=pdf" \
  -H "Authorization: Bearer {access-token}" \
  -L
```

## Example Response

The response is a 302 redirect to a pre-authenticated download URL or a binary content stream.

```json
{
  "@microsoft.graph.downloadUrl": "https://contoso-my.sharepoint.com/_api/download/01ABCDEF12345678?tempauth=token123"
}
```

## Instructions

When the user wants to download a PowerPoint file or convert it to another format, use this operation. Make a GET request to `/me/drive/items/{item-id}/content`. To convert the file, add the `format` query parameter (e.g., `?format=pdf`). The response is typically a 302 redirect to a pre-authenticated download URL.
