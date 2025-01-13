# API Documentation

## Endpoint: Get Single Iframe

### URL

`GET /admin/iframe/:id`

### Description

This endpoint allows a superadmin user to retrieve a single iframe by its ID. The response includes the details of the specified iframe.

### Authentication

This endpoint requires the user to be authenticated.

### Authorization

Only users with the `superadmin` role are authorized to use this endpoint.

### Request Headers

- **Authorization**: Bearer token for authenticated user.

### Request Parameters

- **id** (string, required): The ID of the iframe to be retrieved.

### Request Example

```
GET /admin/iframe/60d9c6b0f1b4d72a8c8b4567
```

### Response

#### Success (200 OK)

If the iframe is retrieved successfully, the server responds with a JSON object containing the success status, a success message, and the iframe data.

##### Response Example

```json
{
  "success": true,
  "message": "Iframe retrieved successfully",
  "data": {
    "_id": "60d9c6b0f1b4d72a8c8b4567",
    "slug": "iframe-slug-1",
    "reportId": "report123",
    "groupId": "group123",
    "entityId": "entity123",
    "createdBy": "60c72b1f4f1b4d72a8c8b123",
    "createdAt": "2024-07-10T12:34:56.789Z",
    "updatedAt": "2024-07-10T12:34:56.789Z"
  }
}
```

#### Client Error (404 Not Found)

If the iframe with the specified ID is not found, the server responds with a not found error message.

##### Response Example

```json
{
  "success": false,
  "message": "Iframe not found"
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

- **404**: Iframe not found.
- **500**: Internal server error.

### Middleware

- **isAuthenticatedUser**: Ensures the user is authenticated.
- **authorizeRoles("superadmin")**: Ensures the user has the `superadmin` role.

### Controller Function

The `handleGetSingleIframe` function handles the retrieval of a single iframe by its ID and performs the necessary validations and operations as described above.