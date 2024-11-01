# ForumEngine
* [About](#about)
* [Tech stack](#tech-stack)
* [API documentation](#api-documentation)
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

### Database
* MySQL

### Testing
Unit & integration tests
* JUnit 5
* Mockito
* SpringBootTest
* Testcontainers

### Containerization
* Docker
* Two containers are configured in the `docker-compose.yml` file:
  - **mysql_db**: MySQL 8.0 database
  - **backend**: Java 17 (Spring Boot) application

### CI/CD
This repository uses **GitHub Actions** for automatic building and testing on every `push` and `pull request` to the `master` branch.

## API documentation
The application generates interactive API documentation (Swagger UI).
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

| #  | Method | Endpoint                   | Description                   | Authorization            |
|----|--------|----------------------------|-------------------------------|--------------------------|
| 1  | POST   | `/auth/register`           | User registration             | No                       |
| 2  | POST   | `/auth/login`              | User login                    | No                       |
| 3  | GET    | `/categories`              | Get all categories            | No                       |
| 4  | POST   | `/categories`              | Add a new category            | Yes (admin)              |
| 5  | GET    | `/categories/{id}`         | Get category by ID            | No                       |
| 6  | DELETE | `/categories/{id}`         | Delete category by ID         | Yes (admin)              |
| 7  | POST   | `/posts`                   | Add a new post                | Yes (authenticated user) |
| 8  | GET    | `/posts`                   | Get all posts                 | No                       |
| 9  | GET    | `/posts/{id}`              | Get post by ID                | No                       |
| 10 | DELETE | `/posts/{id}`              | Delete post by ID             | Yes (authenticated user) |
| 11 | POST   | `/posts/{postId}/comments` | Add a new comment to the post | Yes (authenticated user) |

### Security
To access some resources you need to use `header` authorization.

```
Authorization: Bearer <token>
```

The token can be generated using POST `/login` endpoint.

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

### 11. Add a new comment to the post

**Endpoint:** `/posts/{postId}/comments`

**Method:** `POST`

**Request body:**

```json
{
  "content": "Example comment content"
}
```