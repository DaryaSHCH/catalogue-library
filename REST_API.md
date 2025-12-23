#### REST API Design

This section describes the REST API for the Library Catalogue System. The API follows REST principles and uses JSON as the data format.

## Books

### GET /books

**Description:**  
Get a list of all books.

**Query Parameters:**
- `page` (number) – page number  
- `limit` (number) – number of items per page  
- `genre` (string, optional) – filter books by genre  

**Response:**
- `200 OK` – list of books returned  

**Authentication:**  
Not required

**Pagination:**  
Required

**Caching:**  
Not cached (data may change often)

---

### GET /books/{id}

**Description:**  
Get full information about a book by its ID.

**Path Parameters:**
- `id` – book ID  

**Response:**
- `200 OK` – book found  
- `404 Not Found` – book does not exist  

**Authentication:**  
Not required

**Caching:**  
Not cached

---

### POST /books

**Description:**  
Create a new book.

**Request Body (JSON):**
- `title`
- `description`
- `genre`
- `author_id`
- `published_year`

**Response:**
- `201 Created` – book created  
- `400 Bad Request` – invalid input  
- `401 Unauthorized` – no JWT token  
- `403 Forbidden` – user is not an admin  

**Authentication:**  
Required (JWT, admin only)

---

### PUT /books/{id}

**Description:**  
Update an existing book.

**Path Parameters:**
- `id` – book ID  

**Request Body (JSON):**
- updated book fields  

**Response:**
- `200 OK` – book updated  
- `400 Bad Request` – invalid data  
- `401 Unauthorized` – no JWT token  
- `403 Forbidden` – not an admin  
- `404 Not Found` – book not found  

**Authentication:**  
Required (JWT, admin only)

---

### DELETE /books/{id}

**Description:**  
Delete a book by its ID.

**Path Parameters:**
- `id` – book ID  

**Response:**
- `204 No Content` – book deleted  
- `401 Unauthorized` – no JWT token  
- `403 Forbidden` – not an admin  
- `404 Not Found` – book not found  

**Authentication:**  
Required (JWT, admin only)

---

### PATCH /books/{id}/reserve

**Description:**  
Reserve a book. Changes `is_available` to `false`.

**Path Parameters:**
- `id` – book ID  

**Response:**
- `200 OK` – book reserved  
- `400 Bad Request` – book already reserved  
- `401 Unauthorized` – no JWT token  
- `404 Not Found` – book not found  

**Authentication:**  
Required (JWT)

---

## Authors

### GET /authors

**Description:**  
Get a list of all authors.

**Query Parameters:**
- `page` – page number  
- `limit` – number of items per page  

**Response:**
- `200 OK` – list of authors  

**Authentication:**  
Not required

**Pagination:**  
Required

**Caching:**  
Cached (`Cache-Control: max-age=3600`)

---

### GET /authors/{id}

**Description:**  
Get an author profile with biography and list of books.

**Path Parameters:**
- `id` – author ID  

**Response:**
- `200 OK` – author found  
- `404 Not Found` – author not found  

**Authentication:**  
Not required

**Caching:**  
Cached (`Cache-Control: max-age=3600`)

---

## Genres

### GET /genres

**Description:**  
Get a list of all genres.

**Response:**
- `200 OK` – list of genres  

**Authentication:**  
Not required

**Caching:**  
Cached (`Cache-Control: max-age=86400`)

---

## Authentication

**Authentication Method:**  
JWT (JSON Web Token)

**Header Format:**
Authorization: Bearer <token>

markdown
Copy code

**Rules:**
- `GET` requests are public  
- `POST`, `PUT`, `DELETE`, `PATCH` require JWT  
- Admin role is required for book management  

**Errors:**
- `401 Unauthorized` – token missing or invalid  
- `403 Forbidden` – not enough permissions  

---

## Error Handling

All errors are returned in **JSON** format.

**Example Error Response:**
```json
{
  "status": 404,
  "message": "Book not found"
}
