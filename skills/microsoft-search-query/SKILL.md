# Search via Microsoft Search

Use the Microsoft Search API with KQL syntax to find PowerPoint files across OneDrive and all SharePoint sites the user has access to.

## API Details

- **API**: Microsoft PowerPoint API
- **Method**: POST
- **Path**: `/search/query`
- **Operation ID**: `microsoftSearchQuery`
- **Tag**: Search
- **OpenAPI**: [microsoft-powerpoint-api.yaml](../../openapi/microsoft-powerpoint-api.yaml)

## Sandbox

Mock server URL: `http://localhost:8080/rest/microsoft-powerpoint-api/1.0.0/search/query`

## Required Headers

- `Authorization: Bearer {access-token}`
- `Content-Type: application/json`

## OAuth Scopes

- `Files.Read.All`
- `Sites.Read.All`

## Request Body

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `requests` | array | Yes | Array of search request objects |
| `requests[].entityTypes` | array | Yes | Entity types to search (e.g., `driveItem`, `listItem`, `list`, `site`) |
| `requests[].query` | object | Yes | Query object containing the search string |
| `requests[].query.queryString` | string | Yes | KQL query string (e.g., `filetype:pptx product roadmap`) |
| `requests[].from` | integer | No | Offset for pagination |
| `requests[].size` | integer | No | Page size for results |
| `requests[].fields` | array | No | Array of field names to include in the response |

## Example Request

```bash
curl -X POST \
  "http://localhost:8080/rest/microsoft-powerpoint-api/1.0.0/search/query" \
  -H "Authorization: Bearer {access-token}" \
  -H "Content-Type: application/json" \
  -d '{
    "requests": [
      {
        "entityTypes": ["driveItem"],
        "query": {
          "queryString": "filetype:pptx product roadmap"
        },
        "from": 0,
        "size": 10
      }
    ]
  }'
```

## Example Response

**Status: 200 OK**

```json
{
  "value": [
    {
      "searchTerms": ["product", "roadmap"],
      "hitsContainers": [
        {
          "total": 2,
          "moreResultsAvailable": false,
          "hits": [
            {
              "hitId": "01ABCDEF12345678",
              "rank": 1,
              "summary": "Q2 2025 product roadmap with milestone timelines and feature prioritization...",
              "resource": {
                "id": "01ABCDEF12345678",
                "name": "Product-Roadmap-Q2.pptx",
                "size": 4194304,
                "webUrl": "https://onedrive.live.com/redir?resid=01ABCDEF12345678",
                "file": {
                  "mimeType": "application/vnd.openxmlformats-officedocument.presentationml.presentation"
                }
              }
            },
            {
              "hitId": "01XYZABC98765432",
              "rank": 2,
              "summary": "Q1 2025 product strategy and competitive landscape overview...",
              "resource": {
                "id": "01XYZABC98765432",
                "name": "Product-Roadmap-Q1.pptx",
                "size": 3670016,
                "webUrl": "https://onedrive.live.com/redir?resid=01XYZABC98765432",
                "file": {
                  "mimeType": "application/vnd.openxmlformats-officedocument.presentationml.presentation"
                }
              }
            }
          ]
        }
      ]
    }
  ]
}
```

## Instructions

When the user wants to search for PowerPoint files across OneDrive and SharePoint, use this operation. Make a POST request to `/search/query` with a KQL query string like `filetype:pptx` combined with keywords. This searches across all sites the user has access to, not just their personal OneDrive.
