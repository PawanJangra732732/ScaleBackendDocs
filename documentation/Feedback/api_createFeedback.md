## Endpoint: Create Feedback

### URL

`POST /feedback`

### Description

This endpoint allows authenticated users to create feedback. The feedback includes details such as name, email, rating, and feedback message.

### Authentication

This endpoint requires the user to be authenticated.

### Request Headers

- **Authorization**: Bearer token for authenticated user.
- **Cookie**: Contains the access token.

### Request Body

The request body must be in JSON format and include the following fields:

- **name** (string, required): The name of the person providing feedback.
- **email** (string, required): The email address of the person providing feedback.
- **rating** (number, required): The rating provided by the user.
- **feedback** (string, required): The feedback message.

### Request Example

```json
{
  "name": "John Doe",
  "email": "johndoe@example.com",
  "rating": 5,
  "feedback": "Great service!"
}
```

### Response

#### Success (201 Created)

If the feedback is created successfully, the server responds with a JSON object containing the success status and the feedback data.

##### Response Example

```json
{
  "success": true,
  "data": {
    "_id": "60d9c6b0f1b4d72a8c8b4567",
    "userId": "60d9c6b0f1b4d72a8c8b4568",
    "entityId": "60d9c6b0f1b4d72a8c8b4569",
    "name": "John Doe",
    "email": "johndoe@example.com",
    "rating": 5,
    "feedback": "Great service!",
    "createdAt": "2024-07-10T12:34:56.789Z",
    "updatedAt": "2024-07-10T12:34:56.789Z"
  }
}
```

#### Client Error (400 Bad Request)

If there are validation errors in the provided feedback data, the server responds with an error message.

##### Response Example

```json
{
  "success": false,
  "message": "Validation errors",
  "errors": ["Invalid email format"]
}
```

#### Client Error (401 Unauthorized)

If the authentication token is not found, the server responds with an unauthorized error message. Also, if required fields are missing, the server responds with an error message indicating the missing fields.

##### Response Example

```json
{
  "success": false,
  "message": "Authentication token not found"
}
```

##### Response Example

```json
{
  "success": false,
  "field": "name",
  "error": "Please enter your name"
}
```

##### Response Example

```json
{
  "success": false,
  "field": "email",
  "error": "Please enter your email address"
}
```

##### Response Example

```json
{
  "success": false,
  "field": "rating",
  "error": "Please provide a rating"
}
```

##### Response Example

```json
{
  "success": false,
  "field": "feedback",
  "error": "Please provide feedback"
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

- **400**: Validation errors.
- **401**: Authentication token not found or required fields are missing.
- **500**: Internal server error.

### Controller Function

The `createFeedback` function handles the creation of feedback and performs the necessary validations and operations as described above.
