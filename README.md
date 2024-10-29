# ForumEngine
* [About](#about)
* [Tech stack](#tech-stack)
* [Starting up](#starting-up)
* [Endpoints](#endpoints)

## About
This REST API application built using Spring Boot and Java allows you to manage an online forum.

## Tech stack
### Backend
* Java 17
* Spring Boot 3.3.2
* Spring Data JPA
* Spring Security
* Lombok
* MySQL

### Testing
Unit & integration tests
* JUnit 5
* Mockito
* SpringBootTest
* Testcontainers

### API documentation
Generate interactive API documentation (Swagger UI).
* SpringDoc OpenAPI
```
http://localhost:8080/swagger-ui/index.html
```

## Starting up
To launch the application, follow the steps:
1. Clone project
```
git clone https://github.com/jchojdak/ForumEngine.git
```
2. Open cloned directory
```
cd ForumEngine
```
3. Start the application using docker-compose
```
docker-compose up -d
```

## Endpoints

| Method | Endpoint           | Description           | Authorization            |
|--------|--------------------|-----------------------|--------------------------|
| POST   | `/auth/register`   | User registration     | No                       |
| POST   | `/auth/login`      | User login            | No                       |
| GET    | `/categories`      | Get all categories    | No                       |
| POST   | `/categories`      | Add a new category    | Yes (admin)              |
| GET    | `/categories/{id}` | Get category by ID    | No                       |
| DELETE | `/categories/{id}` | Delete category by ID | Yes (admin)              |
| POST   | `/posts`           | Add a new post        | Yes (authenticated user) |
| GET    | `/posts`           | Get all posts         | No                       |
| GET    | `/posts/{id}`      | Get post by ID        | No                       |
| DELETE | `/posts/{id}`      | Delete post by ID     | Yes (authenticated user) |

### 1. User registration

**Endpoint:** `/auth/register`

**Method:** `POST`

**Request body:**

```json
{
  "username": "example",
  "password": "ExamplePassword",
  "email": "example.example@gmail.com"
}
```

### 2. User login

**Endpoint:** `/auth/login`

**Method:** `POST`

**Request body:**

```json
{
  "username": "example",
  "password": "ExamplePassword"
}
```

### 3. Get all categories

**Endpoint:** `/categories`

**Method:** `GET`

### 4. Add a new category

**Endpoint:** `/categories`

**Method:** `POST`

**Request body:**

```json
{
  "name": "exampleNameOfCategory",
  "description": "exampleDescription"
}
```

### 5. Get category by ID

**Endpoint:** `/categories/{id}`

**Method:** `GET`

### 6. Delete category by ID

**Endpoint:** `/categories/{id}`

**Method:** `DELETE`

### 7. Add a new post

**Endpoint:** `/posts`

**Method:** `POST`

**Request body:**

```json
{
  "categoryId": 1,
  "title": "Example post title",
  "content": "Example post content"
}
```

### 8. Get all posts

**Endpoint:** `/posts`

**Method:** `GET`

**Request parameters:**
- `page` (Integer, optional): The page number to retrieve. Default value is 0.
- `size` (Integer, optional): The number of posts per page. Default value is 10.
- `sort` (Sort.Direction, optional): The sorting direction. Default value is ASC.

*Example:* `/posts?page=3&size=20&sort=DESC`

### 9. Get post by ID

**Endpoint:** `/posts/{id}`

**Method:** `GET`

### 10. Delete post by ID

**Endpoint:** `/posts/{id}`

**Method:** `DELETE`