# 🔄 User Registration Flowchart – Airbnb Clone Backend

This document explains the backend process of user registration, represented in the `user-registration.png` flowchart diagram.

---

## 🧩 Purpose

This flowchart visualizes how the backend handles the **user registration** process in the Airbnb Clone project. It outlines the logical flow from receiving user input to returning a successful response or handling invalid input.

---

## 📊 Flow Description

1. **User submits registration form**
   - Includes email, password, name, and other required data.

2. **Validate input data**
   - Server checks for valid format, required fields, password strength, etc.

3. **Is input valid?**
   - If **No**, return an error response (e.g., 400 Bad Request).
   - If **Yes**, proceed to next step.

4. **Hash password**
   - The password is hashed securely using algorithms like bcrypt or Argon2 before saving.

5. **Store user in database**
   - A new user record is inserted into the database with hashed password and profile info.

6. **Send verification email**
   - A verification link or OTP is sent to confirm user email address.

7. **Generate authentication token**
   - A JWT or similar token is generated to allow immediate access if verification is not mandatory.

8. **Return success response with token**
   - The client receives a response with token and user data to allow access to protected routes.

---

## 🙏 Acknowledgment

This flowchart and documentation were created with the assistance of **ChatGPT by OpenAI** during my AI prompting practice in the **ALX Airbnb Clone backend project**.
