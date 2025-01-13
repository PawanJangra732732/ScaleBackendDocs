# API Documentation for `handleGetUserProfilesByEntityId`

## Description

The `handleGetUserProfilesByEntityId` endpoint allows authenticated admin users to retrieve a paginated list of user profiles associated with their entity. The endpoint supports search functionality by user attributes such as first name, last name, and email. Results are returned in a paginated format with options to specify the page number and page size.

## Endpoint

```
GET /api/v1/admin/user-profiles
```

## Request Headers

- `Content-Type: application/json`
- `Authorization: Bearer <JWT_TOKEN>` (JWT token for authentication)

## Query Parameters

| Parameter  | Type    | Description                                        | Default Value |
|------------|---------|----------------------------------------------------|---------------|
| `page`     | Integer | The page number for pagination.                    | 1             |
| `pageSize` | Integer | The number of users per page.                      | 10            |
| `q`        | String  | Search term to filter users by first name, last name, or email. | ""            |

### Example Request

```
GET /api/v1/admin/user-profiles?page=2&pageSize=20&q=john
```

## Response

### Success Response

- **Status Code:** `200 OK`
- **Body:**

```json
{
  "success": true,
  "results": [
    {
      "_id": "60d21b4667d0d8992e610c85",
      "firstName": "John",
      "lastName": "Doe",
      "email": "john.doe@example.com",
      "addressId": {
        "street": "123 Main St",
        "city": "Anytown",
        "state": "CA",
        "zip": "12345"
      },
      "personalInfoId": {
        "phoneNumber": "555-555-5555",
        "dob": "1990-01-01"
      },
      "entityId": {
        "name": "EntityName",
        "type": "EntityType"
      },
      "createdAt": "2021-06-23T14:48:22.000Z",
      "updatedAt": "2021-06-23T14:48:22.000Z"
    },
    ...
  ],
  "totalResults": 50,
  "totalPages": 5,
  "currentPage": 2
}
```

### Error Responses

- **Status Code:** `401 Unauthorized`
  - **Body:** If the authentication token is missing or invalid.
  
  ```json
  {
    "success": false,
    "message": "Authentication token not found"
  }
  ```

- **Status Code:** `403 Forbidden`
  - **Body:** If the user does not have admin privileges.
  
  ```json
  {
    "success": false,
    "message": "Access denied. Only admins can perform this action."
  }
  ```

- **Status Code:** `500 Internal Server Error`
  - **Body:** If there is an internal server error.
  
  ```json
  {
    "success": false,
    "message": "Internal Server Error"
  }
  ```

## Notes

- This endpoint requires admin privileges.
- The endpoint supports pagination and search functionality.
- Ensure the JWT token is provided in the `Authorization` header to authenticate the request.

---

This API endpoint is part of the admin functionalities, allowing admins to manage and review user profiles associated with their entity effectively with pagination and search capabilities.