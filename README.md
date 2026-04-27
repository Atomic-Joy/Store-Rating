# StoreRating — Full Stack Application

A full-stack web app for submitting and managing store ratings.

## Tech Stack
- **Backend**: Express.js + Mongoose ODM
- **Database**: MongoDB
- **Frontend**: React.js

---

## Quick Start

### 1. Database Setup

Install MongoDB locally or use a cloud service like MongoDB Atlas.

For local MongoDB:
- Install MongoDB Community Server
- Start MongoDB service

Or set up a connection string for a cloud database.

### 2. Backend Setup

```bash
cd backend
npm install
# Create .env file with:
# MONGO_URI=mongodb://127.0.0.1:27017/storerating
# JWT_SECRET=your_jwt_secret_here
# PORT=5000
npm run dev
```

On first start, the server will:
- Connect to MongoDB
- Seed a default admin account:
  - Email: `admin@storerating.com`
  - Password: `Admin@123`

### 3. Frontend Setup

```bash
cd frontend
npm install
npm start
```

Frontend runs on `http://localhost:3000`, proxies API calls to `http://localhost:5000`.

---

## User Roles & Access

| Role | Access |
|------|--------|
| **Admin** | Dashboard stats, manage users & stores, view user details |
| **Normal User** | Browse stores, submit/modify ratings, change password |
| **Store Owner** | View own store's ratings & average, change password |

---

## API Endpoints

### Auth
- `POST /api/auth/register` — Sign up (normal users)
- `POST /api/auth/login` — Log in (all roles)
- `PUT /api/auth/password` — Update password (authenticated)

### Admin (requires `admin` role)
- `GET /api/admin/dashboard` — Stats
- `POST /api/admin/users` — Create user
- `GET /api/admin/users` — List users (filterable + sortable)
- `GET /api/admin/users/:id` — User detail
- `POST /api/admin/stores` — Create store
- `GET /api/admin/stores` — List stores (filterable + sortable)

### Stores
- `GET /api/stores` — Browse stores (normal users)
- `POST /api/stores/rate` — Submit / update rating
- `GET /api/stores/owner/dashboard` — Store owner dashboard

---

## Form Validations

| Field | Rule |
|-------|------|
| Name | 20–60 characters |
| Address | Max 400 characters |
| Password | 8–16 chars, ≥1 uppercase, ≥1 special char |
| Email | Standard email format |

---

## Project Structure

```
storerating/
├── backend/
│   ├── src/
│   │   ├── config/database.js
│   │   ├── models/          (User.js, Store.js, Rating.js, index.js)
│   │   ├── controllers/     (authController.js, adminController.js, storeController.js, ownerController.js)
│   │   ├── middleware/      (auth.js)
│   │   ├── routes/          (auth.js, admin.js, stores.js)
│   │   └── index.js
│   ├── .env
│   └── package.json
├── frontend/
│   ├── public/
│   │   └── index.html
│   ├── src/
│   │   ├── context/AuthContext.js
│   │   ├── utils/api.js
│   │   ├── components/Layout.js
│   │   ├── pages/
│   │   │   ├── Login.js / Register.js / ChangePassword.js
│   │   │   ├── admin/   (Dashboard.js, Users.js, Stores.js, AddUser.js, AddStore.js, UserDetail.js)
│   │   │   ├── user/    (Stores.js)
│   │   │   └── owner/   (Dashboard.js)
│   │   ├── App.js
│   │   ├── index.js
│   │   └── index.css
│   └── package.json
└── README.md
```
