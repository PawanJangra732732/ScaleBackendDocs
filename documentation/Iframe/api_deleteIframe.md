# API Documentation

## Endpoint: Delete an Iframe

### URL

`DELETE /admin/iframe/:id`

### Description

This endpoint allows a superadmin user to delete an existing iframe by its ID. The response includes a success message indicating that the iframe has been deleted.

### Authentication

This endpoint requires the user to be authenticated.

### Authorization

Only users with the `superadmin` role are authorized to use this endpoint.

### Request Headers

- **Authorization**: Bearer token for authenticated user.

### Request Parameters

- **id** (string, required): The ID of the iframe to be deleted.

### Request Example

```
DELETE /admin/iframe/60d9c6b0f1b4d72a8c8b4567
```

### Response

#### Success (200 OK)

If the iframe is deleted successfully, the server responds with a JSON object containing the success status and a success message.

##### Response Example

```json
{
  "success": true,
  "message": "Iframe deleted successfully"
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

The `handleDeleteIframe` function handles the deletion of an iframe by its ID and performs the necessary validations and operations as described above.