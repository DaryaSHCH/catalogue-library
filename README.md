### catalogue-library ###
Designing a REST API of library catalogue (done as part of the training)

## Functional Requirements

### Working with Books
- **List view**: Retrieve a list of all books. Supports filtering by `genre`.
- **Book details**: Retrieve full information about a specific book by its `id`.
- **Management (Admin only)**: 
  - `POST`: Add a new book.
  - `PUT`: Update existing book details.
  - `DELETE`: Remove a book from the catalog.

### Working with Authors
- **List view**: Retrieve a list of all authors.
- **Author profile**: View an author's biography and the collection of books linked to them.

### Status and Reservation
- **Availability**: Every book tracks its status via an `is_available` flag.
- **Reservation**: A partial update (`PATCH`) to change the status to "reserved".

---

## Non-Functional Requirements

- **Data Format**: All request and response bodies must use `application/json`.
- **Pagination**: Implemented for all collection endpoints (e.g., `/books`, `/authors`) using `page` and `limit` query parameters.
- **Security**:
  - **Public Access**: All `GET` requests are open to the public.
  - **Restricted Access**: `POST`, `PUT`, and `DELETE` operations require a valid **JWT (JSON Web Token)**.
- **Caching**: 
  - Use `Cache-Control` headers for static/semi-static data (e.g., Genres and Author Bio).
- **Richardson Maturity Model**: The API is designed at **Level 2** (Resources + HTTP Verbs).
