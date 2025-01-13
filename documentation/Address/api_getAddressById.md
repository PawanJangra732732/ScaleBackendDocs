# API Documentation

## Endpoint: Get Address by ID

### URL

`GET /address/:id`

### Description

This endpoint allows an authenticated user to retrieve an address by its ID. The response includes the details of the specified address.

### Authentication

This endpoint requires the user to be authenticated.

### Authorization

No additional roles are required beyond authentication.

### Request Headers

- **Authorization**: Bearer token for authenticated user.

### Request Parameters

- **id** (string, required): The ID of the address to be retrieved.

### Request Example

```
GET /address/60d9c6b0f1b4d72a8c8b4567
```

### Response

#### Success (200 OK)

If the address is retrieved successfully, the server responds with a JSON object containing the success status and the address data.

##### Response Example

```json
{
  "success": true,
  "data": {
    "address": {
      "_id": "60d9c6b0f1b4d72a8c8b4567",
      "primaryAddress": {
        "street": "123 Main St",
        "city": "Anytown",
        "state": "Anystate",
        "zip": "12345"
      },
      "secondaryAddress": {
        "street": "456 Side St",
        "city": "Othertown",
        "state": "Otherstate",
        "zip": "67890"
      },
      "userId": "60c72b1f4f1b4d72a8c8b123",
      "createdAt": "2024-07-10T12:34:56.789Z",
      "updatedAt": "2024-07-10T12:34:56.789Z"
    }
  }
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

The `handleAddressGet` function handles the retrieval of an address by its ID and performs the necessary validations and operations as described above.