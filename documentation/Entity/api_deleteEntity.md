# API Documentation

## Endpoint: Delete Entity

### URL

`DELETE /entity/:id`

### Description

This endpoint allows an admin to delete an existing entity by its ID. The response includes a success message indicating that the entity has been deleted.

### Authentication

This endpoint requires the user to be authenticated.

### Authorization

Only users with admin roles are authorized to use this endpoint.

### Request Headers

- **Authorization**: Bearer token for authenticated user.

### Request Parameters

- **id** (string, required): The ID of the entity to be deleted.

### Request Example

```
DELETE /entity/60d9c6b0f1b4d72a8c8b4567
```

### Response

#### Success (200 OK)

If the entity is deleted successfully, the server responds with a JSON object containing the success status and a success message.

##### Response Example

```json
{
  "success": true,
  "message": "Entity deleted successfully"
}
```

#### Client Error (400 Bad Request)

If the entity with the specified ID is not found, the server responds with a bad request error message.

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

- **400**: Entity not found.
- **500**: Internal server error.

### Controller Function

The `handleDeleteEntity` function handles the deletion of an entity by its ID and performs the necessary validations and operations as described above.