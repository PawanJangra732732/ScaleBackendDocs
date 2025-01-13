# API Documentation

## Endpoint: Get Iframe by Slug

### URL

`GET /iframes`

### Description

This endpoint allows an authenticated user to retrieve an iframe based on its slug and the `entityId` from the authenticated user's token. The response includes the embed URL, report ID, and an embed token for the iframe.

### Authentication

This endpoint requires the user to be authenticated.

### Request Headers

- **Authorization**: Bearer token for authenticated user.
- **Cookie**: Contains the access token.

### Request Query Parameters

- **slug** (string, required): The slug of the iframe to be retrieved.

### Request Example

```
GET /iframes?slug=example-slug
```

### Response

#### Success (200 OK)

If the iframe is retrieved successfully, the server responds with a JSON object containing the success status and the iframe data including the embed URL, report ID, and embed token.

##### Response Example

```json
{
  "success": true,
  "data": {
    "embedUrl": "https://example.com/embed",
    "reportId": "report123",
    "embedToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
  }
}
```

#### Client Error (404 Not Found)

If no iframe is found with the specified slug and `entityId`, the server responds with a not found error message.

##### Response Example

```json
{
  "success": false,
  "message": "No iframe found"
}
```

#### Server Error (500 Internal Server Error)

If there is an internal server error, the server responds with an error message.

##### Response Example

```json
{
  "success": false,
  "message": "Internal Server Error"
}
```

### Errors

- **404**: No iframe found.
- **500**: Internal server error.

### Middleware

- **isAuthenticatedUser**: Ensures the user is authenticated.

### Controller Function

The `handleGetIframeBySlug` function handles the retrieval of an iframe based on its slug and the authenticated user's `entityId`. It performs the necessary validations and operations as described above.