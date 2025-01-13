# API Documentation

## Endpoint: Create Entity

### URL

`POST /entity`

### Description

This endpoint allows users to create a new entity. The response includes the details of the created entity if successful.

### Authentication

No authentication is required for this endpoint.

### Request Headers

No specific headers are required.

### Request Body

The request body must be in JSON format and include the following field:

- **entityName** (string, required): The name of the entity to be created.

### Request Example

```json
{
  "entityName": "Example Entity"
}
```

### Response

#### Success (201 Created)

If the entity is created successfully, the server responds with a JSON object containing the success status, a success message, and the created entity data.

##### Response Example

```json
{
  "success": true,
  "message": "Entity created successfully",
  "data": {
    "_id": "60d9c6b0f1b4d72a8c8b4567",
    "entityName": "Example Entity",
    "createdAt": "2024-07-10T12:34:56.789Z",
    "updatedAt": "2024-07-10T12:34:56.789Z"
  }
}
```

#### Client Error (400 Bad Request)

If the `entityName` field is missing, the server responds with a bad request error message.

##### Response Example

```json
{
  "success": false,
  "message": "All fields are required"
}
```

#### Client Error (409 Conflict)

If an entity with the specified name already exists, the server responds with a conflict error message.

##### Response Example

```json
{
  "success": false,
  "message": "Entity Already Exists"
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

- **400**: All fields are required.
- **409**: Entity already exists.
- **500**: Internal server error.

### Controller Function

The `handleCreateEntity` function handles the creation of a new entity and performs the necessary validations and operations as described above.