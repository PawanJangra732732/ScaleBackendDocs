# API Documentation

## Endpoint: Get User Profiles by Entity ID

### URL

`GET /entity/:entityId/users`

### Description

This endpoint allows superadmins and admins to retrieve user profiles associated with a specific entity. The response includes paginated user profiles with optional search functionality.

### Authentication

This endpoint requires the user to be authenticated.

### Authorization

Only users with the role of `superadmin` or `admin` are authorized to use this endpoint.

### Request Headers

- **Authorization**: Bearer token for authenticated user.
- **Cookie**: Contains the access token.

### Request Parameters

- **entityId** (string, required): The ID of the entity to retrieve users from.

### Query Parameters

- **page** (integer, optional): The page number to retrieve. Defaults to 1.
- **pageSize** (integer, optional): The number of user profiles per page. Defaults to 10.
- **q** (string, optional): A search term to filter user profiles by their first name, last name, email, or entity name.

### Request Example

```
GET /entity/60d9c6b0f1b4d72a8c8b4567/users?page=1&pageSize=10&q=John
```

### Response

#### Success (200 OK)

If the user profiles are retrieved successfully, the server responds with a JSON object containing the success status, paginated user profiles, and pagination details.

##### Response Example

```json
{
  "success": true,
  "data": [
    {
      "_id": "60d9c6b0f1b4d72a8c8b4568",
      "firstName": "John",
      "lastName": "Doe",
      "email": "john.doe@example.com",
      "entityId": "60d9c6b0f1b4d72a8c8b4567",
      "address": [
        {
          "street": "123 Main St",
          "city": "Anytown",
          "state": "Anystate",
          "zip": "12345"
        }
      ],
      "personalInfo": [
        {
          "phone": "123-456-7890",
          "dob": "1990-01-01"
        }
      ],
      "entity": [
        {
          "_id": "60d9c6b0f1b4d72a8c8b4567",
          "entityName": "Example Entity"
        }
      ]
    }
  ],
  "currentPage": 1,
  "totalPages": 2,
  "totalResults": 20
}
```

#### Client Error (400 Bad Request)

If the entity ID format is invalid, the server responds with a bad request error message.

##### Response Example

```json
{
  "success": false,
  "message": "Invalid entity ID format"
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

#### Client Error (403 Forbidden)

If the user does not have the required role, the server responds with a forbidden error message.

##### Response Example

```json
{
  "success": false,
  "message": "Access denied. Only superadmins and admins can perform this action."
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

- **400**: Invalid entity ID format.
- **401**: Authentication token not found.
- **403**: Access denied. Only superadmins and admins can perform this action.
- **404**: Entity not found.
- **500**: Internal server error.

### Controller Function

The `handleGetUserProfilesByEntityId` function handles the retrieval of user profiles associated with a specific entity and performs the necessary validations and operations as described above. It supports pagination and search functionality.