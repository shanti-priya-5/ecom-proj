# Ecom Proj

A Spring Boot REST API for managing products in an e-commerce style app.
Supports adding, updating, deleting, and searching products, including
uploading a product image that gets stored in the database.

## Tech stack

- Java 25, Spring Boot
- Spring Web (REST controllers)
- Spring Data JPA
- H2 (in-memory database)
- Lombok

## What it does

- `GET /api/products` — get all products
- `GET /api/product/{id}` — get a single product by id
- `POST /api/product` — add a new product (takes product data + an image file)
- `PUT /api/product/{id}` — update an existing product
- `DELETE /api/product/{id}` — delete a product
- `GET /api/product/{productId}/image` — get a product's image
- `GET /api/products/search?keyword=...` — search products by name,
  description, brand, or category (case-insensitive)

Product images are uploaded as `MultipartFile` and stored directly in the
database as a byte array, along with the image name and content type so
they can be served back correctly.

## Project structure

```
├── .gitignore
├── HELP.md
├── mvnw / mvnw.cmd
├── pom.xml
├── .mvn/
└── src/
    ├── main/
    │   ├── java/com/priishaa/ecom_proj/
    │   │   ├── EcomProjApplication.java
    │   │   ├── controller/ProductController.java
    │   │   ├── model/Product.java
    │   │   ├── repo/ProductRepo.java
    │   │   └── service/ProductService.java
    │   └── resources/
    │       ├── application.properties
    │       └── data1.sql
    └── test/
```

## How to run it

Needs a JDK (Java 25) — no need to install Maven separately since the
project includes the Maven wrapper.

```bash
./mvnw spring-boot:run
```
(On Windows, use `mvnw.cmd spring-boot:run`)

The app starts on the default Spring Boot port (8080). The H2 in-memory
database resets every time the app restarts, and `data1.sql` seeds some
initial data on startup.

You can hit the endpoints with Postman, or from a frontend that calls
`http://localhost:8080/api/...`.

## Notes

- `spring.jpa.hibernate.ddl-auto=update` means the database schema is
  auto-generated/updated from the `Product` entity — no manual migrations
  needed for this project.
- CORS is open (`@CrossOrigin` on the controller) so it can be called from
  a separate frontend during development.
