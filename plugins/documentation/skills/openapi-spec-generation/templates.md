# OpenAPI Templates

Extended templates for common API patterns.

## Complete API Specification

```yaml
openapi: 3.1.0
info:
  title: User Management API
  description: |
    API for managing users and their profiles.

    ## Authentication
    All endpoints require Bearer token authentication.

    ## Rate Limiting
    - 1000 requests per minute for standard tier
    - 10000 requests per minute for enterprise tier
  version: 2.0.0
  contact:
    name: API Support
    email: api-support@example.com
  license:
    name: MIT

servers:
  - url: https://api.example.com/v2
    description: Production
  - url: https://staging-api.example.com/v2
    description: Staging

tags:
  - name: Users
    description: User management operations
  - name: Profiles
    description: User profile operations

paths:
  /users:
    get:
      operationId: listUsers
      summary: List all users
      tags: [Users]
      parameters:
        - $ref: '#/components/parameters/PageParam'
        - $ref: '#/components/parameters/LimitParam'
      responses:
        '200':
          description: Success
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/UserList'
    post:
      operationId: createUser
      summary: Create a new user
      tags: [Users]
      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/CreateUser'
      responses:
        '201':
          description: Created
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/User'

  /users/{id}:
    get:
      operationId: getUser
      summary: Get user by ID
      tags: [Users]
      parameters:
        - $ref: '#/components/parameters/UserIdParam'
      responses:
        '200':
          description: Success
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/User'
        '404':
          $ref: '#/components/responses/NotFound'

components:
  schemas:
    User:
      type: object
      required: [id, email, createdAt]
      properties:
        id:
          type: string
          format: uuid
        email:
          type: string
          format: email
        name:
          type: string
        createdAt:
          type: string
          format: date-time

    CreateUser:
      type: object
      required: [email]
      properties:
        email:
          type: string
          format: email
        name:
          type: string

    UserList:
      type: object
      properties:
        data:
          type: array
          items:
            $ref: '#/components/schemas/User'
        pagination:
          $ref: '#/components/schemas/Pagination'

    Pagination:
      type: object
      properties:
        page:
          type: integer
        limit:
          type: integer
        total:
          type: integer
        hasMore:
          type: boolean

    Error:
      type: object
      required: [code, message]
      properties:
        code:
          type: string
        message:
          type: string
        details:
          type: array
          items:
            type: object

  parameters:
    UserIdParam:
      name: id
      in: path
      required: true
      schema:
        type: string
        format: uuid
    PageParam:
      name: page
      in: query
      schema:
        type: integer
        minimum: 1
        default: 1
    LimitParam:
      name: limit
      in: query
      schema:
        type: integer
        minimum: 1
        maximum: 100
        default: 20

  responses:
    NotFound:
      description: Resource not found
      content:
        application/json:
          schema:
            $ref: '#/components/schemas/Error'
          example:
            code: NOT_FOUND
            message: The requested resource was not found

  securitySchemes:
    BearerAuth:
      type: http
      scheme: bearer
      bearerFormat: JWT

security:
  - BearerAuth: []
```

## Webhook Specification

```yaml
webhooks:
  userCreated:
    post:
      operationId: onUserCreated
      summary: User created webhook
      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/UserEvent'
      responses:
        '200':
          description: Webhook processed
```

## File Upload Endpoint

```yaml
paths:
  /files:
    post:
      operationId: uploadFile
      summary: Upload a file
      requestBody:
        required: true
        content:
          multipart/form-data:
            schema:
              type: object
              properties:
                file:
                  type: string
                  format: binary
                description:
                  type: string
      responses:
        '201':
          description: File uploaded
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/File'
```
