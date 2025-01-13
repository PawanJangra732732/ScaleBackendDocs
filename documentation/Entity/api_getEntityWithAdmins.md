# API Documentation

## Endpoint: Get Entity with Admins

### URL

`GET /entity/:id/admins`

### Description

This endpoint allows users to retrieve an entity along with its associated admins. The response includes the entity details and the list of admins with their basic information.

### Authentication

This endpoint requires the user to be authenticated.

### Request Headers

- **Authorization**: Bearer token for authenticated user.

### Request Parameters

- **id** (string, required): The ID of the entity to be retrieved along with its admins.

### Request Example

```
GET /entity/60d9c6b0f1b4d72a8c8b4567/admins
```

### Response

#### Success (200 OK)

If the entity and its admins are retrieved successfully, the server responds with a JSON object containing the success status, the entity details, and the list of admins.

##### Response Example

```json
{
  "success": true,
  "entity": {
    "_id": "60d9c6b0f1b4d72a8c8b4567",
    "entityName": "Example Entity",
    "admins": [
      {
        "_id": "60d9c6b0f1b4d72a8c8b4568",
        "firstName": "John",
        "lastName": "Doe",
        "email": "johndoe@example.com",
        "role": "admin"
      },
      {
        "_id": "60d9c6b0f1b4d72a8c8b4569",
        "firstName": "Jane",
        "lastName": "Smith",
        "email": "janesmith@example.com",
        "role": "admin"
      }
    ],
    "createdAt": "2024-07-10T12:34:56.789Z",
    "updatedAt": "2024-07-10T12:34:56.789Z"
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

The `getEntityWithAdmins` function handles the retrieval of an entity along with its associated admins and performs the necessary validations and operations as described above.