# API Documentation

## Endpoint: Delete Feedback

### URL

`DELETE /feedback/:id`

### Description

This endpoint allows users to delete a specific feedback entry by its ID. The response includes a success message indicating that the feedback has been deleted.

### Authentication

This endpoint requires the user to be authenticated.

### Request Headers

- **Authorization**: Bearer token for authenticated user.

### Request Parameters

- **id** (string, required): The ID of the feedback to be deleted.

### Request Example

```
DELETE /feedback/60d9c6b0f1b4d72a8c8b4567
```

### Response

#### Success (200 OK)

If the feedback entry is deleted successfully, the server responds with a JSON object containing the success status and a success message.

##### Response Example

```json
{
  "success": true,
  "message": "Feedback deleted successfully"
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

- **404**: Feedback not found.
- **500**: Internal server error.

### Controller Function

The `deleteFeedback` function handles the deletion of a specific feedback entry by its ID and performs the necessary validations and operations as described above.