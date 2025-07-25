# Cinemind: Journal module Flow

## Purpose: 
This document details the flow for the journaling feature where authenticated users add, view, edit, and delete journal entries tied to movies.

---

##  Features Covered:
- Create journal entries  
- View journal entries  
- Edit journal entries  
- Delete journal entries

---

## Actors  
- **Authenticated User**: Can manage their journal entries.  
- **Guest User**: Cannot access journal features.

---

## Flow Breakdown

### 1 Create Journal Entry  
**Trigger:** User opens a movie page and writes a journal entry.

**Flow:**  
- Frontend sends `POST /api/journals` with:  
  ```json
  {
    "user_id": 45,
    "movie_id": 123456,
    "content": "My thoughts about this movie..."
  }
-	Backend validates user session.
-	Saves entry in journals table with timestamps

### 2.View Journal Entries
**Trigger**: User visits their journal page or a movie detail page.

**Flow**:
- Frontend sends GET /api/journals?user_id=45 or GET /api/journals?user_id=45&movie_id=123456.
- Backend queries DB and returns entries sorted by date.

### 3.Edit Journal Entry
**Trigger**: User edits an existing journal entry.

**Flow**:
- Frontend sends PUT /api/journals/{entry_id} with updated content.
- Backend verifies ownership and updates DB.

### 4.Delete Journal Entry
**Trigger**: User deletes an entry.

**Flow**:
- Frontend sends DELETE /api/journals/{entry_id}.
- Backend verifies ownership and deletes entry.

## Auth & Security:
- All journal routes require authenticated user.
- Users can only modify their own entries.
- Input sanitized to prevent injection attacks.

## Database Schema (Journals)
journals
- id (PK)
- user_id (FK)
- movie_id
- content (TEXT)
- created_at
- updated_at

## Success Criteria:
- Users can create, read, update, delete their journal entries.
- Data integrity and access control enforced.
- Responsive and consistent UI experience.
