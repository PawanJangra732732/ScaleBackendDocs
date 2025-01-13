# API Documentation

## Endpoint: Update Report Issue

### URL

`PUT /report-issue/:id`

### Description

This endpoint allows authenticated users to update an existing report issue entry. Only the user who created the report or an admin can update it.

### Authentication

This endpoint requires the user to be authenticated.

### Request Headers

- **Authorization**: Bearer token for authenticated user.

### Request Parameters

- **id** (string, required): The ID of the report issue to be updated.

### Request Body

The request body must be in JSON format and include the fields that need to be updated.

### Request Example

```json
{
  "title": "Updated issue with the service",
  "description": "I encountered an updated issue with the service.",
  "priority": "medium"
}
```

### Response

#### Success (200 OK)

If the report issue is updated successfully, the server responds with a JSON object containing the success status and the updated report issue data.

##### Response Example

```json
{
  "success": true,
  "reportAnIssue": {
    "_id": "60d9c6b0f1b4d72a8c8b4567",
    "userId": "60d9c6b0f1b4d72a8c8b4568",
    "entityId": "60d9c6b0f1b4d72a8c8b4569",
    "title": "Updated issue with the service",
    "description": "I encountered an updated issue with the service.",
    "priority": "medium",
    "createdAt": "2024-07-10T12:34:56.789Z",
    "updatedAt": "2024-07-10T12:34:56.789Z"
  }
}
```

#### Client Error (403 Forbidden)

If a user attempts to update a report issue that they did not create, the server responds with a forbidden error message.

##### Response Example

```json
{
  "success": false,
  "message": "You cannot update this feedback"
}
```

#### Client Error (404 Not Found)

If the report issue with the specified ID is not found, the server responds with a not found error message.

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

- **403**: You cannot update this feedback.
- **404**: Feedback not found.
- **500**: Internal server error.

### Controller Function

The `updateReportIssue` function handles the updating of a report issue entry for an authenticated user. It performs the necessary validations and operations as described above.