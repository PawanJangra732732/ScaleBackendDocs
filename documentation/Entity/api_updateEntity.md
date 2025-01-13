
# API Documentation

## Endpoint: Update Entity

### URL

`PUT /entity/:id`

### Description

This endpoint allows users to update the name of an existing entity by its ID. The response includes the details of the updated entity if successful.

### Authentication

No authentication is required for this endpoint.

### Request Headers

No specific headers are required.

### Request Parameters

- **id** (string, required): The ID of the entity to be updated.

### Request Body

The request body must be in JSON format and include the following field:

- **entityName** (string, required): The new name of the entity.

### Request Example

```json
{
  "entityName": "Updated Entity Name"
}
```

### Response

#### Success (200 OK)

If the entity is updated successfully, the server responds with a JSON object containing the success status, a success message, and the updated entity data.

##### Response Example

```json
{
  "success": true,
  "message": "Entity updated successfully",
  "data": {
    "_id": "60d9c6b0f1b4d72a8c8b4567",
    "entityName": "Updated Entity Name",
    "createdAt": "2024-07-10T12:34:56.789Z",
    "updatedAt": "2024-07-10T13:34:56.789Z"
  }
}
```

#### Client Error (404 Not Found)

If the `entityName` field is missing or the entity with the specified ID is not found, the server responds with a not found error message.

##### Response Example

```json
{
  "success": false,
  "message": "Entity name is required"
}
```

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
w
```json
{
  "success": false,
  "message": "Internal Server Error"
}
```

### Errors

- **404**: Entity name is required or Entity not found.
- **500**: Internal server error.

### Controller Function

The `handleUpdateEntity` function handles the updating of an existing entity's name and performs the necessary validations and operations as described above.