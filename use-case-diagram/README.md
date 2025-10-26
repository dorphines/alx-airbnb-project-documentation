# Airbnb Clone Use Case Diagram

This document provides a textual representation of the use case diagram for the Airbnb Clone backend.

## 1. Actors

- **Guest:** A user who books properties.
- **Host:** A user who lists and manages properties.
- **Admin:** A user who oversees the platform.
- **System:** The backend application.
- **Payment Gateway:** External service for processing payments.
- **Email Service:** External service for sending notifications.

## 2. Use Cases

### 2.1. Guest Use Cases

- **Register Account:**
  - Description: A guest creates a new account.
  - Actor: Guest
- **Login to Account:**
  - Description: A guest logs into their account.
  - Actor: Guest
- **Manage Profile:**
  - Description: A guest updates their profile information.
  - Actor: Guest
- **Search for Properties:**
  - Description: A guest searches for properties based on various criteria.
  - Actor: Guest
- **Filter Search Results:**
  - Description: A guest filters search results.
  - Actor: Guest
- **Book a Property:**
  - Description: A guest books a property for specific dates.
  - Actor: Guest
  - Includes: Process Payment
- **Cancel Booking:**
  - Description: A guest cancels a booking.
  - Actor: Guest
- **Leave a Review:**
  - Description: A guest leaves a review and rating for a property after a stay.
  - Actor: Guest
- **Receive Notifications:**
  - Description: A guest receives email notifications for booking updates.
  - Actor: Guest

### 2.2. Host Use Cases

- **Register Account:**
  - Description: A host creates a new account.
  - Actor: Host
- **Login to Account:**
  - Description: A host logs into their account.
  - Actor: Host
- **Manage Profile:**
  - Description: A host updates their profile information.
  - Actor: Host
- **Create Property Listing:**
  - Description: A host creates a new property listing.
  - Actor: Host
- **Update Property Listing:**
  - Description: A host updates an existing property listing.
  - Actor: Host
- **Delete Property Listing:**
  - Description: A host removes a property listing.
  - Actor: Host
- **Manage Bookings:**
  - Description: A host views and manages bookings for their properties.
  - Actor: Host
- **Cancel Booking:**
  - Description: A host cancels a booking.
  - Actor: Host
- **Respond to Review:**
  - Description: A host responds to a review left by a guest.
  - Actor: Host
- **Receive Payouts:**
  - Description: A host receives payments for completed bookings.
  - Actor: Host
- **Receive Notifications:**
  - Description: A host receives email notifications for booking updates.
  - Actor: Host

### 2.3. Admin Use Cases

- **Login to Dashboard:**
  - Description: An admin logs into the admin dashboard.
  - Actor: Admin
- **Manage Users:**
  - Description: An admin views, suspends, or deletes user accounts.
  - Actor: Admin
- **Manage Listings:**
  - Description: An admin views or removes property listings.
  - Actor: Admin
- **Manage Bookings:**
  - Description: An admin views or cancels bookings.
  - Actor: Admin
- **Monitor Payments:**
  - Description: An admin monitors payment transactions.
  - Actor: Admin

### 2.4. System Use Cases

- **Process Payment:**
  - Description: The system processes a payment through a payment gateway.
  - Trigger: Guest books a property.
  - Interacts with: Payment Gateway
- **Send Email Notification:**
  - Description: The system sends an email notification.
  - Trigger: Booking status change, payment update.
  - Interacts with: Email Service
- **Validate Data:**
  - Description: The system validates all incoming data from users.
- **Authenticate User:**
  - Description: The system authenticates user credentials.
- **Authorize User:**
  - Description: The system checks if a user has permission to perform an action.
