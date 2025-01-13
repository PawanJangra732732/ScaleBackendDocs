# API Documentation

## Endpoint: Get All Iframes

### URL

`GET /admin/iframe`

### Description

This endpoint allows a superadmin user to retrieve all iframes with pagination support. The response includes a paginated list of iframes along with the total number of iframes, total pages, and the current page.

### Authentication

This endpoint requires the user to be authenticated.

### Authorization

Only users with the `superadmin` role are authorized to use this endpoint.

### Request Headers

- **Authorization**: Bearer token for authenticated user.

### Query Parameters

- **page** (integer, optional): The page number to retrieve. Defaults to 1.
- **pageSize** (integer, optional): The number of iframes per page. Defaults to 10.

### Request Example

```
GET /admin/iframe?page=2&pageSize=5
```

### Response

#### Success (200 OK)

If the iframes are retrieved successfully, the server responds with a JSON object containing the success status, a success message, and the paginated list of iframes along with pagination details.

##### Response Example

```json
{
  "success": true,
  "message": "All iframes retrieved successfully",
  "data": [
    {
      "_id": "60d9c6b0f1b4d72a8c8b4567",
      "slug": "iframe-slug-1",
      "reportId": "report123",
      "groupId": "group123",
      "entityId": "entity123",
      "createdBy": "60c72b1f4f1b4d72a8c8b123",
      "createdAt": "2024-07-10T12:34:56.789Z",
      "updatedAt": "2024-07-10T12:34:56.789Z"
    },
    {
      "_id": "60d9c6b0f1b4d72a8c8b4568",
      "slug": "iframe-slug-2",
      "reportId": "report124",
      "groupId": "group124",
      "entityId": "entity124",
      "createdBy": "60c72b1f4f1b4d72a8c8b124",
      "createdAt": "2024-07-11T12:34:56.789Z",
      "updatedAt": "2024-07-11T12:34:56.789Z"
    }
  ],
  "totalIframes": 20,
  "totalPages": 4,
  "currentPage": 2
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

### Middleware

- **isAuthenticatedUser**: Ensures the user is authenticated.
- **authorizeRoles("superadmin")**: Ensures the user has the `superadmin` role.

### Controller Function

The `handleGetAllIframes` function handles the retrieval of all iframes and performs the necessary pagination and operations as described above.