🛒 Full-Stack E-Commerce Application
A full-stack e-commerce web application built with React (frontend), Spring Boot (backend), and PostgreSQL (database).
The app allows users to **view, add, update, search, and manage products** with image uploads.
Postman is used for API testing before integration with the frontend.

---

🚀 Tech Stack
1. Frontend:React, React Router, Axios, Bootstrap
2. Backend:Spring Boot, Spring Data JPA, REST APIs
3. Database:PostgreSQL
4. Testing:Postman

---

⚙️ Project Workflow

🔹 React Frontend

1. Entry Point: `main.jsx` renders `<App />` wrapped in `AppProvider` (Context API for global state).
2. Routing: Defined in `App.jsx` using React Router:

  1. `/` → Home (product listing & filtering by category)
  2. `/add_product` → Add new product
  3. `/product/:id` → Product details
  4. `/cart` → Shopping cart
  5. `/product/update/:id` → Update product
     
3. State Management:**
  1. `cart` → maintains items added to cart
  2. `selectedCategory` → filters product list
     
4. API Communication:
  Axios instance (`axios.js`) configured with base URL `http://localhost:8080/api` to connect with backend.
---

🔹 Spring Boot Backend

API Endpoints (ProductController):

1. `GET /api/products` → Fetch all products
2. `GET /api/product/{id}` → Fetch product by ID
3. `GET /api/product/{id}/image` → Fetch product image
4. `POST /api/product` → Add new product (with image upload via multipart/form-data)
5. `PUT /api/product/{id}` → Update product
6. `DELETE /api/product/{id}` → Delete product
7. `GET /api/product/search?keyword=...` → Search products by keyword

Layers:

1. Entity Layer: `Product.java` (fields: id, name, description, price, category, stockQuantity, image data, etc.)
2. Repository Layer: `ProductRepository` (extends `JpaRepository`, includes search method).
3. Service Layer: `ProductService.java` (business logic + image handling).
4. Controller Layer: `ProductController.java` (REST endpoints with CORS enabled for React).

---

🔹 PostgreSQL Database

1. Stores product details and images (`bytea`/`blob`).
2. Managed by **Spring Data JPA** for CRUD operations.

---

🔹 Postman Testing

Before connecting the frontend, APIs were tested using **Postman**:

1. `GET /api/products` → Check product listing.
2. `POST /api/product` → Add new product with image (form-data).
3. `PUT /api/product/{id}` → Update product details.
4. `DELETE /api/product/{id}` → Delete product.
5. `GET /api/product/search?keyword=shoes` → Test search functionality.

---

📝 Data Flow Example

➕ Adding a Product

1. User navigates to `/add_product` in React.
2. Fills product form + uploads image.
3. React sends POST request → `Spring Boot API (/api/product)`.
4. Backend processes request → saves product + image in PostgreSQL.
5. JSON response returned → React updates UI.

 👀 Viewing Products

1. User visits `/`.
2. React calls `GET /api/products`.
3. Backend fetches products → returns JSON list.
4. React displays product cards → loads images using `/api/product/{id}/image`.

---

 📂 Project Structure

```bash
E-Commerce/
├── backend/ (Spring Boot)
│   ├── controller/ProductController.java
│   ├── service/ProductService.java
│   ├── model/Product.java
│   ├── repository/ProductRepository.java
│   └── application.properties
│
├── frontend/ (React)
│   ├── src/
│   │   ├── App.jsx
│   │   ├── main.jsx
│   │   ├── axios.js
│   │   ├── components/
│   │   │   ├── Home.jsx
│   │   │   ├── Navbar.jsx
│   │   │   ├── Cart.jsx
│   │   │   ├── AddProduct.jsx
│   │   │   ├── Product.jsx
│   │   │   ├── UpdateProduct.jsx
│   │   └── Context/Context.jsx
│   └── public/
│
└── README.md
```

---

 ▶️ How to Run

🔹 Backend (Spring Boot)

```bash
cd backend
mvn spring-boot:run
```
Backend runs at: `http://localhost:8080/api`

🔹 Database (PostgreSQL)

Create a database `ecommerce_db`.
 Update `application.properties`:
```properties
spring.datasource.url=jdbc:postgresql://localhost:5432/ecommerce_db
spring.datasource.username=your_username
spring.datasource.password=your_password
```

🔹 Frontend (React)

```bash
cd frontend
npm install
npm start
```
Frontend runs at: `http://localhost:3000`

🎯 Features
✔ Product CRUD (Create, Read, Update, Delete)
✔ Image upload & retrieval
✔ Product search by keyword
✔ Category filtering
✔ Shopping cart functionality
✔ PostgreSQL persistence
✔ Postman API testing

