# Use case 1: Watchlist reminder notification
## 1.Overview:
  **Actor**: System(Automated)
  **Goal**: Remind users of movies they haven't watched.
  **Preconditions**: 
    -Notification gateway set up.
    -Movie in watchlist for > 7 days.
  **Postconditions**:
    -Email is sent.

## 2.Main Flow:
  -Daily cron job checks watchlist entries.
  -Identifies stale entries.
  -Sends notification via gateway.

# Use case 2: Journal Reminder Notification
## 1.Overview:
  **Actor**: System
  **Goal**: Prompt user to write a journal after watching.
  **Preconditions**:
    -Movie was marked as watched
  **Postconditions**:
    -Notification sent.

## 2.Main Flow:
  -Movie marked as watched.
  -No journal entry for the movie after 2 days.
  -Sends reminder via gateway.