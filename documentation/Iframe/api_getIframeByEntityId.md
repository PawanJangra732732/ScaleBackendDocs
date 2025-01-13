# API Documentation

## Endpoint: Get Iframes by Entity ID

### URL

`GET /admin/iframes-by-entityid`

### Description

This endpoint allows authenticated users with roles (`superadmin`, `admin`, `user`) to retrieve all iframes associated with their `entityId` using pagination support. The response includes a paginated list of iframes along with the total number of iframes, total pages, and the current page.

### Authentication

This endpoint requires the user to be authenticated.

### Authorization

Users with the roles `superadmin`, `admin`, and `user` are authorized to use this endpoint.

### Request Headers

- **Authorization**: Bearer token for authenticated user.
- **Cookie**: Contains the access token.

### Query Parameters

- **page** (integer, optional): The page number to retrieve. Defaults to 1.
- **pageSize** (integer, optional): The number of iframes per page. Defaults to 10.

### Request Example

```
GET /admin/iframes-by-entityid?page=2&pageSize=5
```

### Response

#### Success (200 OK)

If the iframes are retrieved successfully, the server responds with a JSON object containing the success status, the paginated list of iframes, and pagination details.

##### Response Example

```json
{
  "success": true,
  "iframes": [
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
      "entityId": "entity123",
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
  "message": "Error fetching iframes."
}
```

### Errors

- **500**: Internal server error.

### Middleware

- **isAuthenticatedUser**: Ensures the user is authenticated.
- **authorizeRoles("superadmin", "admin", "user")**: Ensures the user has the appropriate role.

### Controller Function

The `getIframeByEntityId` function handles the retrieval of iframes based on the authenticated user's `entityId`. It performs the necessary validations and operations as described above.