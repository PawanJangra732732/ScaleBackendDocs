# API Documentation

## Endpoint: Delete Address by ID

### URL

`DELETE /address/:id`

### Description

This endpoint allows an authenticated user to delete an address by its ID. The response includes a success message indicating that the address has been deleted.

### Authentication

This endpoint requires the user to be authenticated.

### Authorization

No additional roles are required beyond authentication.

### Request Headers

- **Authorization**: Bearer token for authenticated user.

### Request Parameters

- **id** (string, required): The ID of the address to be deleted.

### Request Example

```
DELETE /address/60d9c6b0f1b4d72a8c8b4567
```

### Response

#### Success (200 OK)

If the address is deleted successfully, the server responds with a JSON object containing the success status and a success message.

##### Response Example

```json
{
  "success": true,
  "message": "Address deleted successfully"
}
```

#### Client Error (404 Not Found)

If the address with the specified ID is not found, the server responds with a not found error message.

##### Response Example

```json
{
  "success": false,
  "message": "Address not found"
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

- **404**: Address not found.
- **500**: Internal server error.

### Middleware

- **isAuthenticatedUser**: Ensures the user is authenticated.

### Controller Function

The `handleAddressDelete` function handles the deletion of an address by its ID and performs the necessary validations and operations as described above.