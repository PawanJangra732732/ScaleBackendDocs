# API Documentation

## Endpoint: Create an Iframe

### URL

`POST /iframes`

### Description

This endpoint allows a superadmin user to create a new iframe. The iframe is created with specific attributes such as `slug`, `reportId`, `groupId`, and `entityId`. The created iframe will be associated with the user who created it.

### Authentication

This endpoint requires the user to be authenticated.

### Authorization

Only users with the `superadmin` role are authorized to use this endpoint.

### Request Headers

- **Authorization**: Bearer token for authenticated user.

### Request Body

The request body must be in JSON format and include the following fields:

- **slug** (string, required): A unique identifier for the iframe.
- **reportId** (string, required): The ID of the report associated with the iframe.
- **groupId** (string, required): The ID of the group associated with the iframe.
- **entityId** (string, required): The ID of the entity associated with the iframe.

### Request Example

```json
{
  "slug": "unique-iframe-slug",
  "reportId": "report123",
  "groupId": "group123",
  "entityId": "entity123"
}
```

### Response

#### Success (201 Created)

If the iframe is created successfully, the server responds with a JSON object containing the success status, a success message, and the newly created iframe data.

##### Response Example

```json
{
  "success": true,
  "message": "Iframe created successfully",
  "data": {
    "_id": "60d9c6b0f1b4d72a8c8b4567",
    "slug": "unique-iframe-slug",
    "reportId": "report123",
    "groupId": "group123",
    "entityId": "entity123",
    "createdBy": "60c72b1f4f1b4d72a8c8b123",
    "createdAt": "2024-07-10T12:34:56.789Z",
    "updatedAt": "2024-07-10T12:34:56.789Z"
  }
}
```

#### Client Error (400 Bad Request)

If any required field (`slug`, `entityId`, `groupId`, `reportId`) is missing, the server responds with an error message.

##### Response Example

```json
{
  "success": false,
  "message": "slug, entityId, groupId and reportId fields are required"
}
```

#### Client Error (403 Forbidden)

If the authenticated user is not a superadmin, the server responds with a forbidden error message.

##### Response Example

```json
{
  "success": false,
  "message": "Forbidden"
}
```

#### Client Error (404 Not Found)

If the user who is creating the iframe is not found, the server responds with a not found error message.

##### Response Example

```json
{
  "success": false,
  "message": "User not found"
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

- **400**: Missing required fields.
- **403**: User is not authorized (not a superadmin).
- **404**: User not found.
- **500**: Internal server error.

### Middleware

- **isAuthenticatedUser**: Ensures the user is authenticated.
- **authorizeRoles("superadmin")**: Ensures the user has the `superadmin` role.

### Controller Function

The `handleCreationIframe` function handles the creation of the iframe and performs the necessary validations and operations as described above.