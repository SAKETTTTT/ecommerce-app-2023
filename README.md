# E-commerce App (MERN)

A full-stack online store built with **MongoDB, Express, React and Node.js**. Customers can browse, search and filter products, add them to a cart and pay online. Admins manage categories, products and orders from a dashboard.

## Features

**For shoppers**
- Register, log in and reset a forgotten password (JWT authentication, passwords hashed with bcrypt)
- Browse products by category, search by keyword, filter by category and price, paginated product list
- Product detail page with related products
- Cart, and card payment through Braintree (sandbox)
- Order history and profile editing

**For admins**
- Admin-only dashboard (role-protected routes)
- Create, update and delete categories and products (with product photos)
- View all users and all orders

## Tech stack

| Layer | Tools |
|---|---|
| Frontend | React 18, React Router, Ant Design, Axios, React Toastify |
| Backend | Node.js, Express, Mongoose, JSON Web Tokens, bcrypt |
| Database | MongoDB |
| Payments | Braintree (sandbox) |

## Getting started

You need Node.js (v16 or newer) and a MongoDB database (local, or a free MongoDB Atlas cluster).

```bash
# 1. Install dependencies
npm install
npm install --prefix client

# 2. Create your environment file
cp .env.example .env
# then open .env and fill in your own values

# 3. Run the API and the React app together
npm run dev
```

The API runs on `http://localhost:5000` and the React app on `http://localhost:3000` (it proxies API calls to port 5000, so keep `PORT=5000`).

### Environment variables

| Variable | What it is |
|---|---|
| `PORT` | Port for the API (keep `5000`) |
| `DEV_MODE` | Label printed in the server log, e.g. `development` |
| `MONGO_URL` | MongoDB connection string |
| `JWT_SECRET` | Secret used to sign login tokens (use a long random string) |
| `BRAINTREE_MERCHANT_ID`, `BRAINTREE_PUBLIC_KEY`, `BRAINTREE_PRIVATE_KEY` | Braintree **sandbox** credentials |

> Keep real values in `.env` only. It is git-ignored, and `.env.example` shows the shape without any secrets.

## API overview

| Area | Endpoints (prefix `/api/v1`) |
|---|---|
| Auth | `POST /auth/register`, `POST /auth/login`, `POST /auth/forgot-password`, `PUT /auth/profile`, `GET /auth/orders`, `GET /auth/all-orders` |
| Category | `GET /category/get-category`, `GET /category/single-category/:slug`, plus admin create, update and delete |
| Product | `GET /product/get-product`, `GET /product/get-product/:slug`, `GET /product/product-list/:page`, `GET /product/search/:keyword`, `POST /product/product-filters`, `GET /product/related-product/:pid/:cid`, plus admin create, update and delete |
| Payments | `GET /product/braintree/token`, `POST /product/braintree/payment` |

## Project structure

```
├── server.js          # Express entry point
├── config/            # MongoDB connection
├── controllers/       # Request handlers
├── models/            # Mongoose schemas (user, category, product, order)
├── routes/            # Route definitions
├── middlewares/       # Auth and admin checks
├── helpers/           # Password hashing helpers
└── client/            # React app
    └── src/
        ├── pages/       # Home, cart, search, product pages, auth, admin, user
        ├── components/  # Layout, forms, routes
        └── context/     # Auth, cart and search state
```
