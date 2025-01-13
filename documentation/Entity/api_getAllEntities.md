# API Documentation

## Endpoint: Get All Entities

### URL

`GET /entities`

### Description

This endpoint allows users to retrieve a paginated list of all entities. The results can be filtered using a search term.

### Authentication

No authentication is required for this endpoint.

### Request Headers

No specific headers are required.

### Query Parameters

- **page** (integer, optional): The page number to retrieve. Defaults to 1.
- **pageSize** (integer, optional): The number of entities per page. Defaults to 10.
- **q** (string, optional): The search term to filter entities by their name.

### Request Example

```
GET /entities?page=2&pageSize=5&q=example
```

### Response

#### Success (200 OK)

If the entities are retrieved successfully, the server responds with a JSON object containing the success status, the paginated list of entities, and pagination details.

##### Response Example

```json
{
  "success": true,
  "data": [
    {
      "_id": "60d9c6b0f1b4d72a8c8b4567",
      "entityName": "Example Entity",
      "createdAt": "2024-07-10T12:34:56.789Z",
      "updatedAt": "2024-07-10T12:34:56.789Z"
    },
    {
      "_id": "60d9c6b0f1b4d72a8c8b4568",
      "entityName": "Another Entity",
      "createdAt": "2024-07-11T12:34:56.789Z",
      "updatedAt": "2024-07-11T12:34:56.789Z"
    }
  ],
  "totalResults": 20,
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

### Controller Function

The `handleGetAllEntities` function handles the retrieval of all entities with pagination and search functionality. It performs the necessary validations and operations as described above.