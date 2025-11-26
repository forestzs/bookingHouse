# BookingHouse Web App

BookingHouse is a full-stack property booking platform inspired by modern rental apps. It supports geospatial search, robust booking logic, and secure multi-tenant authentication for hosts and guests.

---

## Features

- Property listing and booking management  
- Radius-based geospatial search over 10,000+ records with sub-200ms responses  
- Stateless JWT-based authentication with role-specific authorization  
- Support for both hosts (listing properties) and guests (booking properties)  
- Booking conflict checks and availability validation to prevent double-booking  
- Transaction-safe updates and consistency guarantees for booking operations  
- Cloud deployment with integration between backend and hosted frontend  

---

## Tech Stack

**Backend**

- Java, Spring Boot  
- Spring Security (JWT)  
- Spring Data JPA / Hibernate  
- PostgreSQL + Hibernate Spatial (PostGIS) for geospatial queries  

**Frontend**

- React  
- Ant Design (UI library)  
- Fetch / Axios for API calls  

**Cloud & DevOps**

- Google Cloud Platform for backend deployment (e.g., Cloud Run / GCE)  
- AWS Amplify or similar hosting for React frontend  
- Centralized logging & monitoring (e.g., GCP logs / dashboards)  

---

## Architecture Overview

- **Authentication & Authorization**
  - Stateless JWT-based auth with Spring Security.
  - Different roles for **HOST** and **GUEST**, controlling access to listing/booking endpoints.
  - Login and registration endpoints issue JWTs stored on the client side.

- **Geospatial Search**
  - Properties stored with latitude/longitude in PostgreSQL using Hibernate Spatial / PostGIS.
  - Radius-based search queries using spatial indices for fast lookups.
  - API supports parameters like `lat`, `lng`, and `radius` for nearby listings.

- **Booking Logic**
  - Create/update bookings with conflict detection:
    - No overlapping date ranges for the same property.
    - Validation on both start/end dates and property ID.
  - Transaction-safe operations to avoid race conditions and double-booking.
  - Clear status fields for bookings (e.g., PENDING, CONFIRMED, CANCELLED).

- **Frontend**
  - React + Ant Design for a responsive, modern UI.
  - Forms with validation for login, registration, property creation, and booking.
  - Uses async/await with Fetch / Axios to consume REST APIs.
  - Role-aware UI: different views/actions for hosts vs. guests.

---

## Main Project Structure
```text
booking-house/
├── backend/
│   ├── src/main/java/com/yourorg/booking/
│   │   ├── BookingHouseApplication.java
│   │   ├── config/          # Security, JWT, CORS, etc.
│   │   ├── controller/      # REST controllers (auth, property, booking)
│   │   ├── dto/             # Request/response DTOs
│   │   ├── entity/          # JPA entities (User, Property, Booking, etc.)
│   │   ├── repository/      # Spring Data JPA repositories
│   │   └── service/         # Business logic
│   └── src/main/resources/
│       └── application.yml  # DB, JWT secret, etc.
└── frontend/
    ├── src/
    │   ├── components/
    │   ├── pages/
    │   ├── services/        # API clients
    │   └── App.jsx
    └── package.json
