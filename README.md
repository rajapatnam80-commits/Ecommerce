# Cartly – E-Commerce Web Application

A full-stack online store with product management, order tracking, JWT login and
role-based access (Admin / User).

**Stack:** Node.js · Express · MongoDB (Mongoose) · JWT · bcrypt · Vanilla JS frontend

## Features
- Product catalog with search and category filter
- Add to cart, quantity control, checkout (cash on delivery) with stock validation
- Register / login with hashed passwords and JWT sessions
- Role-based access: **User** (shop, cart, own orders) and **Admin** (product CRUD, all orders, update order status)
- Backend REST APIs for products and orders
- Prices are read from the database at checkout; stock is decremented atomically and restored if an order is cancelled

## Run it
1. Install [Node.js 18+](https://nodejs.org) and MongoDB Community (or create a free MongoDB Atlas cluster and copy its connection string).
2. In this folder:
   ```bash
   npm install
   cp .env.example .env      # on Windows: copy .env.example .env
   npm run seed              # adds sample products + demo accounts
   npm start
   ```
3. Open http://localhost:5000

**Demo accounts**
| Role  | Email          | Password |
|-------|----------------|----------|
| Admin | admin@shop.com | admin123 |
| User  | user@shop.com  | user123  |

## API
| Method | Endpoint | Access | Purpose |
|--------|----------|--------|---------|
| POST | /api/auth/register | Public | Create a user account |
| POST | /api/auth/login | Public | Log in, returns JWT |
| GET | /api/auth/me | Logged in | Current user |
| GET | /api/products | Public | List (`?search=&category=`) |
| GET | /api/products/:id | Public | Single product |
| POST | /api/products | Admin | Create product |
| PUT | /api/products/:id | Admin | Update product |
| DELETE | /api/products/:id | Admin | Delete product |
| POST | /api/orders | User | Place order (checkout) |
| GET | /api/orders/mine | User | My orders |
| GET | /api/orders | Admin | All orders |
| PATCH | /api/orders/:id/status | Admin | Pending / Shipped / Delivered / Cancelled |

Send the token as `Authorization: Bearer <token>`.

## Structure
```
server.js          app entry, DB connection, error handler
seed.js            sample data + demo accounts
models/            User, Product, Order (Mongoose)
routes/            auth, products, orders
middleware/auth.js JWT check + admin role guard
public/index.html  storefront and admin UI
```
