# Build-a-Secure-Login
Create a secure login endpoint that: 1. Hashes passwords with bcrypt 2. Prevents SQL injection 3. Implements rate limiting 4. Returns proper HTTP status codes Submit your GitHub repository URL.

# 🔐 Secure Login API

A production-ready secure login endpoint built with Node.js + Express.

## Security Features

| Feature | Implementation |
|---|---|
| **Password Hashing** | `bcryptjs` with 12 salt rounds |
| **SQL Injection Prevention** | Parameterised queries via `sql.js` |
| **Rate Limiting** | `express-rate-limit` — 5 login attempts / 15 min |
| **Security Headers** | `helmet` with strict CSP |
| **Input Validation** | `express-validator` — whitelist + sanitise |
| **JWT Auth** | `jsonwebtoken` HS256, 1hr expiry |
| **Username Enumeration** | Generic 401 for invalid user OR wrong password |

## HTTP Status Codes

| Code | Scenario |
|---|---|
| `200` | Successful login |
| `201` | Account created |
| `401` | Invalid credentials |
| `404` | Resource not found |
| `409` | Username/email already exists |
| `422` | Validation errors |
| `429` | Rate limit exceeded |
| `500` | Internal server error |

## Quick Start

```bash
npm install
npm start
# → http://localhost:3000
```

## API Reference

### `POST /api/register`
```json
{ "username": "alice", "email": "alice@example.com", "password": "Secret123" }
```

### `POST /api/login`
```json
{ "username": "alice", "password": "Secret123" }
```

### `GET /api/me`
```
Authorization: Bearer <jwt_token>
```

### `GET /api/health`
No auth required.

## Password Rules
- Minimum 8 characters
- At least one uppercase letter
- At least one number

## Rate Limits
- **Login:** 5 attempts per 15 minutes per IP
- **Register:** 10 accounts per hour per IP
