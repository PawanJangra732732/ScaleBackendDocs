### API Documentation: Get All Users Endpoint

#### Endpoint
`GET /api/admin/users`

#### Description
This endpoint allows a superadmin to retrieve a paginated list of all users. The endpoint supports pagination and search functionality.

#### Request

##### Headers
- `Authorization: Bearer <token>` (required): The JWT token for authenticating the superadmin.

##### Query Parameters
- `page` (integer, optional): The page number for pagination. Default is 1.
- `pageSize` (integer, optional): The number of users per page. Default is 10.
- `q` (string, optional): The search term to filter users by first name, last name, or email.

##### Example Request
```
GET /api/admin/users?page=1&pageSize=10&q=john
Authorization: Bearer <token>
```

#### Response

##### Success Response
- **Status Code:** 200 OK
- **Body:**
  ```json
  {
    "success": true,
    "data": [
      {
        "_id": "60c72b2f9e1b8c6d88f6a3b1",
        "firstName": "Pawan",
        "lastName": "Kumar",
        "email": "john.doe@example.com",
        "createdAt": "2021-06-13T12:34:56.789Z"
      },
      {
        "_id": "60c72b2f9e1b8c6d88f6a3b2",
        "firstName": "Ajay",
        "lastName": "Kumar",
        "email": "jane.smith@example.com",
        "createdAt": "2021-06-13T12:34:56.789Z"
      }
    ],
    "totalResults": 50,
    "totalPages": 5,
    "currentPage": 1
  }
  ```

##### Error Responses
- **Unauthorized**
  - **Status Code:** 401 Unauthorized
  - **Body:**
    ```json
    {
      "success": false,
      "message": "Unauthorized"
    }
    ```

- **Internal Server Error**
  - **Status Code:** 500 Internal Server Error
  - **Body:**
    ```json
    {
      "success": false,
      "message": "Internal Server Error"
    }
    ```

#### Implementation Details

**Function Name:** `handleGetAllUser`

**Function Definition:**
```javascript
exports.handleGetAllUser = catchAsyncErrors(async (req, res, next) => {
  try {
    const page = parseInt(req?.query?.page) || 1;
    const pageSize = parseInt(req?.query?.pageSize) || 10;
    const searchTerm = req?.query?.q || "";

    const searchUsers = createSearchFunction(
      User,
      { objectFields: ["_id"], textFields: ["firstName", "lastName", "email"] },
      "",
      {
        createdAt: -1,
      }
    );

    const paginatedResults = await searchUsers(searchTerm, page, pageSize);

    res.status(200).json({
      success: true,
      data: paginatedResults.results,
      totalResults: paginatedResults.totalDocuments,
      totalPages: paginatedResults.totalPages,
      currentPage: paginatedResults.currentPage,
    });
  } catch (error) {
    // Return JSON format error
    res.status(error.statusCode || 500).json({
      success: false,
      message: error.message || "Internal Server Error",
    });
  }
});
```

### Key Points

- **Pagination:** Supports pagination through `page` and `pageSize` query parameters.
- **Search Functionality:** Allows searching users by first name, last name, or email using the `q` query parameter.
- **Error Handling:** Includes error handling for unauthorized access and internal server errors.

#### Call-to-Action
For further assistance or queries, please contact our support team. If you encounter any issues with retrieving the user list, let us know, and we’ll be happy to help! 🚀👥

---
