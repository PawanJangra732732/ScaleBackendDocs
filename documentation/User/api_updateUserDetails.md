# API Documentation: Update User Details

## Endpoint: `/update-user-details`

### Method: `PUT`

### Description:
This endpoint is used to update the authenticated user's profile details. The user can update their first name, last name, email, and date of birth. At least one field must be provided for the update.

### Request Headers:
- `Authorization`: `Bearer <token>` (JWT token for authentication)
- `Content-Type`: `application/json`

### Request Body:
```json
{
  "firstName": "string",
  "lastName": "string",
  "email": "string",
  "dateOfBirth": "string"
}
```

| Field       | Type   | Description                        |
| ----------- | ------ | ---------------------------------- |
| firstName   | string | The first name of the user.        |
| lastName    | string | The last name of the user.         |
| email       | string | The email address of the user.     |
| dateOfBirth | string | The date of birth of the user.     |

### Response:
#### Success (200 OK):
- **Content-Type**: `application/json`

```json
{
  "success": true,
  "message": "Your details have been updated"
}
```

#### Error (400 Bad Request):
- **Content-Type**: `application/json`

```json
{
  "error": "At least one field is required to update."
}
```

#### Error (404 Not Found):
- **Content-Type**: `application/json`

```json
{
  "success": false,
  "message": "User not found"
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
- **400 Bad Request**: Returned if no fields are provided in the request body for updating.
- **404 Not Found**: Returned if the user is not found in the database.
- **500 Internal Server Error**: Returned if there is a server error or an unknown error occurs.

### Implementation Details:
- The function retrieves the user ID from the authenticated user's token.
- It extracts the fields (`firstName`, `lastName`, `email`, `dateOfBirth`) from the request body.
- It checks if at least one field is provided for the update.
- It queries the database for the user by ID.
- If the user is found, it updates the user's details in the database using `findByIdAndUpdate`.
- If successful, it returns a 200 OK response with a success message.
- If any validation fails or an error occurs, it returns an appropriate error response.

### Example Request:
```bash
curl -X PUT https://yourapi.com/update-user-details \
-H "Authorization: Bearer your_jwt