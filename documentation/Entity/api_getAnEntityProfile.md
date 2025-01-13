# API Documentation

## Endpoint: Get a Single Entity Profile

### URL

`GET /entity/:id`

### Description

This endpoint allows users to retrieve a single entity profile by its ID. If the requesting user is an admin, they can only retrieve their own entity profile.

### Authentication

Authentication is required for this endpoint.

### Request Headers

- **Authorization**: Bearer token for authenticated user.

### Request Parameters

- **id** (string, required): The ID of the entity to be retrieved.

### Request Example

```
GET /entity/60d9c6b0f1b4d72a8c8b4567
```

### Response

#### Success (200 OK)

If the entity is retrieved successfully, the server responds with a JSON object containing the success status, a success message, and the entity data.

##### Response Example

```json
{
  "success": true,
  "message": "Entity retrieved successfully",
  "data": {
    "_id": "60d9c6b0f1b4d72a8c8b4567",
    "entityName": "Example Entity",
    "admins": [
      {
        "_id": "60d9c6b0f1b4d72a8c8b4568",
        "name": "Admin User",
        "email": "admin@example.com"
      }
    ]
  }
}
```

#### Client Error (404 Not Found)

If the entity with the specified ID is not found, the server responds with a not found error message.

##### Response Example

```json
{
  "success": false,
  "message": "Entity not found"
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

- **404**: Entity not found.
- **500**: Internal server error.

### Controller Function

The `handleGetAnEntityProfile` function handles the retrieval of a single entity profile by its ID and performs the necessary validations and operations as described above. If the user is an admin, they can only retrieve their own entity profile.