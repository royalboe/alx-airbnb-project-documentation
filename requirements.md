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

- `GET /api/v1/properties/{id}`
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

## 💰 Payment System

### ✅ Functional Requirements

- Guests can pay for bookings securely through supported payment gateways.
- System calculates total price, including service and cleaning fees.
- Hosts receive payouts after bookings are completed.
- Payment statuses tracked: pending, completed, failed.

### ⚙️ Technical Requirements

#### API Endpoints

- `POST /api/v1/payments`
  - **Input**: `booking_id`, `payment_method_id`, `amount`
  - **Output**: Payment confirmation details.
  - **Auth**: Guest JWT required.

- `GET /api/v1/payments`
  - **Output**: User’s payment history (guest or host).
  - **Auth**: JWT required.

- `GET /api/v1/payments/{id}`
  - **Output**: Payment details for a specific payment record.
  - **Auth**: JWT required.

#### Validation Rules

- Payment amount must match booking total price.
- Only valid, supported payment methods allowed (e.g., Stripe, PayPal, credit card).
- Booking status must be "confirmed" before payment.

#### Performance Criteria

- Payments processed within < 1 second on backend after third-party confirmation.
- Secure tokenization of payment data to meet PCI-DSS compliance.
- Clear error handling for failed or incomplete payments.

---

## ⭐ Reviews & Ratings

### ✅ Functional Requirements

- Guests can leave reviews and ratings for properties after a completed stay.
- Hosts can optionally respond to reviews.
- Reviews must be linked to specific bookings to prevent fake reviews.
- Ratings are numeric (e.g., 1 to 10 scale), and properties can have aggregated average ratings.

### ⚙️ Technical Requirements

#### API Endpoints

- `POST /api/v1/reviews`
  - **Input**: `booking_id`, `property_id`, `rating`, `comment`
  - **Output**: Confirmation of review creation.
  - **Auth**: Guest JWT required.

- `GET /api/v1/reviews`
  - **Output**: List of reviews for properties.
  - **Optional query params**: `property_id`, `user_id`
  - **Auth**: Public, but authenticated users get extra context (e.g., if they already reviewed).

- `PUT /api/v1/reviews/{id}`
  - **Input**: `rating`, `comment`
  - **Output**: Updated review details.
  - **Auth**: Guest JWT required, only for the review owner.

- `POST /api/v1/reviews/{id}/reply`
  - **Input**: `comment`
  - **Output**: Host’s reply to a review.
  - **Auth**: Host JWT required.

#### Validation Rules

- Guests can submit one review per completed booking.
- Rating must be an integer between 1 and 10.
- Comments are optional but must not exceed 1000 characters.
- Guests can only edit reviews before a set deadline (e.g., within 30 days).

#### Performance Criteria

- Average rating of a property recalculated and updated in real-time after each new review.
- Review fetch latency < 300ms to support quick rendering on frontend.
- All reviews securely stored and linked to user and booking records.

---

## ✅ Acknowledgment

This requirements file was created with guidance and prompting support from **ChatGPT by OpenAI**, as part of my AI prompting practice for the ALX Airbnb Clone backend project.

---
