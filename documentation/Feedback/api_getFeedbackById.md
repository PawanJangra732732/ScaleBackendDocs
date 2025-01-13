# API Documentation

## Endpoint: Get Feedback by ID

### URL

`GET /feedback/:id`

### Description

This endpoint allows users to retrieve a specific feedback entry by its ID. The response includes the details of the specified feedback entry, and only the user who created the feedback or an admin can access it.

### Authentication

This endpoint requires the user to be authenticated.

### Request Headers

- **Authorization**: Bearer token for authenticated user.

### Request Parameters

- **id** (string, required): The ID of the feedback to be retrieved.

### Request Example

```
GET /feedback/60d9c6b0f1b4d72a8c8b4567
```

### Response

#### Success (200 OK)

If the feedback entry is retrieved successfully, the server responds with a JSON object containing the success status and the feedback data.

##### Response Example

```json
{
  "success": true,
  "data": {
    "_id": "60d9c6b0f1b4d72a8c8b4567",
    "userId": {
      "_id": "60d9c6b0f1b4d72a8c8b4568",
      "firstName": "John",
      "lastName": "Doe"
    },
    "entityId": {
      "_id": "60d9c6b0f1b4d72a8c8b4569",
      "entityName": "Example Entity"
    },
    "name": "John Doe",
    "email": "johndoe@example.com",
    "rating": 5,
    "feedback": "Great service!",
    "createdAt": "2024-07-10T12:34:56.789Z",
    "updatedAt": "2024-07-10T12:34:56.789Z"
  }
}
```

#### Client Error (403 Forbidden)

If a user attempts to access feedback that they did not create, the server responds with a forbidden error message.

##### Response Example

```json
{
  "success": false,
  "message": "You cannot access this feedback"
}
```

#### Client Error (404 Not Found)

If the feedback with the specified ID is not found, the server responds with a not found error message.

##### Response Example

```json
{
  "success": false,
  "message": "Feedback not found"
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

- **403**: You cannot access this feedback.
- **404**: Feedback not found.
- **500**: Internal server error.

### Controller Function

The `getFeedbackById` function handles the retrieval of a specific feedback entry by its ID and performs the necessary validations and operations as described above. Only the user who created the feedback or an admin can access it.