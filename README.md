# express-crud

This project is a simple RESTful API built with Express.js v5 and TypeScript. It demonstrates basic CRUD (Create, Read, Update, Delete) operations and includes features like pagination, error handling, and data validation.

## Features

**Main Features**:

- [ ] CRUD
  - [ ] POST
  - [ ] GET
  - [ ] PUT/PATCH
  - [ ] DELETE
- [ ] DataBase/ORM
  - [ ] MySQL
  - [ ] PostgreSQL
  - [ ] MongoDB
- [ ] MVC
- [ ] Cors
- [ ] Auth
- [ ] Swagger
- [ ] Typescript
- [ ] Logging
- [ ] Docker
- [ ] Unit Testing

**Optional Features**:

- [ ] GraphQL
- [ ] CI/CD
- [ ] Rate Limiting
- [ ] Pressure Testing

## API Docs

- [1. Create](#1-create)
- [2. Read](#2-read)
  - [2.1 Get All Posts](#21-get-all-posts)
  - [2.2 Get a Single Post by ID](#22-get-a-single-post-by-id)
- [3. Update](#3-update)
  - [3.1 Full Update (PUT)](#31-full-update-put)
  - [3.2 Partial Update (PATCH)](#32-partial-update-patch)
- [4. Delete](#4-delete)
- [Notes](#notes)

Here’s a classic example of a REST API for managing blog posts using CRUD operations.

### 1. Create

**HTTP Method**: `POST`

**URL**: `/api/posts`

**Request Body**:

```json
{
  "title": "The Future of Artificial Intelligence",
  "author": "John Doe",
  "content": "Artificial Intelligence is rapidly changing the world...",
  "published_date": "2025-05-01",
  "tags": ["AI", "Technology", "Future"]
}
```

**Response**:

```json
{
  "id": 1,
  "title": "The Future of Artificial Intelligence",
  "author": "John Doe",
  "content": "Artificial Intelligence is rapidly changing the world...",
  "published_date": "2025-05-01",
  "tags": ["AI", "Technology", "Future"]
}
```

### 2. Read

#### 2.1 Get All Posts

**HTTP Method**: `GET`

**URL**: `/api/posts?page={page}&size={size}`

**Response**:

```json
{
  "page": 1,
  "size": 2,
  "total_pages": 5,
  "total_posts": 10,
  "posts": [
    {
      "id": 1,
      "title": "The Future of Artificial Intelligence",
      "author": "John Doe",
      "content": "Artificial Intelligence is rapidly changing the world...",
      "published_date": "2025-05-01",
      "tags": ["AI", "Technology", "Future"]
    },
    {
      "id": 2,
      "title": "The Benefits of Renewable Energy",
      "author": "Jane Smith",
      "content": "Renewable energy sources are essential for a sustainable future...",
      "published_date": "2025-04-20",
      "tags": ["Environment", "Energy", "Sustainability"]
    }
  ]
}
```

**Notes**:

- **Pagination**: The response includes pagination metadata (`page`, `size`, `total_pages`, `total_posts`) to help clients navigate through the posts.
- **Default Values**: If `page` or `size` parameters are not provided, default values can be set (e.g., `page=1`, `size=25`).
- **Error Handling**: If the requested page is out of range, an appropriate error message can be returned.

#### 2.2 Get a Single Post by ID

**HTTP Method**: `GET`

**URL**: `/api/posts/{id}` (e.g., `/api/posts/1`)

**Response**:

```json
{
  "id": 1,
  "title": "The Future of Artificial Intelligence",
  "author": "John Doe",
  "content": "Artificial Intelligence is rapidly changing the world...",
  "published_date": "2025-05-01",
  "tags": ["AI", "Technology", "Future"]
}
```

### 3. Update

#### 3.1 Full Update (PUT)

**HTTP Method**: `PUT`

**URL**: `/api/posts/{id}` (e.g., `/api/posts/1`)

**Request Body**:

```json
{
  "title": "The Future of Artificial Intelligence",
  "author": "John Doe",
  "content": "Artificial Intelligence is rapidly changing the world. New advancements are being made every day...",
  "published_date": "2025-05-01",
  "tags": ["AI", "Technology", "Future"]
}
```

**Response**:

```json
{
  "id": 1,
  "title": "The Future of Artificial Intelligence",
  "author": "John Doe",
  "content": "Artificial Intelligence is rapidly changing the world. New advancements are being made every day...",
  "published_date": "2025-05-01",
  "tags": ["AI", "Technology", "Future"]
}
```

#### 3.2 Partial Update (PATCH)

**HTTP Method**: `PATCH`

**URL**: `/api/posts/{id}` (e.g., `/api/posts/1`)

**Request Body**:

```json
{
  "content": "Artificial Intelligence is rapidly changing the world. New advancements are being made every day, and its impact is felt across various industries..."
}
```

**Response**:

```json
{
  "id": 1,
  "title": "The Future of Artificial Intelligence",
  "author": "John Doe",
  "content": "Artificial Intelligence is rapidly changing the world. New advancements are being made every day, and its impact is felt across various industries...",
  "published_date": "2025-05-01",
  "tags": ["AI", "Technology", "Future"]
}
```

**Notes**:

- **Validation**: Ensure that the request body contains valid data and that the fields being updated are allowed to be modified.
- **Error Handling**: If the post with the specified ID does not exist, return a `404 Not Found` status code. If the request body is invalid, return a `400 Bad Request` status code.

### 4. Delete

**HTTP Method**: `DELETE`

**URL**: `/api/posts/{id}` (e.g., `/api/posts/1`)

**Response**:

```json
{
  "message": "Post with ID 1 has been deleted successfully."
}
```

### Notes

- **Status Codes**: In practice, you should return appropriate HTTP status codes based on the success or failure of the operation, such as:
  - Create successful: `201 Created`
  - Retrieve successful: `200 OK`
  - Update successful: `200 OK`
  - Delete successful: `200 OK` or `204 No Content`
  - Resource not found: `404 Not Found`
  - Bad request: `400 Bad Request`
- **Security**: In real applications, consider authentication and authorization to ensure that only authorized users can perform these operations.
