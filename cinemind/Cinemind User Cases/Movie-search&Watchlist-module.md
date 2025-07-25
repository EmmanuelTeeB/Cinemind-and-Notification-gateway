# Use case 1: Search for Movie
## 1.Overview:
**Actor**: Guest or Logged in user
**Goal**: Explore movies.
**Preconditions**:
  -Internet connection.
**Postconditions**:
  -Search results are displayed.

## 2.Main Flow:
  -User enter search query.
  -Request sent to TMDb API.
  -API returns matching movies.
  -System displays results.

## 3.Alternate Flow:
  -If movie not available, show message. "No movie found"
  -If User submit empty search box,show message."Enter valid name"
  
# User case 2: Add to watchlist
## 1.Overview:
 **Actor**:Logged-in User.
 **Goal**: To bookmark movie for later use.
 **Preconditions**:
   -User is authenticated.
   -Movie exists in TMDb.
 **Postconditions**:
   -Movie added to user's watchlist in Database.

## 2.Main Flow:
  -User clicks "Add to watchlist".
  -Backend verifies movie ID and user auth.
  -Saves record in Watchlist table.
  -Returns success message.

## 3. Alternate Flow:
  - User is not authenticated, display error message, redirect to login page.

# Uset case 3: Remove from Watchlist
## 1.Overview:
 **Actor**: Logged-in User.
 **Goal**: To unbookmark a movie.
 **Preconditions**:
   -Movie is already in watchlist.
 **Postconditions**:
   -Movie removed from Watchlist table.
 
## Main Flow:
  -User clicks "Remove from watchlist".
  -System checks if entry exists.
  -Deletes record from Database.
  -Returns confirmation.
