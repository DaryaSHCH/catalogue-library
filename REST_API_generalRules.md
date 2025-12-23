# Common API Rules

This document describes common rules and conventions used across the API.

---

## Status Codes

The API uses the following HTTP status codes:

- **400 Bad Request** – the request data is invalid
- **401 Unauthorized** – authentication token is missing or invalid
- **403 Forbidden** – the user does not have enough permissions
- **404 Not Found** – the requested resource does not exist
- **500 Internal Server Error** – unexpected server error

---

## Richardson Maturity Model

The API follows **Level 2** of the Richardson Maturity Model:

- Resources are identified by **URI**
- HTTP methods (`GET`, `POST`, `PUT`, `DELETE`, `PATCH`) are used correctly
- No HATEOAS links are implemented

---

## Pagination

Pagination is implemented using query parameters:

- `page` – page number
- `limit` – number of items per page

Pagination is used in:
- `GET /books`
- `GET /authors`

---

## Caching

Caching is implemented using HTTP headers:

- `Cache-Control`

Cached endpoints:
- `GET /authors`
- `GET /authors/{id}`
- `GET /genres`

**Reason:**  
This data changes rarely.
