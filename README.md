# 🧭 Vagabond — Full-Stack Tour Management Platform

[![Java](https://img.shields.io/badge/Java-17%2B-orange.svg)](https://www.oracle.com/java/)
[![Spring Boot](https://img.shields.io/badge/Spring%20Boot-3.x-brightgreen.svg)](https://spring.io/projects/spring-boot)
[![React](https://img.shields.io/badge/React-18.x-blue.svg)](https://react.dev/)
[![Vite](https://img.shields.io/badge/Vite-5.x-purple.svg)](https://vitejs.dev/)
[![Tailwind CSS](https://img.shields.io/badge/Tailwind%20CSS-3.x-38bdf8.svg)](https://tailwindcss.com/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

**Vagabond** is an enterprise-grade, full-stack tour booking and travel management platform. It features a robust **Spring Boot** RESTful backend for relational data persistence and business logic, paired with a modern **Vite + React** single-page application styled with **Tailwind CSS**.

---

## ✨ Key Features

* **Spring Boot REST Architecture:** Clean separation of concerns across Controllers, Services, and Repositories.
* **Relational Database Schema:** Managed database initializations via `schema.sql` and `data.sql` for structured tour catalogs, user records, and booking workflows.
* **Modern Frontend (Vite + React):** Fast module replacement, component-based layout, and smooth routing for client-side interactions.
* **Tailwind CSS UI:** Fully responsive utility-first UI design tailored for desktop and mobile viewports.
* **Configurable Environments:** Environment variable configuration (`.env`, `application.properties`) for local development, testing, and production builds.

---

## 🛠️ Tech Stack

### Backend (`tour-app-backend`)
* **Language/Framework:** Java, Spring Boot
* **Build Tool:** Maven (`pom.xml`, Maven Wrapper)
* **Database Management:** SQL (`schema.sql`, `data.sql`), Spring Data JPA / Hibernate

### Frontend (`tours_frontend`)
* **Framework / Build:** React.js, Vite
* **Styling:** Tailwind CSS, PostCSS
* **Tooling & Linting:** ESLint, Node.js (`package.json`)

---

## 🏛️ System Architecture

```text
┌─────────────────────────────────────────────────────────┐
│               Vite + React Frontend (SPA)               │
│        (Tailwind CSS, Dynamic Booking Forms, UI)        │
└────────────────────────────┬────────────────────────────┘
                             │ REST APIs / JSON
                             ▼
┌─────────────────────────────────────────────────────────┐
│                Spring Boot Backend API                  │
│       (Controllers, Service Layer, Repositories)        │
└────────────────────────────┬────────────────────────────┘
                             │ SQL / Hibernate JPA
                             ▼
┌─────────────────────────────────────────────────────────┐
│                   Relational Database                   │
│         (Tours, Bookings, Users, Schema Files)          │
└─────────────────────────────────────────────────────────┘
