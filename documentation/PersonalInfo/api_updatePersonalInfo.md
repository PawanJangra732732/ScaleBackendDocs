# API Documentation

## Endpoint: Update Personal Information

### URL

`PUT /personal-info`

### Description

This endpoint allows authenticated users to update their personal information. If the user does not have existing personal information, a new entry will be created.

### Authentication

This endpoint requires the user to be authenticated.

### Request Headers

- **Authorization**: Bearer token for authenticated user.
- **Cookie**: Contains the access token.

### Request Body

The request body must be in JSON format and include the necessary personal information fields. The fields will vary depending on what is being updated, but should be validated accordingly.

### Request Example

```json
{
  "firstName": "John",
  "lastName": "Doe",
  "phone": "123-456-7890",
  "dob": "1990-01-01"
}
```

### Response

#### Success (200 OK)

If the personal information is updated successfully, the server responds with a JSON object containing the success status and the updated personal information data.

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

#### Client Error (400 Bad Request)

If there are validation errors in the provided personal information data, the server responds with an error message.

##### Response Example

```json
{
  "success": false,
  "message": "Validation errors",
  "errors": ["Invalid phone number format"]
}
```

#### Client Error (401 Unauthorized)

If the authentication token is not found, the server responds with an unauthorized error message.

##### Response Example

```json
{
  "success": false,
  "message": "Authentication token not found"
}
```

#### Client Error (404 Not Found)

If the user is not found, the server responds with a not found error message.

##### Response Example

```json
{
  "success": false,
  "message": "User not found"
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
- **401**: Authentication token not found.
- **404**: User not found.
- **500**: Internal server error.

### Controller Function

The `handlePersonalInfoUpdate` function handles the updating of personal information for an authenticated user. It performs the necessary validations and operations as described above. If the user does not have existing personal information, a new entry will be created.