# [BugBusters API Integration Documentation ![BugBusters API Integration Documentation](https://i.ibb.co/RCdFLsf/bugbusters-logo.png)](https://app.swaggerhub.com/apis/BugBusters_HNG/bugbusters/0.0.1) 

## Overview

This document provides an overview of the BugBusters API, outlining its structure, dependencies, setup instructions, and folder organization.

- **Authentication:** Secure user login, registration, and social authentication (Google, Facebook, Twitter), magic link.
  
- **Authorization:** Role-based access control (RBAC) ensures secure access to endpoints (Amin, user roles).
  
- **User Management:** CRUD operations for user profiles, password resets, and profile settings.
  
- **Organization Management:** CRUD operations for managing organizations, with admin-specific routes for organizational settings.
  
- **Email and Messaging:** Endpoints for managing emails, invites, waitlists and messages, including CRUD operations.
  
- **Payment Processing:** Secure endpoints for processing payments.
  
- **Customization:** Configuration options for settings, dashboard, charts, widgets and email templates.
  
- **Error Handling:** Consistent handling of errors with appropriate status codes and messages.

Base URL
Live URL: https://example.com/api/v1
Staging URL: https://staging.example.com/api/v1



We have created Markdown  for each endpoint as described in the OpenAPI specification. Each contains the endpoint's path, method, summary, tags, request body, and responses. Below are the contents of the files for each endpoint:

### 1. `auth_login`
```markdown
# POST /auth/login

## Summary
User Login

## Tags
- Authentication

## Request Body
- **email** (string, format: email, example: user@example.com)
- **password** (string, format: password, example: password123)

## Responses
### 200: Login successful
- **token** (string)

### 401: Invalid credentials
- **error** (string, example: Invalid email or password)

### 500: Internal Server Error
- **error** (string, example: An unexpected error occurred)
```

### 2. `auth_register`
```markdown
# POST /auth/register

## Summary
User Registration

## Tags
- Authentication

## Request Body
- **username** (string, example: john_doe)
- **email** (string, format: email, example: user@example.com)
- **password** (string, format: password, example: password123)

## Responses
### 201: User registered successfully
- **token** (string)

### 400: Bad request
- **error** (string, example: Invalid input data)

### 500: Internal Server Error
- **error** (string, example: An unexpected error occurred)
```

### 3. `auth_social`
```markdown
# POST /auth/social

## Summary
Social Authentication

## Tags
- Authentication

## Request Body
- **provider** (string, enum: [google, facebook, twitter], example: google)
- **token** (string, example: soc1alt0ken)

## Responses
### 200: Authentication successful
- **token** (string)

### 400: Bad request
- **error** (string, example: Invalid input data)

### 500: Internal Server Error
- **error** (string, example: An unexpected error occurred)
```

### 4. `auth_magic_link`
```markdown
# POST /auth/magic-link

## Summary
Magic Link Authentication

## Tags
- Authentication

## Request Body
- **email** (string, format: email, example: user@example.com)

## Responses
### 200: Magic link sent
- **message** (string, example: Magic link sent successfully)

### 400: Bad request
- **error** (string, example: Invalid input data)

### 500: Internal Server Error
- **error** (string, example: An unexpected error occurred)
```

### 5. `auth_password_reset_request`
```markdown
# POST /auth/password-reset-request

## Summary
Request Password Reset

## Tags
- Authentication

## Description
Request a password reset link to be sent to the user's email

## Request Body
- **email** (string, format: email, example: user@example.com)

## Responses
### 200: Password reset email sent
- **message** (string, example: Password reset email sent successfully)

### 400: Bad request
- **error** (string, example: Invalid input data)

### 404: User not found
- **error** (string, example: User not found)

### 500: Internal Server Error
- **error** (string, example: An unexpected error occurred)
```

### 6. `auth_reset_password`
```markdown
# POST /auth/reset-password

## Summary
Reset Password

## Tags
- Authentication

## Description
Reset the user's password using a reset token

## Request Body
- **token** (string, description: Password reset token, example: 1a2b3c4d5e6f7g8h9i0j)
- **newPassword** (string, format: password, description: The new password, example: newPassword123)

## Responses
### 200: Password reset successful
- **message** (string, example: Password reset successful)

### 400: Bad request
- **error** (string, example: Invalid input data)

### 404: Invalid or expired token
- **error** (string, example: Invalid or expired token)

### 500: Internal Server Error
- **error** (string, example: An unexpected error occurred)
```

### 7. `users_get`
```markdown
# GET /users

## Summary
List Users

## Tags
- User Management

## Security
- BearerAuth: []

## Responses
### 200: List of users
- Content-Type: application/json
- Schema: 
  ```json
  {
    "type": "array",
    "items": {
      "$ref": "#/components/schemas/User"
    }
  }
  ```

### 400: Bad request
- **error** (string, example: Invalid request parameters)

### 500: Internal Server Error
- **error** (string, example: An unexpected error occurred)
```

### 8. `users_userId_get`
```markdown
# GET /users/{userId}

## Summary
Get User Details

## Tags
- User Management

## Parameters
- **userId** (string, in: path, required: true)

## Security
- BearerAuth: []

## Responses
### 200: User details
- Schema: 
  ```json
  {
    "$ref": "#/components/schemas/User"
  }
  ```

### 404: User not found
- **error** (string, example: User not found)

### 500: Internal Server Error
- **error** (string, example: An unexpected error occurred)
```

### 9. `users_userId_put`
```markdown
# PUT /users/{userId}

## Summary
Update User

## Tags
- User Management

## Parameters
- **userId** (string, in: path, required: true)

## Security
- BearerAuth: []

## Request Body
- Content-Type: application/json
- Schema:
  ```json
  {
    "$ref": "#/components/schemas/User"
  }
  ```

## Responses
### 200: User updated
- **message** (string, example: User updated successfully)

### 404: User not found
- **error** (string, example: User not found)

### 500: Internal Server Error
- **error** (string, example: An unexpected error occurred)
```

### 10. `users_userId_delete`
```markdown
# DELETE /users/{userId}

## Summary
Delete User

## Tags
- User Management

## Parameters
- **userId** (string, in: path, required: true)

## Security
- BearerAuth: []

## Responses
### 200: User deleted
- **message** (string, example: User deleted successfully)

### 404: User not found
- **error** (string, example: User not found)

### 500: Internal Server Error
- **error** (string, example: An unexpected error occurred)
```


### 11. `organisations_get`
```markdown
# GET /organisations

## Summary
Get all organisations

## Tags
- Organisations

## Security
- BearerAuth: []

## Responses
### 200: Successfully retrieved organisations
- Content-Type: application/json
- Schema: 
  ```json
  {
    "status": true,
    "message": "Organisations retrieved successfully",
    "data": [
      {
        "id": "string",
        "name": "string"
      }
    ]
  }
  ```

### 401: Unauthorized
- Content-Type: application/json
- Schema: 
  ```json
  {
    "status": false,
    "message": "Unauthorized"
  }
  ```

### 500: Internal Server Error
- Content-Type: application/json
- Schema: 
  ```json
  {
    "status": false,
    "message": "An unexpected error occurred"
  }
  ```
```

### 12. `organisations_post`
```markdown
# POST /organisations

## Summary
Create an organisation

## Tags
- Organisations

## Security
- BearerAuth: []

## Request Body
- Content-Type: application/json
- Schema:
  ```json
  {
    "name": "New Organisation"
  }
  ```

## Responses
### 201: Organisation created successfully
- Content-Type: application/json
- Schema: 
  ```json
  {
    "status": true,
    "message": "Organisation created successfully",
    "data": {
      "id": "string",
      "name": "string"
    }
  }
  ```

### 400: Bad request
- Content-Type: application/json
- Schema: 
  ```json
  {
    "status": false,
    "message": "Invalid input data"
  }
  ```

### 500: Internal Server Error
- Content-Type: application/json
- Schema: 
  ```json
  {
    "status": false,
    "message": "An unexpected error occurred"
  }
  ```
```

### 13. `organisations_id_get`
```markdown
# GET /organisations/{id}

## Summary
Get an organisation by ID

## Tags
- Organisations

## Security
- BearerAuth: []

## Parameters
- **id** (string, in: path, required: true, description: ID of the organisation)

## Responses
### 200: Successfully retrieved organisation
- Content-Type: application/json
- Schema: 
  ```json
  {
    "status": true,
    "message": "Organisation retrieved successfully",
    "data": {
      "id": "string",
      "name": "string"
    }
  }
  ```

### 401: Unauthorized
- Content-Type: application/json
- Schema: 
  ```json
  {
    "status": false,
    "message": "Unauthorized"
  }
  ```

### 404: Organisation not found
- Content-Type: application/json
- Schema: 
  ```json
  {
    "status": false,
    "message": "Organisation not found"
  }
  ```

### 500: Internal Server Error
- Content-Type: application/json
- Schema: 
  ```json
  {
    "status": false,
    "message": "An unexpected error occurred"
  }
  ```
```

### 14. `organisations_id_put`
```markdown
# PUT /organisations/{id}

## Summary
Update an organisation by ID

## Tags
- Organisations

## Security
- BearerAuth: []

## Parameters
- **id** (string, in: path, required: true, description: ID of the organisation)

## Request Body
- Content-Type: application/json
- Schema:
  ```json
  {
    "name": "Updated Organisation"
  }
  ```

## Responses
### 200: Organisation updated successfully
- Content-Type: application/json
- Schema: 
  ```json
  {
    "status": true,
    "message": "Organisation updated successfully",
    "data": {
      "id": "string",
      "name": "string"
    }
  }
  ```

### 400: Bad request
- Content-Type: application/json
- Schema: 
  ```json
  {
    "status": false,
    "message": "Invalid input data"
  }
  ```

### 401: Unauthorized
- Content-Type: application/json
- Schema: 
  ```json
  {
    "status": false,
    "message": "Unauthorized"
  }
  ```

### 404: Organisation not found
- Content-Type: application/json
- Schema: 
  ```json
  {
    "status": false,
    "message": "Organisation not found"
  }
  ```

### 500: Internal Server Error
- Content-Type: application/json
- Schema: 
  ```json
  {
    "status": false,
    "message": "An unexpected error occurred"
  }
  ```
```

### 15. `organisations_id_delete`
```markdown
# DELETE /organisations/{id}

## Summary
Delete an organisation by ID

## Tags
- Organisations

## Security
- BearerAuth: []

## Parameters
- **id** (string, in: path, required: true, description: ID of the organisation)

## Responses
### 200: Organisation deleted successfully
- Content-Type: application/json
- Schema: 
  ```json
  {
    "status": true,
    "message": "Organisation deleted successfully"
  }
  ```

### 401: Unauthorized
- Content-Type: application/json
- Schema: 
  ```json
  {
    "status": false,
    "message": "Unauthorized"
  }
  ```

### 404: Organisation not found
- Content-Type: application/json
- Schema: 
  ```json
  {
    "status": false,
    "message": "Organisation not found"
  }
  ```

### 500: Internal Server Error
- Content-Type: application/json
- Schema: 
  ```json
  {
    "status": false,
    "message": "An unexpected error occurred"
  }
  ```
```

### 16. `organisations_admin_get`
```markdown
# GET /organisations/admin

## Summary
Get all organisations (Admin)

## Tags
- Organisations Admin

## Security
- BearerAuth: []

## Responses
### 200: Successfully retrieved organisations
- Content-Type: application/json
- Schema: 
  ```json
  {
    "status": true,
    "message": "Organisations retrieved successfully",
    "data": [
      {
        "id": "string",
        "name": "string"
      }
    ]
  }
  ```

### 401: Unauthorized
- Content-Type: application/json
- Schema: 
  ```json
  {
    "status": false,
    "message": "Unauthorized"
  }
  ```

### 500: Internal Server Error
- Content-Type: application/json
- Schema: 
  ```json
  {
    "status": false,
    "message": "An unexpected error occurred"
  }
  ```
```

### 17. `organisations_admin_id_get`
```markdown
# GET /organisations/admin/{id}

## Summary
Get an organisation by ID (Admin)

## Tags
- Organisations Admin

## Security
- BearerAuth: []

## Parameters
- **id** (string, in: path, required: true, description: ID of the organisation)

## Responses
### 200: Successfully retrieved organisation
- Content-Type: application/json
- Schema: 
  ```json
  {
    "status": true,
    "message": "Organisation retrieved successfully",
    "data": {
      "id": "string",
      "name": "string"
    }
  }
  ```

### 401: Unauthorized
- Content-Type: application/json
- Schema: 
  ```json
  {
    "status": false,
    "message": "Unauthorized"
  }
  ```

### 404: Organisation not found
- Content-Type: application/json
- Schema: 
  ```json
  {
    "status": false,
    "message": "Organisation not found"
  }
  ```

### 500: Internal Server Error
- Content-Type: application/json
- Schema: 
  ```json
  {
    "status": false,
    "message": "An unexpected error occurred"
  }
  ```
```

### 18. `organisations_admin_id_put`
```markdown
# PUT /organisations/admin/{id}

## Summary
Update an organisation by ID (Admin)

## Tags
- Organisations Admin

## Security
- BearerAuth: []

## Parameters
- **id** (string, in: path, required: true, description: ID of the organisation)

## Request Body
- Content-Type: application/json
- Schema:
  ```json
  {
    "name": "Updated Organisation"
  }
  ```

## Responses
### 200: Organisation updated successfully
- Content-Type: application/json
- Schema: 
  ```json
  {
    "status": true,
    "message": "Organisation updated successfully",
    "data": {
      "id": "string",
      "name": "string"
    }
  }
  ```

### 400: Bad request
- Content-Type: application/json
- Schema: 
  ```json
  {
    "status": false,
    "message": "Invalid input data"
  }
  ```

### 401: Unauthorized
- Content-Type: application/json
- Schema: 


  ```json
  {
    "status": false,
    "message": "Unauthorized"
  }
  ```

### 404: Organisation not found
- Content-Type: application/json
- Schema: 
  ```json
  {
    "status": false,
    "message": "Organisation not found"
  }
  ```

### 500: Internal Server Error
- Content-Type: application/json
- Schema: 
  ```json
  {
    "status": false,
    "message": "An unexpected error occurred"
  }
  ```
```

### 19. `organisations_admin_id_delete`
```markdown
# DELETE /organisations/admin/{id}

## Summary
Delete an organisation by ID (Admin)

## Tags
- Organisations Admin

## Security
- BearerAuth: []

## Parameters
- **id** (string, in: path, required: true, description: ID of the organisation)

## Responses
### 200: Organisation deleted successfully
- Content-Type: application/json
- Schema: 
  ```json
  {
    "status": true,
    "message": "Organisation deleted successfully"
  }
  ```

### 401: Unauthorized
- Content-Type: application/json
- Schema: 
  ```json
  {
    "status": false,
    "message": "Unauthorized"
  }
  ```

### 404: Organisation not found
- Content-Type: application/json
- Schema: 
  ```json
  {
    "status": false,
    "message": "Organisation not found"
  }
  ```

### 500: Internal Server Error
- Content-Type: application/json
- Schema: 
  ```json
  {
    "status": false,
    "message": "An unexpected error occurred"
  }
  ```
```

Let me know if you need any adjustments or additional information!




## Contact Us Form Submission

**Endpoint:** /api/[version]/contact-us  
**Method:** POST  
**Description:** Contact Us Form Submission endpoint.

**Body:**
```json
{
  "name": "John Doe",
  "email": "johndoe@example.com",
  "message": "Your message here"
}
```

**Success Response:**

Code: 200
Content:
```json
{
  "status": true,
  "message": "Form submitted successfully",
  "data": {
    "message": "Form submitted successfully"
  }
}
```

**Error Responses:**

Code: 400
Content:
```json
{
  "status": false,
  "message": "Invalid input data"
}
```

---

## List Notifications

**Endpoint:** /api/[version]/notifications  
**Method:** GET  
**Description:** Endpoint to list all notifications.

**Success Response:**

Code: 200
Content:
```json
{
  "status": true,
  "message": "List of notifications",
  "data": [
    {
      "id": "1",
      "message": "Notification message 1"
    },
    {
      "id": "2",
      "message": "Notification message 2"
    }
    // Add more notification objects as needed
  ]
}
```

**Error Responses:**

Code: 500
Content:
```json
{
  "status": false,
  "message": "An unexpected error occurred"
}
```

**Endpoint:** /api/[version]/notifications  
**Method:** POST  
**Description:** Endpoint to send a notification.

**Body:**
```json
{
  "message": "Notification message"
}
```

**Success Response:**

Code: 200
Content:
```json
{
  "status": true,
  "message": "Notification sent successfully",
  "data": {
    "message": "Notification sent successfully"
  }
}
```

**Error Responses:**

Code: 400
Content:
```json
{
  "status": false,
  "message": "Invalid input data"
}
```

---

## Get a Notification

**Endpoint:** /api/[version]/notifications/{notificationId}  
**Method:** GET  
**Description:** Endpoint to get a specific notification.

**Success Response:**

Code: 200
Content:
```json
{
  "status": true,
  "message": "Notification retrieved successfully",
  "data": {
    "id": "1",
    "message": "Notification message"
  }
}
```

**Error Responses:**

Code: 500
Content:
```json
{
  "status": false,
  "message": "An unexpected error occurred"
}
```

**Endpoint:** /api/[version]/notifications/{notificationId}  
**Method:** DELETE  
**Description:** Endpoint to delete a specific notification.

**Success Response:**

Code: 200
Content:
```json
{
  "status": true,
  "message": "Notification deleted successfully",
  "data": {
    "message": "Notification deleted successfully"
  }
}
```

**Error Responses:**

Code: 404
Content:
```json
{
  "status": false,
  "message": "Notification not found"
}
```

---

## Get Settings

**Endpoint:** /api/[version]/settings  
**Method:** GET  
**Description:** Endpoint to get application settings.

**Success Response:**

Code: 200
Content:
```json
{
  "status": true,
  "message": "Settings retrieved successfully",
  "data": {
    "setting1": "value1",
    "setting2": "value2"
  }
}
```

**Error Responses:**

Code: 500
Content:
```json
{
  "status": false,
  "message": "An unexpected error occurred"
}
```

**Endpoint:** /api/[version]/settings  
**Method:** PUT  
**Description:** Endpoint to update application settings.

**Body:**
```json
{
  "setting1": "new value1",
  "setting2": "new value2"
}
```

**Success Response:**

Code: 200
Content:
```json
{
  "status": true,
  "message": "Settings updated successfully",
  "data": {
    "message": "Settings updated successfully"
  }
}
```

**Error Responses:**

Code: 400
Content:
```json
{
  "status": false,
  "message": "Invalid input data"
}
```

---

## Retrieve Profile Settings

**Endpoint:** /api/[version]/profile-settings  
**Method:** GET  
**Description:** Endpoint to retrieve profile settings.

**Success Response:**

Code: 200
Content:
```json
{
  "status": true,
  "message": "Profile settings retrieved successfully",
  "data": {
    "profileSetting1": "value1",
    "profileSetting2": "value2"
  }
}
```

**Error Responses:**

Code: 500
Content:
```json
{
  "status": false,
  "message": "An unexpected error occurred"
}
```

**Endpoint:** /api/[version]/profile-settings  
**Method:** PUT  
**Description:** Endpoint to update profile settings.

**Body:**
```json
{
  "profileSetting1": "new value1",
  "profileSetting2": "new value2"
}
```

**Success Response:**

Code: 200
Content:
```json
{
  "status": true,
  "message": "Profile settings updated successfully",
  "data": {
    "message": "Profile settings updated successfully"
  }
}
```

**Error Responses:**

Code: 400
Content:
```json
{
  "status": false,
  "message": "Invalid input data"
}
```
```
Here's the complete Markdown file with all the endpoints formatted according to the OpenAPI specification:

```markdown
# API Endpoints Documentation

## /waitlist

### POST /api/[version]/waitlist

**Summary:** Add to Waitlist  
**Tags:** Waitlist  
**Request Body:**
```json
{
  "email": "user@example.com"
}
```

**Responses:**

**200**  
Description: Added to waitlist  
```json
{
  "message": "Added to waitlist successfully"
}
```

**400**  
Description: Bad request  
```json
{
  "error": "Invalid input data"
}
```

**500**  
Description: Internal Server Error  
```json
{
  "error": "An unexpected error occurred"
}
```

---

## /invite

### GET /api/[version]/invite

**Summary:** Retrieve Invite List  
**Tags:** Invite Flow  
**Security:** Requires Bearer Token  

**Responses:**

**200**  
Description: List of invites retrieved successfully  
```json
[
  {
    "$ref": "#/components/schemas/Invite"
  }
]
```

**401**  
Description: Unauthorized  
```json
{
  "error": "Unauthorized access"
}
```

**500**  
Description: Internal Server Error  
```json
{
  "error": "An unexpected error occurred"
}
```

### POST /api/[version]/invite

**Summary:** Send an Invite  
**Tags:** Invite Flow  
**Request Body:**
```json
{
  "$ref": "#/components/schemas/Invite"
}
```

**Security:** Requires Bearer Token  

**Responses:**

**200**  
Description: Invite sent  
```json
{
  "message": "Invite sent successfully"
}
```

**400**  
Description: Bad request  
```json
{
  "error": "Invalid input data"
}
```

**500**  
Description: Internal Server Error  
```json
{
  "error": "An unexpected error occurred"
}
```

---

## /user-data

### GET /api/[version]/user-data

**Summary:** Retrieve User Data  
**Tags:** User Data  
**Security:** Requires Bearer Token  

**Responses:**

**200**  
Description: User data retrieved successfully  
```json
[
  {
    "$ref": "#/components/schemas/UserData"
  }
]
```

**401**  
Description: Unauthorized access  
```json
{
  "error": "Unauthorized access"
}
```

**500**  
Description: Internal Server Error  
```json
{
  "error": "An unexpected error occurred"
}
```

### POST /api/[version]/user-data

**Summary:** Create User Data  
**Tags:** User Data  
**Security:** Requires Bearer Token  
**Request Body:**
```json
{
  "$ref": "#/components/schemas/UserData"
}
```

**Responses:**

**201**  
Description: User data created successfully  
```json
{
  "message": "User data created successfully"
}
```

**400**  
Description: Bad request  
```json
{
  "error": "Invalid input data"
}
```

**401**  
Description: Unauthorized access  
```json
{
  "error": "Unauthorized access"
}
```

**500**  
Description: Internal Server Error  
```json
{
  "error": "An unexpected error occurred"
}
```

### GET /api/[version]/user-data/{userId}

**Summary:** Retrieve User Data by ID  
**Tags:** User Data  
**Security:** Requires Bearer Token  
**Parameters:**
- userId (path)

**Responses:**

**200**  
Description: User data retrieved successfully  
```json
{
  "$ref": "#/components/schemas/UserData"
}
```

**404**  
Description: User data not found  
```json
{
  "error": "User data not found"
}
```

**401**  
Description: Unauthorized access  
```json
{
  "error": "Unauthorized access"
}
```

**500**  
Description: Internal Server Error  
```json
{
  "error": "An unexpected error occurred"
}
```

### PUT /api/[version]/user-data/{userId}

**Summary:** Update User Data  
**Tags:** User Data  
**Security:** Requires Bearer Token  
**Parameters:**
- userId (path)  
**Request Body:**
```json
{
  "$ref": "#/components/schemas/UserData"
}
```

**Responses:**

**200**  
Description: User data updated successfully  
```json
{
  "message": "User data updated successfully"
}
```

**404**  
Description: User data not found  
```json
{
  "error": "User data not found"
}
```

**401**  
Description: Unauthorized access  
```json
{
  "error": "Unauthorized access"
}
```

**500**  
Description: Internal Server Error  
```json
{
  "error": "An unexpected error occurred"
}
```

### DELETE /api/[version]/user-data/{userId}

**Summary:** Delete User Data  
**Tags:** User Data  
**Security:** Requires Bearer Token  
**Parameters:**
- userId (path)  

**Responses:**

**200**  
Description: User data deleted successfully  
```json
{
  "message": "User data deleted successfully"
}
```

**404**  
Description: User data not found  
```json
{
  "error": "User data not found"
}
```

**401**  
Description: Unauthorized access  
```json
{
  "error": "Unauthorized access"
}
```

**500**  
Description: Internal Server Error  
```json
{
  "error": "An unexpected error occurred"
}
```

```
Here's the expanded Markdown file with the additional endpoints formatted according to the OpenAPI specification:

```markdown
# API Endpoints Documentation

## /random-data

### GET /api/[version]/random-data

**Summary:** List Random Data  
**Tags:** Random Data  

**Responses:**

**200**  
Description: List of random data  
```json
[
  {
    "$ref": "#/components/schemas/RandomData"
  }
]
```

**500**  
Description: Internal Server Error  
```json
{
  "error": "An unexpected error occurred"
}
```

### GET /api/[version]/random-data/{dataId}

**Summary:** View Single Data Item  
**Tags:** Random Data  
**Parameters:**
- dataId (path)

**Responses:**

**200**  
Description: Random data item details  
```json
{
  "$ref": "#/components/schemas/RandomData"
}
```

**404**  
Description: Data item not found  

**500**  
Description: Internal Server Error  
```json
{
  "error": "An unexpected error occurred"
}
```

---

## /other-data

### GET /api/[version]/other-data

**Summary:** List Other Data with Search and Sorting  
**Tags:** Other Data List  

**Responses:**

**200**  
Description: List of other data  
```json
[
  {
    "$ref": "#/components/schemas/RandomData"
  }
]
```

**500**  
Description: Internal Server Error  
```json
{
  "error": "An unexpected error occurred"
}
```

---

## /charts

### GET /api/[version]/charts

**Summary:** Retrieve Chart Data  
**Tags:** Charts  

**Responses:**

**200**  
Description: Chart data retrieved  
```json
{
  "$ref": "#/components/schemas/Chart"
}
```

**500**  
Description: Internal Server Error  
```json
{
  "error": "An unexpected error occurred"
}
```

---

## /content

### GET /api/[version]/content

**Summary:** Retrieve Content Data for Editing  
**Tags:** Content Edit  

**Responses:**

**200**  
Description: Content data retrieved  
```json
{
  "$ref": "#/components/schemas/Content"
}
```

**500**  
Description: Internal Server Error  
```json
{
  "error": "An unexpected error occurred"
}
```

---

## /blog

### GET /api/[version]/blog

**Summary:** Retrieve Blog Data  
**Tags:** Blog  

**Responses:**

**200**  
Description: Blog data retrieved  
```json
{
  "$ref": "#/components/schemas/Blog"
}
```

**500**  
Description: Internal Server Error  
```json
{
  "error": "An unexpected error occurred"
}
```

---

## /language

### GET /api/[version]/language

**Summary:** Retrieve Available Languages and Regions  
**Tags:** Language & Region  

**Responses:**

**200**  
Description: Languages and regions retrieved  
```json
[
  "string"
]
```

**500**  
Description: Internal Server Error  
```json
{
  "error": "An unexpected error occurred"
}
```

---

## /email

### GET /api/[version]/email

**Summary:** List Emails  
**Tags:** Email Management  
**Security:** Requires Bearer Token  

**Responses:**

**200**  
Description: List of emails retrieved  
```json
[
  {
    "$ref": "#/components/schemas/Email"
  }
]
```

**500**  
Description: Internal Server Error  
```json
{
  "error": "An unexpected error occurred"
}
```

### POST /api/[version]/email

**Summary:** Create Email  
**Tags:** Email Management  
**Security:** Requires Bearer Token  
**Request Body:**
```json
{
  "$ref": "#/components/schemas/Email"
}
```

**Responses:**

**201**  
Description: Email created successfully  
```json
{
  "$ref": "#/components/schemas/Email"
}
```

**400**  
Description: Bad request  
```json
{
  "error": "Invalid input"
}
```

**500**  
Description: Internal Server Error  
```json
{
  "error": "An unexpected error occurred"
}
```

### GET /api/[version]/email/{emailId}

**Summary:** Get Email Details  
**Tags:** Email Management  
**Parameters:**
- emailId (path)  
**Security:** Requires Bearer Token  

**Responses:**

**200**  
Description: Email details retrieved  
```json
{
  "$ref": "#/components/schemas/Email"
}
```

**404**  
Description: Email not found  

**500**  
Description: Internal Server Error  
```json
{
  "error": "An unexpected error occurred"
}
```

### PUT /api/[version]/email/{emailId}

**Summary:** Update Email  
**Tags:** Email Management  
**Parameters:**
- emailId (path)  
**Security:** Requires Bearer Token  
**Request Body:**
```json
{
  "$ref": "#/components/schemas/Email"
}
```

**Responses:**

**200**  
Description: Email updated successfully  
```json
{
  "$ref": "#/components/schemas/Email"
}
```

**404**  
Description: Email not found  

**500**  
Description: Internal Server Error  
```json
{
  "error": "An unexpected error occurred"
}
```

### DELETE /api/[version]/email/{emailId}

**Summary:** Delete Email  
**Tags:** Email Management  
**Parameters:**
- emailId (path)  
**Security:** Requires Bearer Token  

**Responses:**

**200**  
Description: Email deleted successfully  
```json
{
  "message": "Email deleted successfully"
}
```

**404**  
Description: Email not found  

**500**  
Description: Internal Server Error  
```json
{
  "error": "An unexpected error occurred"
}
```

---

## /email-templates

### GET /api/[version]/email-templates

**Summary:** Retrieve and Manage Email Templates  
**Tags:** Email Template Management  

**Responses:**

**200**  
Description: Email templates retrieved  
```json
[
  {
    "$ref": "#/components/schemas/EmailTemplate"
  }
]
```

**500**  
Description: Internal Server Error  
```json
{
  "error": "An unexpected error occurred"
}
```

```
Here's the expanded Markdown file with the newly added endpoints `/messages`, `/messages/{messageId}`, `/payments`, and `/widget` formatted according to the OpenAPI specification:

```markdown
# API Endpoints Documentation

## /messages

### GET /api/[version]/messages

**Summary:** List Messages  
**Tags:** Messages  
**Security:** Requires Bearer Token  

**Responses:**

**200**  
Description: List of messages  
```json
[
  {
    "$ref": "#/components/schemas/Message"
  }
]
```

**401**  
Description: Unauthorized  

**500**  
Description: Internal Server Error  
```json
{
  "error": "An unexpected error occurred"
}
```

### POST /api/[version]/messages

**Summary:** Create a New Message  
**Tags:** Messages  
**Security:** Requires Bearer Token  
**Request Body:**
```json
{
  "$ref": "#/components/schemas/Message"
}
```

**Responses:**

**201**  
Description: Message created successfully  

**400**  
Description: Bad request  

**401**  
Description: Unauthorized  

**500**  
Description: Internal Server Error  
```json
{
  "error": "An unexpected error occurred"
}
```

### GET /api/[version]/messages/{messageId}

**Summary:** Get Message Details  
**Tags:** Messages  
**Parameters:**
- messageId (path)  
**Security:** Requires Bearer Token  

**Responses:**

**200**  
Description: Message details  
```json
{
  "$ref": "#/components/schemas/Message"
}
```

**404**  
Description: Message not found  

**401**  
Description: Unauthorized  

**500**  
Description: Internal Server Error  
```json
{
  "error": "An unexpected error occurred"
}
```

### PUT /api/[version]/messages/{messageId}

**Summary:** Update a Message  
**Tags:** Messages  
**Parameters:**
- messageId (path)  
**Security:** Requires Bearer Token  
**Request Body:**
```json
{
  "$ref": "#/components/schemas/Message"
}
```

**Responses:**

**200**  
Description: Message updated  

**404**  
Description: Message not found  

**401**  
Description: Unauthorized  

**500**  
Description: Internal Server Error  
```json
{
  "error": "An unexpected error occurred"
}
```

### DELETE /api/[version]/messages/{messageId}

**Summary:** Delete a Message  
**Tags:** Messages  
**Parameters:**
- messageId (path)  
**Security:** Requires Bearer Token  

**Responses:**

**200**  
Description: Message deleted  

**404**  
Description: Message not found  

**401**  
Description: Unauthorized  

**500**  
Description: Internal Server Error  
```json
{
  "error": "An unexpected error occurred"
}
```

---

## /payments

### GET /api/[version]/payments

**Summary:** List Payments  
**Tags:** Payments  
**Security:** Requires Bearer Token  

**Responses:**

**200**  
Description: List of payments  
```json
[
  {
    "$ref": "#/components/schemas/Payment"
  }
]
```

**401**  
Description: Unauthorized  

**500**  
Description: Internal Server Error  
```json
{
  "error": "An unexpected error occurred"
}
```

### POST /api/[version]/payments

**Summary:** Create a New Payment  
**Tags:** Payments  
**Security:** Requires Bearer Token  
**Request Body:**
```json
{
  "$ref": "#/components/schemas/Payment"
}
```

**Responses:**

**201**  
Description: Payment created successfully  

**400**  
Description: Bad request  

**401**  
Description: Unauthorized  

**500**  
Description: Internal Server Error  
```json
{
  "error": "An unexpected error occurred"
}
```

---

## /widget

### GET /api/[version]/widget

**Summary:** Retrieve Widgets  
**Tags:** Widgets  
**Security:** Requires Bearer Token  

**Responses:**

**200**  
Description: List of widgets retrieved successfully  
```json
[
  {
    "$ref": "#/components/schemas/Widget"
  }
]
```

**401**  
Description: Unauthorized access  
```json
{
  "error": "Unauthorized access"
}
```

**500**  
Description: Internal Server Error  
```json
{
  "error": "An unexpected error occurred"
}
```

### POST /api/[version]/widget

**Summary:** Create a Widget  
**Tags:** Widgets  
**Security:** Requires Bearer Token  
**Request Body:**
```json
{
  "$ref": "#/components/schemas/Widget"
}
```

**Responses:**

**201**  
Description: Widget created successfully  
```json
{
  "message": "Widget created successfully"
}
```

**400**  
Description: Bad request  

**401**  
Description: Unauthorized access  
```json
{
  "error": "Unauthorized access"
}
```

**500**  
Description: Internal Server Error  
```json
{
  "error": "An unexpected error occurred"
}
```

```
Your updated OpenAPI specification now includes the `/widget/{widgetId}` endpoint with `GET`, `PUT`, and `DELETE` operations for retrieving, updating, and deleting a widget by its ID. Here's the complete Markdown format:

```markdown
# API Endpoints Documentation

## /widget/{widgetId}

### GET /api/[version]/widget/{widgetId}

**Summary:** Retrieve a Widget by ID  
**Tags:** Widgets  
**Security:** Requires Bearer Token  
**Parameters:**
- widgetId (path)  
**Responses:**

**200**  
Description: Widget retrieved successfully  
```json
{
  "$ref": "#/components/schemas/Widget"
}
```

**404**  
Description: Widget not found  
```json
{
  "error": "Widget not found"
}
```

**401**  
Description: Unauthorized access  
```json
{
  "error": "Unauthorized access"
}
```

**500**  
Description: Internal Server Error  
```json
{
  "error": "An unexpected error occurred"
}
```

### PUT /api/[version]/widget/{widgetId}

**Summary:** Update a Widget  
**Tags:** Widgets  
**Security:** Requires Bearer Token  
**Parameters:**
- widgetId (path)  
**Request Body:**
```json
{
  "$ref": "#/components/schemas/Widget"
}
```

**Responses:**

**200**  
Description: Widget updated successfully  

**404**  
Description: Widget not found  

**401**  
Description: Unauthorized access  

**500**  
Description: Internal Server Error  

### DELETE /api/[version]/widget/{widgetId}

**Summary:** Delete a Widget  
**Tags:** Widgets  
**Security:** Requires Bearer Token  
**Parameters:**
- widgetId (path)  
**Responses:**

**200**  
Description: Widget deleted successfully  

**404**  
Description: Widget not found  

**401**  
Description: Unauthorized access  

**500**  
Description: Internal Server Error  

---

## Security

### BearerAuth

Type: HTTP  
Scheme: Bearer  
Bearer format: JWT  

---

## Components

### Schemas

- User
- Notification
- Setting
- ProfileSetting
- Invite
- RandomData
- Chart
- Content
- Blog
- Email
- EmailTemplate
- Message
- Payment
- Widget
- UserData

---

## External Documentation

For more details, visit the [BugBusters API Documentation](https://app.swaggerhub.com/apis/BugBusters_HNG/BugBusters/0.0.1).

## Database Design

[Database ER diagram](https://dbdiagram.io/d/backend-stage-3-task-6691555b9939893daec97fa6)  

[Database Reference](https://dbdocs.io/cyber330d/BugBusters)  Password == @BugBusters    Public Documentaton for DB

[![Database ER diagram](https://i.ibb.co/whKQSsP/backend-stage-3-task-1.png)](https://dbdiagram.io/d/backend-stage-3-task-6691555b9939893daec97fa6)

##Versioning
This API is versioned to ensure backward compatibility and easy maintenance. The current version is 0.0.1

```
