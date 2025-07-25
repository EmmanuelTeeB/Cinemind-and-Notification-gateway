# Use case 1: User registration(Sign up)
## 1.Overview
  **Actor**: New user
  **Goal**: To create a new user account
  **Preconditions**: 
   -User has not registered before.
   -User has access to email.
  **Postconditions**:
   -User credentials are stored in the Database.
   -User is registered and redirected to login.

## 2. Main flow
   -User clicks 'Sign up'.
   -Enter email, username, password.
   -System validates inputs.
   -Password is hashed and stored.
   -User record is saved to a Database.
   -System sends a confirmation message.
   -User is redirected to login page.

## 3. Alternate flow
  -Email already exists ->Shows "Email already in use"
  -Weak password ->Show validation error.

# Use case 2: User Login
## 1.Overview
  **Actor**: Registered user
  **Goal**: To gain access to their account.
  **Preconditions**:
   -User is registered.
   -Correct credentials.
  **Postconditions**:
   -User is logged in, JWT token issued
 
 ## 2. Main Flow
   -User enters email/username and password.
   -System verifies credentials.
   -If valid, token is issued
   -Redirect user to dashboard/home.

## 3. Alternate Flow
  -Wrong credentials.

# User case 3: Logout
## 1.Overview:
  **Actor**: Logged in
  **Goal**: To terminate current session.
  **Preconditions**:
   -Valid session.
  **Postconditions**:
   -Token is destroyed, session ended.

## 2. Main Flow
 -User clicks 'Logout'.
 -Token is invalidated.
 -Redirected to landing page.
