# Pitstop: Car Service Centre API

A REST API (back end) for running a chain of car service centres: branches, staff, customers, their cars, service bookings, a parts shop and payments.

Built in 2024 with NestJS and TypeScript on PostgreSQL, as a personal project to learn how a real multi-role back end is designed.

## Features

- **25-table relational database** designed with Prisma (service centres, branches, services, cars, clients, appointments, staff, departments, suppliers, parts, baskets, payments, promo codes)
- **Authentication** with JWT access and refresh tokens (refresh token in an HTTP-only cookie) and bcrypt password hashing
- **Role-based access control** with 8 guards (admin, staff, HR, client, and "only edit your own account" rules)
- **Account activation by email** (Nodemailer + Handlebars templates)
- **Input validation** on every request with class-validator DTOs, including custom rules (password confirmation, work-day schedules)
- **Soft delete** for admins and staff, so records are kept rather than erased
- **134 endpoints**, documented with Swagger

## Tech stack

| Area | Tools |
|---|---|
| Language | TypeScript |
| Framework | NestJS (Node.js, Express) |
| Database | PostgreSQL, Prisma ORM and migrations |
| Auth | JWT, bcrypt, cookie-parser |
| Docs | Swagger (OpenAPI) |
| Email | Nodemailer, Handlebars |

## Run it locally

You need Node.js 20+ and a PostgreSQL database.

```bash
git clone https://github.com/d4vrn/pitStop.git
cd pitStop
npm install
```

Create a `.env` file in the project root:

```
DATABASE_URL=postgresql://USER:PASSWORD@localhost:5432/pitstop
API_PORT=3001
API_URL=http://localhost:3001
ACCESS_TOKEN_KEY=any-long-random-string
ACCESS_TOKEN_TIME=15m
REFRESH_TOKEN_KEY=another-long-random-string
REFRESH_TOKEN_TIME=7d
COOKIE_TIME_MS=604800000
SMTP_HOST=smtp.example.com
SMTP_USER=you@example.com
SMTP_PASSWORD=your-smtp-password
```

Then create the tables and start the server:

```bash
npx prisma migrate dev
npm run start:dev
```

The API runs at `http://localhost:3001/api`, and the Swagger docs at `http://localhost:3001/api/docs`.

## Project structure

Each part of the business is its own NestJS module under `src/` (for example `appointment/`, `staff/`, `payment/`), each with a controller (routes), a service (logic) and DTOs (validated input). Shared guards are in `src/guards/`, and email, validation and token types are in `src/common/`.

## Status

About 80% complete. Still to do:
- [Davron: list what is missing, e.g. finishing payments, adding tests]
