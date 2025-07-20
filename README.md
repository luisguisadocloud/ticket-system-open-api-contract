# Serverless Ticket System - OpenAPI Contract

[![OpenAPI](https://img.shields.io/badge/OpenAPI-3.0.4-brightgreen.svg)](https://swagger.io/specification/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

## 📖 Overview

This repository serves as an educational example demonstrating how to create a comprehensive OpenAPI contract following the OpenAPI specification. The contract defines a **Serverless Ticket System API** designed to be implemented with AWS Lambda and API Gateway.

This project is part of a didactic approach to teach API-First development principles using Swagger Editor as the primary tool for design and validation.

## 🎯 Purpose

The main objectives of this repository are:

- **Educational**: Demonstrate best practices for OpenAPI contract design
- **API-First Approach**: Show how to design APIs before implementation
- **Documentation**: Provide a complete, well-documented API specification
- **Validation**: Showcase proper error handling and response schemas
- **Security**: Demonstrate JWT Bearer token authentication patterns

## 🏗️ Architecture

The API is designed for a serverless architecture with the following characteristics:

- **Backend**: AWS Lambda functions
- **API Gateway**: AWS API Gateway for request routing
- **Authentication**: JWT Bearer token authentication
- **Data Format**: JSON for all requests and responses
- **Status Tracking**: Comprehensive ticket lifecycle management

## 🔧 API Components

### Core Resources

#### Ticket Management
The API revolves around **Ticket** entities, which are digital records used to track and manage support requests, problems, or incidents.

**Ticket Status Lifecycle:**
- `NEW` → `OPEN` → `IN_PROGRESS` → `RESOLVED` → `CLOSED`

**Ticket Priority Levels:**
- `LOW` → `MEDIUM` → `HIGH` → `CRITICAL`

**Ticket Types:**
- `INCIDENT` - Technical issues or problems
- `SERVICE_REQUEST` - Service requests or feature requests
- `QUESTION` - General questions or inquiries

### Endpoints

| Method | Endpoint | Description | Status Codes |
|--------|----------|-------------|--------------|
| `POST` | `/v1/tickets` | Create a new ticket | 201, 400, 401, 500 |
| `GET` | `/v1/tickets` | List all tickets | 200, 401, 500 |
| `GET` | `/v1/tickets/{id}` | Get ticket by ID | 200, 400, 401, 404, 500 |
| `PUT` | `/v1/tickets/{id}` | Update ticket (total replacement) | 200, 400, 401, 404, 500 |
| `PATCH` | `/v1/tickets/{id}` | Update ticket (partial update) | 204, 400, 401, 404, 500 |
| `DELETE` | `/v1/tickets/{id}` | Delete ticket | 204, 400, 401, 404, 500 |

### Data Models

#### Request Schemas
- **CreateTicketRequest**: Required fields for ticket creation (title, description, reporterId)
- **UpdateTicketRequest**: Complete ticket update with all required fields
- **PatchTicketRequest**: Partial ticket updates (any combination of fields)

> **🔒 Security Note**: In a production environment, the `reporterId` field should not be included in the request payload. Instead, it should be automatically extracted from the JWT token's user context to prevent impersonation attacks. The current specification includes `reporterId` in requests for educational purposes and API contract completeness, but real implementations should derive this value from the authenticated user's identity.

#### Response Schemas
- **TicketResponse**: Complete ticket information including:
  - `id`: Unique identifier (UUID)
  - `title`: Brief title describing the issue (1-50 characters)
  - `description`: Detailed description (1-250 characters)
  - `status`: Current status (NEW, OPEN, IN_PROGRESS, RESOLVED, CLOSED)
  - `reporterId`: UUID of the user who reported the ticket
  - `assignedToId`: UUID of the assigned agent (nullable)
  - `priority`: Urgency level (LOW, MEDIUM, HIGH, CRITICAL)
  - `type`: Ticket category (INCIDENT, SERVICE_REQUEST, QUESTION)
  - `createdAt`: Timestamp when ticket was created
  - `updatedAt`: Timestamp when ticket was last updated
- **ListTicketResponse**: Array of tickets
- **ErrorResponse**: Standardized error format with code, message, and optional details

### Security

The API implements **JWT Bearer token authentication**:
- All endpoints require authentication
- Tokens must be provided in the `Authorization` header
- Format: `Bearer <token>`

### Error Handling

Comprehensive error responses for different scenarios:

| Error Type | Code | Description |
|------------|------|-------------|
| `UnauthorizedError` | 401 | Missing or invalid token |
| `NotFoundError` | 404 | Resource not found |
| `BadRequestError` | 400 | Invalid input data or malformed UUID |
| `InternalServerError` | 500 | Unexpected server error |

**Error Response Format:**
```json
{
  "code": "bad_request",
  "message": "Validation failed",
  "details": [
    "Title is required and must be between 1 and 50 characters",
    "Description is required and must be between 1 and 250 characters",
    "Reporter ID must be a valid UUID format"
  ]
}
```

## 🛠️ Development Tools

### Swagger Editor
This contract was designed and validated using [Swagger Editor](https://editor.swagger.io/), which provides:
- Real-time validation
- Interactive documentation
- Code generation capabilities
- Visual API design interface

### Validation
The OpenAPI specification follows version 3.0.4 and includes:
- Schema validation
- Response examples
- Request/response models
- Security definitions

## 📚 Learning Resources

For a detailed explanation of the API-First approach and how this contract was created, visit these articles:

### Part 1: Complete Guide & Introduction
**[API-First Approach: OpenAPI Contract with Swagger](https://blog.luisguisado.cloud/enfoque-api-first-contrato-openapi-swagger/)**
- Introduction to API-First development approach
- Understanding OpenAPI specification and Swagger tools
- Real-world scenario: Technical support ticket management system
- Complete OpenAPI contract with all endpoints and schemas

### Part 2: Detailed Contract Analysis
**[API-First Approach with OpenAPI and Swagger 2: Example Explanation](https://blog.luisguisado.cloud/enfoque-api-first-con-openapi-y-swagger-2-explicacion-del-ejemplo/)**
- Detailed breakdown of each OpenAPI contract section
- Component-by-component analysis of schemas and responses
- Best practices for error handling and response design

## 🚀 Getting Started

### Prerequisites
- Understanding of REST APIs
- Basic knowledge of OpenAPI specification
- Swagger Editor (online or local installation)

### Usage

1. **View the Contract**: Open `openapi.yaml` in Swagger Editor
2. **Explore Endpoints**: Use the interactive documentation
3. **Test Examples**: Try the provided request/response examples
4. **Generate Code**: Use Swagger Codegen for implementation

### Interactive Documentation

You can view the interactive API documentation by:
1. Opening the `openapi.yaml` file in [Swagger Editor](https://editor.swagger.io/)
2. Or using any OpenAPI-compatible documentation generator

## 📋 Project Structure

```
ticket-system-open-api-contract/
├── openapi.yaml          # Main OpenAPI specification
├── README.md            # This file
└── LICENSE              # MIT License
```

## 🤝 Contributing

This is an educational project. Contributions are welcome to improve:
- Documentation clarity
- Additional examples
- Better error handling patterns
- More comprehensive schemas

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 👨‍💻 Author

**Luis Guisado**
- Email: lguisadom@gmail.com
- Blog: [https://blog.luisguisado.cloud](https://blog.luisguisado.cloud)

---

## 🎓 Educational Value

This repository demonstrates:

1. **API Design Principles**: RESTful design patterns with proper HTTP methods
2. **OpenAPI Best Practices**: Proper schema definitions and references
3. **Error Handling**: Comprehensive error response patterns with detailed validation messages
4. **Security**: Authentication and authorization patterns
5. **Documentation**: Self-documenting API contracts with examples
6. **Validation**: Input/output validation schemas with proper constraints
7. **Versioning**: API versioning with `/v1/` prefix
8. **Status Codes**: Proper HTTP status code usage for different scenarios

Suitable for developers learning API design, OpenAPI specification, or preparing for serverless implementations with AWS Lambda and API Gateway. 