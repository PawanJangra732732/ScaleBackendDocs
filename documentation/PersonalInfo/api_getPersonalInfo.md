# API Documentation

## Endpoint: Get Personal Information by ID

### URL

`GET /personal-info/:id`

### Description

This endpoint allows users to retrieve personal information by its ID. The response includes the details of the specified personal information entry.

### Authentication

No authentication is required for this endpoint.

### Request Headers

No specific headers are required.

### Request Parameters

- **id** (string, required): The ID of the personal information to be retrieved.

### Request Example

```
GET /personal-info/60d9c6b0f1b4d72a8c8b4567
```

### Response

#### Success (200 OK)

If the personal information is retrieved successfully, the server responds with a JSON object containing the success status and the personal information data.

##### Response Example

```json
{
  "success": true,
  "data": {
    "_id": "60d9c6b0f1b4d72a8c8b4567",
    "firstName": "John",
    "lastName": "Doe",
    "phone": "123-456-7890",
    "dob": "1990-01-01",
    "userId": "60d9c6b0f1b4d72a8c8b4568",
    "createdAt": "2024-07-10T12:34:56.789Z",
    "updatedAt": "2024-07-10T12:34:56.789Z"
  }
}
```

#### Client Error (404 Not Found)

If the personal information ID is not provided or the personal information with the specified ID is not found, the server responds with a not found error message.

##### Response Example

```json
{
  "success": false,
  "message": "id not found"
}
```

##### Response Example

```json
{
  "success": false,
  "message": "Personal information not found"
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

- **404**: ID not found or personal information not found.
- **500**: Internal server error.

### Controller Function

The `handlePersonalInfoGet` function handles the retrieval of personal information by its ID and performs the necessary validations and operations as described above.