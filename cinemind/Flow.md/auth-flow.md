# Cinemind: Authentication Flow

## Purpose:
- This doocument outlines the user authentication and session management flow for Cinemind. It refines how users sign up, log in, and maintain authenticated sessions securely.

## Features Covered
- User Sign up
- User Login  
- Token issuance and storage  
- Token refresh and expiration  
- Protected route access

## Actors
- **Guest User**: Unauthenticated user accessing public routes
- **Authenticated User**: User with valid session token

## Flow Breakdown
**Trigger**:User submits name, email, password on signup form.

**Flow:**  
- Frontend sends `POST /api/signup` with user data.  
- Backend validates data, hashes password securely  
- Stores new user in `users` table.  
- Issues **JWT access token** (short-lived, for  x minutes).  
- Issues **refresh token** (longer-lived, for x days), stored HTTP-only cookie.  
- Returns access token to frontend.

### 2. User Login  
**Trigger**: User submits email and password.

**Flow:**  
- Frontend sends `POST /api/login` with credentials.  
- Backend verifies password hash.  
- On success, issues new access and refresh tokens as above.  
- Sends refresh token as secure HTTP-only cookie.  
- Returns access token in response body.


### 3. Access Token Usage  
- Frontend stores access token (e.g., in memory or secure storage).  
- Includes access token in `Authorization: Bearer <token>` header on protected API calls.  
- Backend middleware validates access token on each request.


### 4. Token Refresh  
**Trigger:** Access token expires.

**Flow:**  
- Frontend calls `POST /api/token/refresh` endpoint, sending refresh token automatically via HTTP-only cookie.  
- Backend verifies refresh token, issues new access token.  
- Frontend updates stored access token seamlessly.


### 5. Logout  
- Frontend deletes stored access token.  
- Backend invalidates refresh token (optional).  
- Clears refresh token cookie.


## Auth & Security Notes:
- Access tokens are short-lived to reduce risk if stolen.  
- Refresh tokens stored in HTTP-only, Secure cookies to mitigate XSS.  
- Protect against CSRF attacks on refresh endpoint.
- Passwords hashed with bcrypt or Argon2.  
- Use HTTPS in production to secure cookies and tokens.


## Database Schema (Auth-related):

users
•	id (PK)
•	name
•	email (unique)
•	password_hash
•	created_at
•	updated_at
refresh_tokens
•	id (PK)
•	user_id (FK)
•	token_hash
•	issued_at
•	expires_at
•	revoked (boolean)

---

##  Success Criteria: 
- Secure signup and login flows with proper validation.  
- Seamless token refresh without user disruption.  
- Tokens stored securely to protect user data.  
- Logout invalidates tokens properly.
