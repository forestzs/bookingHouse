
---

## BookingHouse Web App – README

```markdown
# BookingHouse Web App

BookingHouse is a full-stack property booking platform inspired by modern rental apps. It supports geospatial search, robust booking logic, and secure multi-tenant authentication for hosts and guests.

## Features

- Property listing and booking management
- Radius-based geospatial search over 10,000+ records with sub-200ms responses 
- Stateless JWT-based authentication with role-specific authorization
- Support for both hosts (listing properties) and guests (booking properties)
- Booking conflict checks and availability validation to prevent double-booking
- Transaction-safe updates and consistency guarantees for booking operations
- Cloud deployment with integration between backend and hosted frontend :contentReference[oaicite:6]{index=6}

## Tech Stack

**Backend**

- Java, Spring Boot
- Spring Security (JWT)
- Spring Data JPA / Hibernate
- PostgreSQL + Hibernate Spatial for geospatial queries

**Frontend**

- React
- Ant Design (UI library)
- Fetch / Axios for API calls

**Cloud & DevOps**

- Google Cloud Platform (backend deployment with autoscaling)
- AWS Amplify hosting (for React frontend)
- Centralized logging & monitoring :contentReference[oaicite:7]{index=7}

## Architecture Overview

- **Authentication & Authorization**
  - Stateless JWT-based auth with Spring Security.
  - Different roles for **HOST** and **GUEST**, controlling access to listing/booking endpoints.

- **Geospatial Search**
  - Properties stored with spatial coordinates in PostgreSQL using Hibernate Spatial.
  - Radius-based search queries using spatial indices for fast lookups.

- **Booking Logic**
  - Create/update bookings with conflict detection:
    - No overlapping date ranges for the same property.
    - Transaction-safe operations to avoid race conditions and double-booking.

- **Frontend**
  - React + Ant Design for responsive UI.
  - Forms with validation for login, registration, listing creation, and booking.
  - Async/await patterns for clean API integration.

## Getting Started

### Prerequisites

- JDK 17+
- Maven or Gradle
- PostgreSQL (with PostGIS / spatial support)
- Node.js & npm (for React)
- Cloud accounts (GCP + AWS) if you want full deployment

### Backend Setup

1. Clone the repository:

   ```bash
   git clone https://github.com/<your-username>/booking-house.git
   cd booking-house
