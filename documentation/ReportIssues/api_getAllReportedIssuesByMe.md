# API Documentation

## Endpoint: Get All Reports Issued by the Logged-In User

### URL

`GET /my-reports`

### Description

This endpoint allows authenticated users to retrieve all report issues they have issued. The response includes paginated report issues and additional pagination details.

### Authentication

This endpoint requires the user to be authenticated.

### Request Headers

- **Authorization**: Bearer token for authenticated user.

### Query Parameters

- **page** (integer, optional): The page number to retrieve. Defaults to 1.
- **pageSize** (integer, optional): The number of report issues per page. Defaults to 10.
- **q** (string, optional): A search term to filter report issues by their name or email.

### Request Example

```
GET /my-reports?page=1&pageSize=10&q=issue
```

### Response

#### Success (200 OK)

If the report issues are retrieved successfully, the server responds with a JSON object containing the success status, a message, paginated report issues, and pagination details.

##### Response Example

```json
{
  "success": true,
  "message": "All reports issued by the user retrieved successfully",
  "data": [
    {
      "_id": "60d9c6b0f1b4d72a8c8b4567",
      "userId": "60d9c6b0f1b4d72a8c8b4568",
      "entityId": "60d9c6b0f1b4d72a8c8b4569",
      "title": "Issue with the service",
      "description": "I encountered an issue with the service.",
      "priority": "high",
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

The `getAllReportsIssuedByMe` function handles the retrieval of all report issues issued by the authenticated user. It performs the necessary operations as described above, including pagination and search functionality.