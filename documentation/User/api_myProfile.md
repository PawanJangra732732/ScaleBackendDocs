# API Documentation: Get My Profile

## Endpoint: `/my-profile`

### Method: `GET`

### Description:
This endpoint is used to retrieve the profile information of the authenticated user. It returns detailed information about the user's profile, including personal information, address, and associated entity details.

### Request Headers:
- `Authorization`: `Bearer <token>` (JWT token for authentication)

### Request Body:
- None

### Response:
#### Success (200 OK):
- **Content-Type**: `application/json`

```json
{
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
```

#### Error (404 Not Found):
- **Content-Type**: `application/json`

```json
{
  "error": "User not found"
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
- **404 Not Found**: Returned if the user is not found in the database.
- **500 Internal Server Error**: Returned if there is a server error or an unknown error occurs.

### Implementation Details:
- The function retrieves the user ID from the authenticated user's token.
- It queries the database for the user by ID.
- It populates related fields (`addressId`, `personalInfoId`, `entityId`) excluding their `createdAt` and `updatedAt` fields.
- It selects specific fields (`_id`, `firstName`, `lastName`, `email`, `mobileNum`, `role`, `dateOfBirth`) to include in the response