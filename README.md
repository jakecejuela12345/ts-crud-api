# TypeScript CRUD API

A robust RESTful CRUD API built with Express, TypeScript, and MySQL using Sequelize ORM. Includes JWT authentication, role-based access control, and comprehensive error handling.

## Features

- ✅ Express.js with TypeScript support
- ✅ MySQL database with Sequelize ORM
- ✅ JWT authentication
- ✅ Role-based access control
- ✅ Input validation with Joi
- ✅ Password encryption with bcryptjs
- ✅ CORS enabled
- ✅ Global error handling middleware
- ✅ Development and production builds

## Prerequisites

Before setup, ensure you have:

- **Node.js** (v16 or higher)
- **npm** (v7 or higher)
- **MySQL** (v5.7 or higher)

## Setup Instructions

### 1. Clone & Install Dependencies

```bash
npm install
```

### 2. Configure Database

Update `config.json` with your MySQL credentials:

```json
{
    "database": {
        "host": "localhost",
        "port": 3306,
        "user": "root",
        "password": "your-password",
        "database": "typescript_crud_api"
    },
    "jwtSecret": "your-secret-key-change-in-production"
}
```

### 3. Create Database

Run the following in MySQL:

```sql
CREATE DATABASE typescript_crud_api;
```

Tables will be automatically created by Sequelize on first run.

### 4. Environment Configuration

Database configuration is read from `config.json`. Ensure the database is running and accessible.

## Development

### Start Development Server

Run the server with hot-reload using ts-node and nodemon:

```bash
npm run start:dev
```

Server starts on `http://localhost:4000` by default. 

**Custom port:**
```bash
PORT=3000 npm run start:dev
```

## Production Build

### Build TypeScript

```bash
npm run build
```

Compiles TypeScript to JavaScript in the `dist/` directory.

### Start Production Server

```bash
npm start
```

Runs the compiled server from `dist/server.js`.

## Testing

### Test User Endpoints

The test file is located at `tests/users.test.ts`.

#### Manual Testing with cURL

**Create User (POST)**
```bash
curl -X POST http://localhost:4000/users \
  -H "Content-Type: application/json" \
  -d '{
    "email": "user@example.com",
    "password": "SecurePass123!",
    "firstName": "John",
    "lastName": "Doe",
    "role": "user"
  }'
```

**Get All Users (GET)**
```bash
curl http://localhost:4000/users
```

**Get User by ID (GET)**
```bash
curl http://localhost:4000/users/1
```

**Update User (PUT)**
```bash
curl -X PUT http://localhost:4000/users/1 \
  -H "Content-Type: application/json" \
  -d '{
    "firstName": "Jane",
    "lastName": "Smith"
  }'
```

**Delete User (DELETE)**
```bash
curl -X DELETE http://localhost:4000/users/1
```

### Testing with Postman

1. Create a new Postman collection
2. Use the cURL examples above as reference
3. Set `Content-Type: application/json` header for POST/PUT requests
4. Authenticate using JWT tokens if protected routes are implemented

## Project Structure

```
src/
├── server.ts                 # Express app initialization
├── _helpers/
│   ├── db.ts                # Database configuration & connection
│   └── role.ts              # Role definitions
├── _middleware/
│   ├── errorHandler.ts      # Global error handling
│   └── validateRequest.ts   # Request validation middleware
└── users/
    ├── user.model.ts        # Sequelize user model
    ├── user.service.ts      # Business logic
    └── users.controller.ts   # Route handlers

tests/
└── users.test.ts            # Test definitions

dist/                        # Compiled JavaScript (generated)
```

## Scripts

| Script | Description |
|--------|-------------|
| `npm run build` | Compile TypeScript to JavaScript |
| `npm run start:dev` | Start development server with hot-reload |
| `npm start` | Start production server from compiled dist/ |
| `npm test` | Run test suite (placeholder) |

## Dependencies

### Production

- **express** - Web framework
- **sequelize** - ORM for database operations
- **mysql2** - MySQL client
- **jsonwebtoken** - JWT authentication
- **bcryptjs** - Password hashing
- **joi** - Data validation
- **cors** - Cross-Origin Resource Sharing
- **rootpath** - Root path resolution

### Development

- **typescript** - TypeScript compiler
- **ts-node** - TypeScript execution for Node.js
- **nodemon** - Auto-restart on file changes
- **@types/** - TypeScript type definitions

## Error Handling

The application includes a global error handler middleware (`errorHandler.ts`) that catches all errors and returns consistent JSON responses with appropriate HTTP status codes.

## License

ISC
