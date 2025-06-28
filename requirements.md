# 📄 Airbnb Clone – Requirements Document

This document describes the technical and functional requirements for core backend features of the Airbnb Clone project.

---

## 🔐 User Authentication

### ✅ Functional Requirements

- Allow users to register as a guest or host.
- Support login via email and password.
- Enable profile management (update name, photo, contact info).
- Secure authentication using JWT tokens.

### ⚙️ Technical Requirements

#### API Endpoints

- `POST /api/v1/auth/register`
  - **Input**: `first_name`, `last_name`, `email`, `password`, `role`
  - **Output**: Success message, JWT token.
  - **Validation**: Email must be unique, password meets minimum security standards.

- `POST /api/v1/auth/login`
  - **Input**: `email`, `password`
  - **Output**: JWT token, user details.
  - **Validation**: Email and password must match records.

- `GET /api/v1/auth/profile`
  - **Output**: User profile information.
  - **Auth**: JWT required.

- `PATCH /api/v1/auth/profile`
  - **Input**: `first_name`, `last_name`, `photo`, `phone_number`
  - **Output**: Updated profile data.
  - **Auth**: JWT required.

#### Validation Rules

- Email format validation.
- Password minimum length (e.g., 8 characters) and complexity.
- Only valid roles ("guest", "host") allowed.

#### Performance Criteria

- Authentication response time < 300ms.
- Passwords hashed securely (bcrypt or Argon2).
- Token expiration and refresh handled correctly.

---

## 🏠 Property Management

### ✅ Functional Requirements

- Hosts can create, update, delete, or deactivate listings.
- Guests can view and search listings by filters (location, price, capacity, amenities).
- Listings include detailed property information: name, description, location, price, photos, availability.

### ⚙️ Technical Requirements

#### API Endpoints

- `POST /api/v1/properties`
  - **Input**: `name`, `description`, `location_id`, `price_per_night`, `max_guests`, `images`, `amenities`
  - **Output**: Created property details.
  - **Auth**: Host JWT required.

- `GET /api/v1/properties`
  - **Query Params**: `location`, `price_min`, `price_max`, `guests`, `amenities`
  - **Output**: List of properties matching filters.

- `PATCH /api/v1/properties/{id}`
  - **Input**: Any updatable fields.
  - **Output**: Updated property data.
  - **Auth**: Host JWT required.

- `DELETE /api/v1/properties/{id}`
  - **Output**: Deletion confirmation.
  - **Auth**: Host JWT required.

#### Validation Rules

- Mandatory fields: name, description, price, location.
- Price must be positive.
- Images must be valid URLs or uploaded files to supported storage.

#### Performance Criteria

- Search results returned within < 500ms using indexed queries.
- Image storage optimized using cloud services (e.g., AWS S3).

---

## 📅 Booking System

### ✅ Functional Requirements

- Guests can create and cancel bookings.
- System validates dates to avoid double bookings.
- Hosts can view and manage bookings (accept/reject).
- Booking statuses: pending, confirmed, canceled, completed.

### ⚙️ Technical Requirements

#### API Endpoints

- `POST /api/v1/bookings`
  - **Input**: `property_id`, `start_date`, `end_date`, `number_of_guests`
  - **Output**: Booking details.
  - **Auth**: Guest JWT required.

- `GET /api/v1/bookings`
  - **Output**: User’s booking history.
  - **Auth**: JWT required.

- `PATCH /api/v1/bookings/{id}/cancel`
  - **Output**: Updated booking status.
  - **Auth**: JWT required.

- `GET /api/v1/bookings/host`
  - **Output**: List of bookings for host’s properties.
  - **Auth**: Host JWT required.

#### Validation Rules

- Booking dates must be in the future.
- No overlapping bookings for the same property.
- Guest count must not exceed max guests allowed.

#### Performance Criteria

- Conflict checks performed in < 500ms.
- Bookings persisted reliably with transactional integrity.

---

## ✅ Acknowledgment

This requirements file was created with guidance and prompting support from **ChatGPT by OpenAI**, as part of my AI prompting practice for the ALX Airbnb Clone backend project.

---
