# User Registration Process Flowchart

This document provides a textual representation of the flowchart for the user registration process in the Airbnb Clone backend.

```
[ Start ]
    |
    v
[ User navigates to registration page ]
    |
    v
[ User fills and submits registration form (Name, Email, Password, Role) ]
    |
    v
< Is the submitted data valid? >
    |        ^
    |-- No -->[ Show error message ]--|
    |
    `-- Yes
        |
        v
< Does user with this email already exist? >
    |        ^
    |-- Yes ->[ Show "User already exists" error ]--|
    |
    `-- No
        |
        v
[ Hash the user's password ]
    |
    v
[ Save new user to the database ]
    |
    v
[ Generate JWT for user session ]
    |
    v
[ Send welcome email via Email Service ]
    |
    v
< Was the email sent successfully? >
    |        
    |-- No -->[ Log email sending failure ]
    |           |
    |-----------`
    |
    `-- Yes
        |
        v
[ Redirect user to their dashboard ]
    |
    v
[ End ]
```

## Flowchart Steps Explained

1.  **Start:** The process begins.
2.  **Navigate to Registration:** The user accesses the registration page.
3.  **Fill and Submit Form:** The user provides their details (name, email, password, and chosen role) and submits the form.
4.  **Validate Data:** The system checks if the provided data is in the correct format (e.g., valid email, strong password).
    -   If invalid, it displays an error and waits for the user to correct the information.
5.  **Check for Existing User:** The system checks if the email is already registered in the database.
    -   If it exists, it displays an error to prevent duplicate accounts.
6.  **Hash Password:** The user's plain-text password is securely hashed before storage.
7.  **Save User:** The new user's account information is saved to the `Users` table in the database.
8.  **Generate JWT:** A JSON Web Token is created to manage the user's session after registration.
9.  **Send Welcome Email:** The system requests the Email Service to send a welcome email to the user.
10. **Check Email Status:** The system checks if the email was sent successfully. A failure is logged, but it does not stop the registration process.
11. **Redirect to Dashboard:** The user is redirected to their personalized dashboard (e.g., Guest or Host dashboard).
12. **End:** The process is complete.
