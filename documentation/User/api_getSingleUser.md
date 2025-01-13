# API Documentation: Get Single User

## Endpoint: `/users/:id`

### Method: `GET`

### Description:
This endpoint retrieves the details of a single user by their user ID. The user ID must be a valid ObjectID. If the requesting user is an admin, the endpoint also verifies if the target user is related to the same entity.

### Request Headers:
- `Authorization`: `Bearer <token>` (JWT token for authentication)

### Request Parameters:
- `id`: `string` (User ID)

### Response:
#### Success (200 OK):
- **Content-Type**: `application/json`

```json
{
  "success": true,
  "user": {
    "_id": "string",
    "firstName": "string",
    "lastName": "string",
    "email": "string",
    "mobileNum": "string",
    "role": "string",
    "dateOfBirth": "string",
    "addressId": {
      "street": "string",
      "city": "string",
      "state": "string",
      "zip": "string",
      "country": "string"
    },
    "personalInfoId": {
      "gender": "string",
      "maritalStatus": "string",
      "nationality": "string"
    },
    "entityId": {
      "entityName": "string",
      "entityType": "string"
    }
  }
}
```

#### Error (400 Bad Request):
- **Content-Type**: `application/json`

```json
{
  "success": false,
  "message": "Invalid user ID format"
}
```

#### Error (404 Not Found):
- **Content-Type**: `application/json`

```json
{
  "success": false,
  "message": "User not found with ID: [user ID]"
}
```

#### Error (500 Internal Server Error):
- **Content-Type**: `application/json`

```json
{
  "success": false,
  "message": "Internal Server Error"
}
```

### Error Handling:
- **400 Bad Request**: Returned if the user ID format is invalid.
- **404 Not Found**: Returned if no user is found with the provided ID.
- **500 Internal Server Error**: Returned if there is a server error or an unknown error occurs.

### Implementation Details:
- The function validates the user ID format to ensure it's a valid ObjectID.
- It constructs a query object `_query` to find the user by ID.
- If the requesting user is an admin, it adds an additional condition to the query to verify if the target user is related to the same entity.
- It queries the database to find the user and populates related fields (`addressId`, `personalInfoId`, `entityId`) excluding their `createdAt` and `updatedAt` fields.
- It excludes the `password`, `createdAt`, and `updatedAt` fields from the selected user details.
- If successful, it returns a 200 OK response with the user details.
- If any validation fails or an error occurs, it returns an appropriate error response.

### Example Request:
```bash
curl -X GET https://yourapi.com/users/60d0fe4f5311236168a109ca \
-H "Authorization: Bearer your_jwt_token"
```

### Example Success Response:
```json
{
  "success": true,
  "user": {
    "_id": "60d0fe4f5311236168a109ca",
    "firstName": "John",
    "lastName": "Doe",
    "email": "john.doe@example.com",
    "mobileNum": "1234567890",
    "role": "user",
    "dateOfBirth": "1990-01-01",
    "addressId": {
      "street": "123 Main St",
      "city": "Anytown",
      "state": "Anystate",
      "zip": "12345",
      "country": "USA"
    },
    "personalInfoId": {
      "gender": "male",
      "maritalStatus": "single",
      "nationality": "American"
    },
    "entityId": {
      "entityName": "Example Corp",
      "entityType": "Company"
    }
  }
}
```

### Example Error Responses:
#### Invalid User ID Format:
```json
{
  "success": false,
  "message": "Invalid user ID format"
}
```

#### User Not Found:
```json
{
  "success": false,
  "message": "User not found with ID: 60d0fe4f5311236168a109ca"
}
```

#### Internal Server Error:
```json
{
  "success": false,
  "message": "Internal Server Error"
}
```

### Security Considerations:
- Ensure the user ID format is validated to prevent injection attacks.
- Use HTTPS to transmit sensitive information.
- Implement proper error handling to avoid exposing sensitive information.