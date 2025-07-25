# User case 1: Create Journal entry
## 1.Overview :
  **Actor**: Logged-in User
  **Goal**: To reflect and log their thoughts on a movie they just watched.
  **Preconditions**:
    -Movie exists in DB or TMDb.
    -User is logged in.
  **Postconditions**:
   -Journal entry saved in the Database.

## 2.Main Flow:
  -User selects a movie from watchlist or search.
  -Clicks "Write journal".
  -Enter text entry and ratings
  -System saves journal entry to Database.

# Use case 2: Edit Journal Entry
## 1.Overview:
 **Actor**: Logged-in user
 **Goal**: To revise their journal.
 **Preconditions**:
   -User is aunthenticated.
   -Journal entry exists.
 **Postconditions**:
   -Updated journal saved

## 2.Main Flow:
  -User clicks on the old journal.
  -System opens the journal
  -User updates the journal or/and ratings.
  -System replace old journal with the updated journal on the Database.

# Use case 3: Delete Journal Entry.
## 1.Overview:
  **Actor**: Logged-in user
  **Goal**: To permanately delete an entry.
  **Preconditions**:
    -User is aunthenticated.
    -Journal entry exists.
  **Postconditions**:
    -Entry deleted from Database.

## 2.Main Flow:
  -User navigates to a journal entries..
  -System loads all past entries.
  -User select(s) entry they want to delete.
  -User clicks "Delete entry(s).
  -Entry is deleted from Database.
