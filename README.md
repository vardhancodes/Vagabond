# 🧭 Vagabond — Full-Stack Tour Booking & Travel Management Platform

[![Node.js](https://img.shields.io/badge/Node.js-v18%2B-green.svg)](https://nodejs.org/)
[![Express.js](https://img.shields.io/badge/Express.js-4.x-lightgrey.svg)](https://expressjs.com/)
[![React](https://img.shields.io/badge/React-18.x-blue.svg)](https://react.dev/)
[![MongoDB](https://img.shields.io/badge/MongoDB-Atlas-brightgreen.svg)](https://www.mongodb.com/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

**Vagabond** is a full-stack, end-to-end travel booking and tour management platform built using the MERN stack (MongoDB, Express.js, React.js, Node.js). It provides a seamless interface for users to discover, search, and book curated guided tours, while giving administrators dynamic control over tour itineraries, user bookings, and platform reviews.

---

## ✨ Key Features

* **Authentication & Authorization:** Secure user registration and login utilizing **JSON Web Tokens (JWT)** and **Bcrypt** password hashing with Role-Based Access Control (RBAC).
* **Tour Discovery & Search:** Dynamic filtering and search options (location, price, group size, duration) powered by **MongoDB Aggregation Pipelines**.
* **Booking & Reservation Management:** Real-time booking processing allowing users to manage active reservations and view travel histories.
* **Interactive Reviews & Ratings:** Verified user feedback system allowing travelers to submit reviews and star ratings for completed tours.
* **Responsive UI/UX:** Modern, mobile-first design built with **React** and **Tailwind CSS**.

---

## 🛠️ Tech Stack

* **Frontend:** React.js, React Router, Context API / Redux, Tailwind CSS / CSS Modules
* **Backend:** Node.js, Express.js REST APIs
* **Database:** MongoDB, Mongoose ODM
* **Security & Auth:** JSON Web Tokens (JWT), Bcrypt.js, CORS
* **Development Tools:** Postman, Git/GitHub

---

## 🏛️ System Architecture

```text
┌─────────────────────────────────────────────────────────┐
│                     React Frontend                      │
│     (Tour Search, Booking Forms, User Dashboard)        │
└────────────────────────────┬────────────────────────────┘
                             │ REST API / JSON
                             ▼
┌─────────────────────────────────────────────────────────┐
│                   Express Backend API                   │
│  (JWT Auth Middleware, Controllers, Error Handlers)     │
└────────────────────────────┬────────────────────────────┘
                             │ Mongoose ODM
                             ▼
┌─────────────────────────────────────────────────────────┐
│                    MongoDB Database                     │
│    (User Accounts, Tour Schemas, Bookings, Reviews)     │
└─────────────────────────────────────────────────────────┘
