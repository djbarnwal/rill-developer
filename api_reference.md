# API Reference

This document provides a comprehensive API reference for Rill, including all available endpoints, their parameters, return values, and example usage. The API is organized by service and includes information on authentication and error handling.

## Table of Contents

1. [Authentication](#authentication)
2. [Error Handling](#error-handling)
3. [RuntimeService](#runtimeservice)
4. [AdminService](#adminservice)

## Authentication

[Include information about authentication methods and requirements]

## Error Handling

[Describe common error codes, their meanings, and how to handle them]

## RuntimeService

The RuntimeService provides endpoints for managing runtime operations in Rill.

### Method: ExampleMethod

Description of the ExampleMethod and its purpose.

**Request:**

```protobuf
message ExampleRequest {
  string example_field = 1;
}
```

**Response:**

```protobuf
message ExampleResponse {
  string result = 1;
}
```

**Parameters:**

- `example_field` (string): Description of the example field.

**Returns:**

- `result` (string): Description of the result.

**Example Usage:**

```go
client := rill.NewRuntimeServiceClient(conn)
resp, err := client.ExampleMethod(ctx, &rill.ExampleRequest{
    ExampleField: "example value",
})
if err != nil {
    // Handle error
}
fmt.Printf("Result: %s\n", resp.Result)
```

[Include additional methods for RuntimeService]

## AdminService

The AdminService provides endpoints for administrative operations in Rill.

### Method: ExampleAdminMethod

Description of the ExampleAdminMethod and its purpose.

**Request:**

```protobuf
message ExampleAdminRequest {
  string admin_field = 1;
}
```

**Response:**

```protobuf
message ExampleAdminResponse {
  string admin_result = 1;
}
```

**Parameters:**

- `admin_field` (string): Description of the admin field.

**Returns:**

- `admin_result` (string): Description of the admin result.

**Example Usage:**

```go
adminClient := rill.NewAdminServiceClient(conn)
resp, err := adminClient.ExampleAdminMethod(ctx, &rill.ExampleAdminRequest{
    AdminField: "admin value",
})
if err != nil {
    // Handle error
}
fmt.Printf("Admin Result: %s\n", resp.AdminResult)
```

[Include additional methods for AdminService]