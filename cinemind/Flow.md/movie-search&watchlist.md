
#  Cinemind:    Movie Search & Watchlist Flow

## Purpose
- This document outlines the full flow for searching movies via    TMDb API and managing a personal watchlist. It distinguishes between guest and authenticated user experiences and defines the interactions between external APIs, the database, and internal services.


##  Features Covered:
- Search for Movies (via TMDb API)
- View Search Results
- Add/Remove Movie to/from Watchlist
- View Personal Watchlist

## Actors:
- Guest user
- Authenticated user

### Guest User:
-  Can search for movies via TMDb API
-  Cannot save to Watchlist
-  Prompted to sign up or log in when attempting restricted actions

### Authenticated User:
-  Can search for movies
-  Can add/remove movies from personal Watchlist
-  Watchlist persists in database

## Flow Breakdown:

### 1. `Search for a Movie` (All Users)
**Trigger**:
- User types into search bar and presses enter.

**Flow**:
1. Frontend calls internal `/api/search?query=batman`
2. Backend relays query to TMDb API:  
   `https://api.themoviedb.org/3/search/movie?query=batman`
3. TMDb responds with movie metadata (title, poster, overview, etc.)
4. Backend returns curated data to frontend
5. Frontend displays results (clickable cards)

### 2. `Add to Watchlist` (Authenticated Users Only)
**Trigger**:
- User clicks “Add to Watchlist” on a movie card

**Flow**:
- Frontend sends `POST /api/watchlist/add` with:
   ```json
   {
     "user_id": 45,
     "movie_id": 123456,
     "movie_data": {
       "title": "The Batman",
       "poster_path": "...",
       "overview": "...",
       "tmdb_id": 123456
     }
   }
- Backend validates user session (via JWT or Cookie)
- Checks if movie already exists in user’s Watchlist
- If not, stores record in watchlist table
- Returns success message + optional new Watchlist snapshot
- Trigger event to Notification Gateway (e.g., send confirmation)

### 3. Remove from Watchlist
**Trigger**:
- User clicks “Remove from Watchlist”

**Flow**:
- Frontend sends DELETE /api/watchlist/remove
- Backend verifies session and deletes record for user/movie combo
- Response returned to frontend to update UI

### 4. View Watchlist
**Trigger**:
- User navigates to /watchlist

**Flow**:
- Frontend calls GET /api/watchlist
- Backend:
       - Verifies user
       - Queries DB for all watchlist entries under user_id
       - Optionally refreshes poster/metadata from TMDb (if stale)
- Returns full Watchlist payload
- Frontend renders cards in grid layout

## Auth & Security:
- All Watchlist actions require authentication
- Session management via:
                - JWT (current choice) stored in HTTP-only cookies
- API routes protected with middleware:
             -  @login_required decorator or equivalent logic

## Database Schema
Table: watchlist

Field	      Type	        Notes
id	         UUID / INT	   Primary key
user_id	     UUID / INT	   Foreign key
tmdb_id	     INT	       Unique per movie
title	     VARCHAR	   Cached title
poster_path	 VARCHAR	   Poster URL (relative or full)
overview	 TEXT	       Short description
created_at	 TIMESTAMP	   Entry added time

## External API: TMDb
- Rate-limited to ~40 requests every 10 seconds
- No auth needed for public movie data
- API key stored as environment variable (TMDB_API_KEY)


## Integration Points:
- Search → External API (TMDb)
- Watchlist Add/Remove → DB insert/delete
- Watchlist View → DB query
- Notification Gateway Event when added to Watchlist

## Edge Cases:
- Duplicate movie added → should be ignored
- User removes nonexistent movie → safe fail
- TMDb downtime → fallback message on frontend
- No movies found → “No Results” message with suggestions
