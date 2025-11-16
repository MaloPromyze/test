# API Response Formatting

This standard defines a consistent structure for API responses across all endpoints, including success responses, error responses, and pagination metadata. It ensures predictable response formats that enable easier client-side integration and error handling.

## Rules

* Always return responses in a consistent structure with data, error, and metadata fields
* Use appropriate HTTP status codes and include error details in the response body
* Include pagination metadata for list endpoints using a standard pagination structure
