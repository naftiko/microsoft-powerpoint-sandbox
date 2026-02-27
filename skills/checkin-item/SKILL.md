# Check In PowerPoint File

Release the exclusive lock on a checked-out PowerPoint file and optionally publish a new version with a descriptive comment.

## API Details

- **API**: Microsoft PowerPoint API
- **Method**: POST
- **Path**: `/me/drive/items/{item-id}/checkin`
- **Operation ID**: `checkinItem`
- **Tag**: DocumentLocks
- **OpenAPI**: [microsoft-powerpoint-api.yaml](../../openapi/microsoft-powerpoint-api.yaml)

## Sandbox

Mock server URL: `http://localhost:8080/rest/microsoft-powerpoint-api/1.0.0/me/drive/items/{item-id}/checkin`

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

| Name | Type | Required | Description |
|------|------|----------|-------------|
| `comment` | string | No | Check-in comment associated with the version |

## Example Request

```bash
curl -X POST \
  "http://localhost:8080/rest/microsoft-powerpoint-api/1.0.0/me/drive/items/{item-id}/checkin" \
  -H "Authorization: Bearer {access-token}" \
  -H "Content-Type: application/json" \
  -d '{
    "comment": "Updated slide transitions and speaker notes."
  }'
```

## Example Response

**Status: 204 No Content**

*(empty body)*

## Instructions

When the user wants to release the lock on a checked-out PowerPoint file, use this operation. Make a POST request to `/me/drive/items/{item-id}/checkin` with an optional comment describing the changes. Returns 204 on success.
