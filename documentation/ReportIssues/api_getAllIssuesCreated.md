# API Documentation

## Endpoint: Get All Issues Created (Superadmin Only)

### URL

`GET /report-issues`

### Description

This endpoint allows a superadmin to retrieve all report issues created. The response includes paginated report issues and additional pagination details.

### Authentication

This endpoint requires the user to be authenticated.

### Authorization

Only users with the role of `superadmin` are authorized to use this endpoint.

### Request Headers

- **Authorization**: Bearer token for authenticated user.

### Query Parameters

- **page** (integer, optional): The page number to retrieve. Defaults to 1.
- **pageSize** (integer, optional): The number of report issues per page. Defaults to 10.

### Request Example

```
GET /report-issues?page=1&pageSize=10
```

### Response

#### Success (200 OK)

If the report issues are retrieved successfully, the server responds with a JSON object containing the success status, a message, paginated report issues, and pagination details.

##### Response Example

```json
{
  "success": true,
  "issues": [
    {
      "_id": "60d9c6b0f1b4d72a8c8b4567",
      "userId": "60d9c6b0f1b4d72a8c8b4568",
      "entityId": "60d9c6b0f1b4d72a8c8b4569",
      "title": "Issue with the service",
      "description": "I encountered an issue with the service.",
      "priority": "high",
      "status": "submitted",
      "createdAt": "2024-07-10T12:34:56.789Z",
      "updatedAt": "2024-07-10T12:34:56.789Z"
    },
    {
      "_id": "60d9c6b0f1b4d72a8c8b4570",
      "userId": "60d9c6b0f1b4d72a8c8b4568",
      "entityId": "60d9c6b0f1b4d72a8c8b4569",
      "title": "Another issue",
      "description": "I encountered another issue.",
      "priority": "medium",
      "status": "submitted",
      "createdAt": "2024-07-11T12:34:56.789Z",
      "updatedAt": "2024-07-11T12:34:56.789Z"
    }
  ],
  "totalResults": 2,
  "totalPages": 1,
  "currentPage": 1
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

- **500**: Internal server error.

### Controller Function

The `getAllIssuesCreated` function handles the retrieval of all report issues created with pagination. It performs the necessary operations as described above.