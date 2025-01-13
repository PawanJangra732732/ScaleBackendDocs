# API Documentation

## Endpoint: Delete Report Issue

### URL

`DELETE /report-issue/:id`

### Description

This endpoint allows authenticated users to delete a specific report issue entry by its ID. Only the user who created the report or an admin can delete it.

### Authentication

This endpoint requires the user to be authenticated.

### Request Headers

- **Authorization**: Bearer token for authenticated user.

### Request Parameters

- **id** (string, required): The ID of the report issue to be deleted.

### Request Example

```
DELETE /report-issue/60d9c6b0f1b4d72a8c8b4567
```

### Response

#### Success (200 OK)

If the report issue is deleted successfully, the server responds with a JSON object containing the success status and a success message.

##### Response Example

```json
{
  "success": true,
  "message": "Report issue deleted successfully"
}
```

#### Client Error (403 Forbidden)

If a user attempts to delete a report issue that they did not create, the server responds with a forbidden error message.

##### Response Example

```json
{
  "success": false,
  "message": "You cannot delete this feedback"
}
```

#### Client Error (404 Not Found)

If the report issue with the specified ID is not found, the server responds with a not found error message.

##### Response Example

```json
{
  "success": false,
  "message": "Report issue not found"
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

- **403**: You cannot delete this feedback.
- **404**: Report issue not found.
- **500**: Internal server error.

### Controller Function

The `deleteReportIssue` function handles the deletion of a report issue entry for an authenticated user. It performs the necessary validations and operations as described above.