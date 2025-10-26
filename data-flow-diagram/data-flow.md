# Airbnb Clone Data Flow Diagram (DFD)

This document provides a textual representation of the Data Flow Diagram for the Airbnb Clone backend.

## Level 0: Context Diagram

The context diagram shows the entire system as a single process and its interactions with external entities.

- **External Entities:**
  - Guest
  - Host
  - Admin
  - Payment Gateway
  - Email Service

- **Process:**
  - Airbnb Clone Backend System

- **Data Flows:**
  - **Guest -> System:** Registration Info, Login Credentials, Profile Updates, Search Queries, Booking Requests, Cancellation Requests, Review Data
  - **System -> Guest:** User Profile, Property Information, Booking Confirmations, Search Results
  - **Host -> System:** Registration Info, Login Credentials, Profile Updates, Property Details, Booking Responses, Cancellation Requests
  - **System -> Host:** User Profile, Booking Notifications, Payout Information, Review Notifications
  - **Admin -> System:** Login Credentials, Management Commands (Manage Users, Listings, Bookings)
  - **System -> Admin:** Dashboard Data (Users, Listings, Bookings, Payments)
  - **System -> Payment Gateway:** Payment Request (Amount, User Details)
  - **Payment Gateway -> System:** Payment Confirmation/Failure
  - **System -> Email Service:** Email Content (Recipient, Subject, Body)
  - **Email Service -> System:** Email Sent Confirmation

## Level 1: Detailed DFD

The Level 1 DFD breaks down the main process into smaller, more detailed processes.

- **External Entities:** Guest, Host, Admin, Payment Gateway, Email Service

- **Processes:**
  1.  **User Management**
  2.  **Property Management**
  3.  **Booking Management**
  4.  **Payment System**
  5.  **Notification System**
  6.  **Review System**

- **Data Stores:**
  - `DS1: Users`
  - `DS2: Properties`
  - `DS3: Bookings`
  - `DS4: Payments`
  - `DS5: Reviews`

- **Data Flows:**

  - **From Guest:**
    - `Guest Registration Info` -> (1) User Management -> `DS1: Users`
    - `Guest Login Credentials` -> (1) User Management -> `DS1: Users`
    - `Booking Request` -> (3) Booking Management -> `DS3: Bookings`
    - `Payment Details` -> (4) Payment System
    - `Review Data` -> (6) Review System -> `DS5: Reviews`

  - **From Host:**
    - `Host Registration Info` -> (1) User Management -> `DS1: Users`
    - `Property Details` -> (2) Property Management -> `DS2: Properties`
    - `Booking Response` -> (3) Booking Management -> `DS3: Bookings`

  - **From Admin:**
    - `Admin Commands` -> (1) User Management, (2) Property Management, (3) Booking Management

  - **Process to Process:**
    - `Booking Details` -> (3) Booking Management -> (4) Payment System
    - `Payment Confirmation` -> (4) Payment System -> (3) Booking Management
    - `Notification Request` -> (3) Booking Management -> (5) Notification System
    - `Notification Request` -> (4) Payment System -> (5) Notification System

  - **To External Entities:**
    - `Payment Request` -> (4) Payment System -> Payment Gateway
    - `Email Request` -> (5) Notification System -> Email Service
    - `Property Info` -> `DS2: Properties` -> Guest
    - `Booking Confirmation` -> `DS3: Bookings` -> Guest/Host
