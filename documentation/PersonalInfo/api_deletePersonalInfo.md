# API Documentation

## Endpoint: Delete Personal Information by ID

### URL

`DELETE /personal-info/:id`

### Description

This endpoint allows users to delete personal information by its ID. The response includes a success message indicating that the personal information has been deleted.

### Authentication

This endpoint requires the user to be authenticated.

### Request Headers

- **Authorization**: Bearer token for authenticated user.

### Request Parameters

- **id** (string, required): The ID of the personal information to be deleted.

### Request Example

```
DELETE /personal-info/60d9c6b0f1b4d72a8c8b4567
```

### Response

#### Success (200 OK)

If the personal information is deleted successfully, the server responds with a JSON object containing the success status and a success message.

##### Response Example

```json
{
  "success": true,
  "message": "Deleted successfully"
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

The `handlePersonalInfoDelete` function handles the deletion of personal information by its ID and performs the necessary validations and operations as described above.