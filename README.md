# Node.js CRUD REST API Demo

This project is a simple RESTful API built with Express.js v5 and TypeScript. It demonstrates basic CRUD (Create, Read, Update, Delete) operations and includes features like pagination, error handling, and data validation.

## Features

**Main Features**:

- [x] Typescript
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
- [ ] Logging
- [ ] Unit Testing
- [ ] Docker

**Advanced Features**:

- [ ] GraphQL
- [ ] CI/CD
- [ ] Rate Limiting
- [ ] Pressure Testing

## API Docs

Here’s a classic example of a REST API for managing blog posts using CRUD operations.

- [1. Create](#1-create)
- [2. Read](#2-read)
  - [2.1 Get All Posts with Pagination](#21-get-all-posts-with-pagination)
  - [2.2 Search Posts by Query Parameters](#22-search-posts-by-query-parameters)
  - [2.3 Get a Single Post by ID](#23-get-a-single-post-by-id)
- [3. Update](#3-update)
  - [3.1 Full Update (PUT)](#31-full-update-put)
  - [3.2 Partial Update (PATCH)](#32-partial-update-patch)
- [4. Delete](#4-delete)
- [Notes](#notes)

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

#### 2.1 Get All Posts with Pagination

**HTTP Method**: `GET`

**URL**: `/api/posts?page={page}&size={size}`

**Response**:

```json
{
  "page": 1,
  "size": 25,
  "total_pages": 1,
  "total_posts": 2,
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

#### 2.2 Search Posts by Query Parameters

**HTTP Method**: `GET`

**URL**: `/api/posts?search={query}&page={page}&size={size}`

**Example Request**:

- Search for posts containing the word "AI" in the title or content:

  ```http
  GET /api/posts?search=AI&page=1&size=10
  ```

**Response**:

```json
{
  "page": 1,
  "size": 25,
  "total_pages": 1,
  "total_posts": 2,
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
      "id": 9,
      "title": "The Impact of AI on Healthcare",
      "author": "Ivy Green",
      "content": "Artificial Intelligence is improving healthcare diagnostics and treatment...",
      "published_date": "2024-09-20",
      "tags": ["AI", "Healthcare", "Technology"]
    }
  ]
}
```

**Notes**:

- **Search Parameter**: The `search` query parameter allows users to search for posts based on keywords. The search can be performed on fields like `title`, `content`, or `tags`.
- **Pagination**: The search results are paginated, and the response includes pagination metadata (`page`, `size`, `total_pages`, `total_posts`).
- **Case Sensitivity**: The search should be case-insensitive to ensure that users can find posts regardless of the case used in the query.
- **Error Handling**: If no posts match the search query, return an empty list with appropriate pagination metadata.

This approach allows users to efficiently search for specific posts while still benefiting from pagination for large datasets.

#### 2.3 Get a Single Post by ID

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
