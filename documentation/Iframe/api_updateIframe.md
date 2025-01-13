# API Documentation

## Endpoint: Update an Iframe

### URL

`PUT /iframes/:id`

### Description

This endpoint allows a superadmin user to update an existing iframe. The iframe can be updated with specific attributes such as `slug`, `groupId`, `reportId`, and `entityId`.

### Authentication

This endpoint requires the user to be authenticated.

### Authorization

Only users with the `superadmin` role are authorized to use this endpoint.

### Request Headers

- **Authorization**: Bearer token for authenticated user.

### Request Parameters

- **id** (string, required): The ID of the iframe to be updated.

### Request Body

The request body must be in JSON format and can include any of the following fields. At least one field must be provided for the update.

- **slug** (string, optional): A unique identifier for the iframe.
- **groupId** (string, optional): The ID of the group associated with the iframe.
- **reportId** (string, optional): The ID of the report associated with the iframe.
- **entityId** (string, optional): The ID of the entity associated with the iframe.

### Request Example

```json
{
  "slug": "updated-iframe-slug",
  "reportId": "updated-report123",
  "groupId": "updated-group123",
  "entityId": "updated-entity123"
}
```

### Response

#### Success (200 OK)

If the iframe is updated successfully, the server responds with a JSON object containing the success status, a success message, and the updated iframe data.

##### Response Example

```json
{
  "success": true,
  "message": "Iframe updated successfully",
  "data": {
    "_id": "60d9c6b0f1b4d72a8c8b4567",
    "slug": "updated-iframe-slug",
    "reportId": "updated-report123",
    "groupId": "updated-group123",
    "entityId": "updated-entity123",
    "createdBy": "60c72b1f4f1b4d72a8c8b123",
    "createdAt": "2024-07-10T12:34:56.789Z",
    "updatedAt": "2024-07-10T12:34:56.789Z"
  }
}
```

#### Client Error (400 Bad Request)

If no fields are provided for update, the server responds with an error message.

##### Response Example

```json
{
  "success": false,
  "message": "At least one field must be provided for update"
}
```

#### Client Error (404 Not Found)

If the iframe to be updated is not found, the server responds with a not found error message.

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

- **400**: No fields provided for update.
- **404**: Iframe not found.
- **500**: Internal server error.

### Middleware

- **isAuthenticatedUser**: Ensures the user is authenticated.
- **authorizeRoles("superadmin")**: Ensures the user has the `superadmin` role.

### Controller Function

The `handleUpdateIframe` function handles the update of the iframe and performs the necessary validations and operations as described above.