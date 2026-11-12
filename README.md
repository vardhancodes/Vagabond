# 🧭 Vagabond — Full-Stack Tour Management Platform

[![Java](https://img.shields.io/badge/Java-17%2B-orange.svg)](https://www.oracle.com/java/)
[![Spring Boot](https://img.shields.io/badge/Spring%20Boot-3.x-brightgreen.svg)](https://spring.io/projects/spring-boot)
[![React](https://img.shields.io/badge/React-18.x-blue.svg)](https://react.dev/)
[![Vite](https://img.shields.io/badge/Vite-6.x-purple.svg)](https://vitejs.dev/)
[![Tailwind CSS](https://img.shields.io/badge/Tailwind%20CSS-3.x-38bdf8.svg)](https://tailwindcss.com/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

**Vagabond** is an enterprise-grade, full-stack tour booking and travel management platform. It features a robust **Spring Boot** RESTful backend for relational data persistence and business logic, paired with a modern **Vite + React** single-page application styled with **Tailwind CSS**.

---

## 🏛️ System Architecture

```text
┌─────────────────────────────────────────────────────────────────────────┐
│                    REACT + VITE SINGLE PAGE CLIENT                      │
│            (Tailwind CSS · Redux Toolkit · React Router v7)             │
└───────────────┬─────────────────────────────────────────┬───────────────┘
                │                                         │
     Public / Customer Operations              Admin Dashboard Operations
    (Browse, Register, Book Tours)             (CRUD Tours, Transports, Stays)
                │                                         │
                ▼                                         ▼
┌─────────────────────────────────────────────────────────────────────────┐
│                      SPRING BOOT REST API LAYER                         │
│                    (Controllers & Filters on :8080)                     │
├─────────────────────────────────────────────────────────────────────────┤
│ • AuthController       (Sign-In, Sign-Up, OAuth2 Google, JWT Issuance)  │
│ • TourController       (Catalog pagination, detail view, availability)  │
│ • BookingController    (Cart submission, ticket calculation, payment)   │
│ • AdminControllers     (Lodging, Transport, Location, Tour Modals)      │
└───────────────┬─────────────────────────────────────────┬───────────────┘
                │                                         │
                ▼                                         ▼
┌───────────────────────────────────────┐ ┌───────────────────────────────┐
│          SERVICE & LOGIC              │ │      SECURITY & SESSIONS      │
│   • TourService      • BookingService │ │ • JwtAuthenticationFilter     │
│   • StripeService    • FileStorage    │ │ • SecurityFilterChain         │
└───────────────────┬───────────────────┘ └───────────────┬───────────────┘
                    │                                     │
                    ▼                                     ▼
┌─────────────────────────────────────────────────────────────────────────┐
│                   HIBERNATE JPA DATA PERSISTENCE                        │
│                 (Spring Data JPA Relational Schema)                     │
└───────────────────────────────────┬─────────────────────────────────────┘
                                    │
                                    ▼
┌─────────────────────────────────────────────────────────────────────────┐
│                            DATABASE ENGINE                              │
│       • Production / Development: PostgreSQL (schema.sql + data.sql)    │
│       • Test Profile: Embedded In-Memory H2 Engine                      │
└─────────────────────────────────────────────────────────────────────────┘
```

---

## 🔐 Authentication & Session Flow

```text
Customer / Admin Browser                 Vite / React State (Redux)            Spring Boot (:8080)
           │                                         │                                  │
           │── Enter Email & Password ──────────────>│                                  │
           │                                         │── POST /api/auth/login ─────────>│
           │                                         │                                  │── Validate bcrypt
           │                                         │                                  │── Sign JWT with Claims
           │                                         │<── Return Bearer JWT Token ──────│
           │                                         │                                  │
           │                                         │── Save to localStorage           │
           │                                         │── Update Redux Auth State        │
           │<── Redirect to Dashboard ───────────────│                                  │
           │                                         │                                  │
           │── Access Protected Route (/user/*) ────>│── Check JWT expiration           │
           │                                         │── Send Bearer Token in Header ──>│
           │                                         │<── Authorized 200 OK + Data ─────│
```

---

## 🗄️ Relational Data Model (ER Architecture)

```text
┌───────────────────────┐             ┌─────────────────────────┐
│         USER          │             │          TOUR           │
├───────────────────────┤             ├─────────────────────────┤
│ id (PK)               │ 1         * │ id (PK)                 │
│ name                  │────────────>│ tour_name               │
│ email (Unique)        │             │ tour_description        │
│ password (Hash)       │             │ price                   │
│ role (CUSTOMER/ADMIN) │             │ tickets_available       │
└──────────┬────────────┘             │ start_date / end_date   │
           │ 1                        └───────┬─────────┬───────┘
           │                                  │ 1       │ 1
           │ *                                │         │
┌──────────▼────────────┐                     │         │
│        BOOKING        │                     ▼ 1       ▼ 1
├───────────────────────┤ 1         * ┌──────────────┐ ┌──────────────┐
│ id (PK)               │<────────────│   LOCATION   │ │   LODGING    │
│ user_id (FK)          │             ├──────────────┤ ├──────────────┤
│ tour_id (FK)          │             │ id (PK)      │ │ id (PK)      │
│ booking_date          │             │ city, state  │ │ hotel_name   │
│ ticket_count          │             │ country      │ │ room_type    │
│ payment_status        │             └──────────────┘ └──────────────┘
└───────────────────────┘
```

---

## ✨ Key Features

* **Spring Boot REST Architecture:** Clean separation of concerns across Controllers, Services, and Repositories.
* **Relational Database Schema:** Managed database initializations via `schema.sql` and `data.sql` for structured tour catalogs, user records, and booking workflows.
* **Role-Based Access Control:** Distinct roles (`ROLE_CUSTOMER`, `ROLE_ADMIN`) governing administrative dashboards and booking checkout flows.
* **Modern Frontend (Vite + React):** Fast module replacement, Redux Toolkit state management, and protected client-side routes.
* **Interactive Dashboards:** Visual booking management, tour catalog browsing, and ticket summary inspection.
* **Configurable Environments:** Environment variable configuration (`.env`, `application.properties`) for local development, testing, and production builds.

---

## 🛠️ Tech Stack

### Backend (`tour-app-backend`)
* **Language/Framework:** Java 17+, Spring Boot 3.3.5
* **Build Tool:** Maven (`pom.xml`, Maven Wrapper)
* **Security & Auth:** Spring Security, JWT (`jjwt`), Google OAuth2
* **Database & Persistence:** PostgreSQL / H2 Database, Spring Data JPA / Hibernate
* **Third-Party Integrations:** Stripe Payments, Cloudinary Media Storage

### Frontend (`tours_frontend`)
* **Framework / Build:** React 18, Vite 6
* **State Management:** Redux Toolkit, React-Redux
* **Routing:** React Router v7
* **Styling:** Tailwind CSS, PostCSS, Lucide Icons
* **Notifications:** Sonner Toast Notifications

---

## 🚀 Getting Started

### Prerequisites
* Java JDK 17 or 21
* Node.js 18+ and npm
* PostgreSQL (or use embedded H2 profile for testing)

---

### 1. Setting Up Backend (`tour-app-backend`)

1. Navigate to the backend directory:
   ```bash
   cd tour-app-backend
   ```

2. Configure environment properties in `src/main/resources/application.properties`:
   ```properties
   # Profile selection: dev (PostgreSQL) or test (In-Memory H2)
   spring.profiles.active=dev

   # PostgreSQL credentials (if using dev profile)
   spring.datasource.url=jdbc:postgresql://localhost:5432/TeluskoTours
   spring.datasource.username=postgres
   spring.datasource.password=your_password
   ```

3. Build and launch the Spring Boot service:
   ```bash
   ./mvnw clean spring-boot:run
   ```
   The backend API will start on `http://localhost:8080`.

---

### 2. Setting Up Frontend (`tours_frontend`)

1. Navigate to the frontend directory:
   ```bash
   cd tours_frontend
   ```

2. Install dependencies:
   ```bash
   npm install
   ```

3. Ensure API endpoint is configured in `.env`:
   ```env
   VITE_BASE_URL="http://localhost:8080"
   ```

4. Launch Vite development server:
   ```bash
   npm run dev
   ```
   The frontend UI will be accessible at `http://localhost:5173`.

5. Build for production:
   ```bash
   npm run build
   ```

---

## 📁 Repository Structure

```text
Vagabond/
├── tour-app-backend/              # Spring Boot REST API
│   ├── src/main/java/com/tours/
│   │   ├── Controller/            # REST API Controllers (Tour, Booking, Auth)
│   │   ├── Entities/              # JPA Data Models (Tour, User, Booking)
│   │   ├── Repository/            # Spring Data JPA Repositories
│   │   ├── Service/               # Business logic & JWT services
│   │   └── Config/                # Security & CORS configuration
│   └── src/main/resources/        # application.properties, schema.sql, data.sql
└── tours_frontend/                # React + Vite + Tailwind Client
    ├── src/
    │   ├── components/            # UI components (Admin & Customer Views)
    │   ├── Redux/                 # Redux Toolkit store & API slices
    │   └── Routing/               # Client-side protected route declarations
    └── package.json               # Dependencies and scripts
```

---

## 📄 License
This project is licensed under the [MIT License](tour-app-backend/LICENSE).
