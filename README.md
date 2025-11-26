# BookingHouse Web App

BookingHouse is a full-stack property booking platform inspired by modern rental apps. It supports geospatial search, robust booking logic, and secure authentication for both hosts and guests.

---

## Features

- Property listing and booking management  
- Radius-based geospatial search over 10,000+ records  
- Stateless JWT-based authentication with role-specific authorization  
- Separate flows for **HOST** (list properties) and **GUEST** (book properties)  
- Booking conflict checks and availability validation to prevent double-booking  
- Transaction-safe updates to keep booking state consistent  
- Cloud deployment with separate backend and frontend hosting  

---

## Tech Stack

**Backend**

- Java, Spring Boot  
- Spring Security (JWT)  
- Spring Data JPA / Hibernate  
- PostgreSQL + PostGIS / Hibernate Spatial for geospatial queries  

**Frontend**

- React  
- Ant Design (UI library)  
- Fetch / Axios for API calls  

**Cloud & DevOps**

- Google Cloud Platform for backend deployment  
- AWS Amplify (or similar) for React frontend hosting  
- Basic logging and monitoring on cloud platform  

---

## Architecture Overview

- **Authentication & Authorization**  
  - Stateless JWT-based auth with Spring Security.  
  - Different roles for **HOST** and **GUEST** control which endpoints can be called.  

- **Geospatial Search**  
  - Property locations stored as spatial columns in PostgreSQL.  
  - Radius-based search using spatial indices for fast “nearby” queries.  

- **Booking Logic**  
  - Creates bookings only when dates are available (no overlapping ranges for the same property).  
  - Uses transactional operations to avoid race conditions and double-booking.  
  - Clear booking status (e.g. PENDING, CONFIRMED, CANCELLED).  

- **Frontend**  
  - React + Ant Design for modern, responsive UI.  
  - Forms for login/register, create listing, and booking.  
  - Uses async/await with Axios/Fetch to call REST APIs.  

---

## Project Structure

```text
booking-house/
├── backend/
│   ├── src/main/java/com/yourorg/booking/
│   │   ├── BookingHouseApplication.java
│   │   ├── config/        # Security, JWT, CORS, etc.
│   │   ├── controller/    # REST controllers (auth, property, booking)
│   │   ├── dto/           # Request/response DTOs
│   │   ├── entity/        # User, Property, Booking, etc.
│   │   ├── repository/    # Spring Data JPA repositories
│   │   └── service/       # Business logic
│   └── src/main/resources/
│       └── application.yml
└── frontend/
    ├── src/
    │   ├── components/
    │   ├── pages/
    │   ├── services/      # API clients
    │   └── App.jsx
    └── package.json
