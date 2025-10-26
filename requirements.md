# Airbnb Clone Backend Requirement Specifications

This document provides detailed technical and functional requirement specifications for key backend features of the Airbnb Clone project.

---

## 1. User Authentication

### 1.1. Functional Requirements
- The system must allow users to register with an email, password, and role (Guest/Host).
- The system must allow registered users to log in using their email and password.
- The system must issue a JSON Web Token (JWT) upon successful login to manage user sessions.
- The system must protect certain routes, allowing access only to authenticated users.

### 1.2. API Endpoints

#### `POST /api/auth/register`
- **Description:** Registers a new user.
- **Request Body:**
  ```json
  {
    "name": "John Doe",
    "email": "john.doe@example.com",
    "password": "password123",
    "role": "Guest"
  }
  ```
- **Response (Success - 201 Created):**
  ```json
  {
    "userId": "12345",
    "token": "<jwt_token>"
  }
  ```
- **Response (Error - 400 Bad Request):** If validation fails or user already exists.

#### `POST /api/auth/login`
- **Description:** Logs in an existing user.
- **Request Body:**
  ```json
  {
    "email": "john.doe@example.com",
    "password": "password123"
  }
  ```
- **Response (Success - 200 OK):**
  ```json
  {
    "userId": "12345",
    "token": "<jwt_token>"
  }
  ```
- **Response (Error - 401 Unauthorized):** If credentials are invalid.

### 1.3. Validation Rules
- `name`: Required, string, min 2 characters.
- `email`: Required, must be a valid email format, must be unique.
- `password`: Required, string, min 8 characters, at least one uppercase, one lowercase, one number, and one special character.
- `role`: Required, must be either `Guest` or `Host`.

### 1.4. Performance Criteria
- API response time for registration and login should be under 300ms.

---

## 2. Property Management

### 2.1. Functional Requirements
- Authenticated users with the `Host` role must be able to create, update, and delete property listings.
- All users (including unauthenticated ones) must be able to view property listings.
- The system must store property details including title, description, location, price, amenities, and photos.

### 2.2. API Endpoints

#### `POST /api/properties`
- **Description:** Creates a new property listing.
- **Authentication:** Required (Host role).
- **Request Body:** Includes property details (title, description, location, price, etc.).
- **Response (Success - 201 Created):** The newly created property object.

#### `GET /api/properties/:id`
- **Description:** Retrieves a single property by its ID.
- **Authentication:** Not required.
- **Response (Success - 200 OK):** The property object.
- **Response (Error - 404 Not Found):** If property does not exist.

#### `PUT /api/properties/:id`
- **Description:** Updates an existing property.
- **Authentication:** Required (Host role, must be owner of the property).
- **Request Body:** Fields to be updated.
- **Response (Success - 200 OK):** The updated property object.

#### `DELETE /api/properties/:id`
- **Description:** Deletes a property.
- **Authentication:** Required (Host role, must be owner of the property).
- **Response (Success - 204 No Content):**

### 2.3. Validation Rules
- `title`: Required, string, min 5 characters.
- `description`: Required, string, min 20 characters.
- `price`: Required, number, greater than 0.
- `location`: Required, string.

### 2.4. Performance Criteria
- Property search and retrieval should be optimized, with response times under 500ms.

---

## 3. Booking System

### 3.1. Functional Requirements
- Authenticated users with the `Guest` role must be able to book a property for a specific date range.
- The system must prevent double-bookings for the same property on the same dates.
- Both Guests and Hosts should be able to cancel a booking, subject to cancellation policies.

### 3.2. API Endpoints

#### `POST /api/bookings`
- **Description:** Creates a new booking for a property.
- **Authentication:** Required (Guest role).
- **Request Body:**
  ```json
  {
    "propertyId": "prop123",
    "checkInDate": "2024-12-20",
    "checkOutDate": "2024-12-25"
  }
  ```
- **Response (Success - 201 Created):** The new booking object.
- **Response (Error - 400 Bad Request):** If dates are invalid or property is unavailable.

#### `GET /api/bookings`
- **Description:** Retrieves a list of bookings for the authenticated user (Guest or Host).
- **Authentication:** Required.
- **Response (Success - 200 OK):** An array of booking objects.

#### `PUT /api/bookings/:id/cancel`
- **Description:** Cancels a booking.
- **Authentication:** Required (Guest who made the booking or Host who owns the property).
- **Response (Success - 200 OK):** The updated booking object with `status: "canceled"`.

### 3.3. Validation Rules
- `propertyId`: Required, must be a valid and existing property ID.
- `checkInDate`: Required, must be a valid date in the future.
- `checkOutDate`: Required, must be a valid date after `checkInDate`.

### 3.4. Performance Criteria
- Booking creation and validation should have a response time under 400ms.
