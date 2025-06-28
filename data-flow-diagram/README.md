# 🗺️ Data Flow Diagram – Airbnb Clone Project

## 📄 Overview

This document explains the **Data Flow Diagram (DFD)** for the Airbnb Clone backend system. The DFD visualizes how data moves between external entities, internal processes, and data stores within the application.  

The diagram was created using [Eraser.io](https://app.eraser.io) to clearly illustrate the core backend operations and support better system understanding and implementation planning.

---

## 💡 Key Components

### 🔹 External Entities

- **Guest**: Registers, searches, books, pays, reviews.
- **Host**: Manages listings, receives bookings and payments.
- **Admin**: Monitors and manages users, listings, payments, and bookings.
- **Payment Gateway**: Handles secure payment processing.

---

### ⚙️ Core Processes

1. **User Registration & Authentication**: Validates user data, hashes passwords, stores user info, and returns authentication tokens.
2. **Property Management**: Handles creating, editing, and deleting listings by hosts.
3. **Search & Booking**: Enables guests to search for properties, view details, and book available listings.
4. **Payment Processing**: Manages payment validations, sends data to payment gateways, and stores payment records.
5. **Reviews & Ratings**: Allows guests to submit reviews and ratings after stays.
6. **Notifications**: Sends email and in-app notifications for booking updates, payment confirmations, and system alerts.

---

### 💾 Data Stores

- **Users DB**
- **Properties DB**
- **Bookings DB**
- **Payments DB**
- **Reviews DB**

---

## 🔁 Data Flow Description

- Guests interact with the system to register, search, book, and leave reviews.
- Hosts manage listings and respond to bookings.
- Admins monitor activities, manage user accounts, and enforce policies.
- Payments flow through a secure gateway and are stored in the database.
- All user and system interactions generate notifications for better communication.

---

## ✅ Acknowledgment

This diagram was created using **Eraser.io** as part of the ALX Airbnb Clone backend project documentation.  

Guidance and prompting support were provided by **ChatGPT by OpenAI** to enhance clarity and completeness.

---
