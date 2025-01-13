# API Documentation

## Endpoint: Delete Contact Us by ID

### URL

`DELETE /contact-us/:id`

### Description

This endpoint allows users to delete a specific "Contact Us" form submission by its ID. The response includes a success message indicating that the submission has been deleted.

### Authentication

No authentication is required for this endpoint.

### Request Headers

No specific headers are required.

### Request Parameters

- **id** (string, required): The ID of the "Contact Us" form submission to be deleted.

### Request Example

```
DELETE /contact-us/60d9c6b0f1b4d72a8c8b4567
```

### Response

#### Success (200 OK)

If the "Contact Us" form submission is deleted successfully, the server responds with a JSON object containing the success status and a success message.

##### Response Example

```json
{
  "success": true,
  "message": "Contact deleted successfully"
}
```

#### Client Error (404 Not Found)

If the "Contact Us" form submission with the specified ID is not found, the server responds with a not found error message.

##### Response Example

```json
{
  "success": false,
  "message": "Contact not found"
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

- **404**: Contact not found.
- **500**: Internal server error.

### Controller Function

The `handleContactUsDelete` function handles the deletion of a specific "Contact Us" form submission by its ID and performs the necessary validations and operations as described above.