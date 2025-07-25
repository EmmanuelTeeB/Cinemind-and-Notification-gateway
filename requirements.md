# Functional Requirements – Cinemind & Notification Gateway

## Cinemind

### User Stories

- **Search Movies**: As a user, I want to search for movies using keywords.
- **Watchlist Management**: As a user, I want to add and remove movies from my watchlist.
- **Journal Entries**: As a user, I want to journal my thoughts after watching a movie.
- **Notifications**: As a user, I want to receive email or SMS reminders for movies in my watchlist.

### Functional Requirements

-  User authentication via JWT.
-  Integration with TMDb API for movie data.
-  CRUD operations on journal entries and watchlist.
-  Trigger notifications on journal creation or idle watchlist items.

---

## Notification Gateway

### User Stories

- **Failover Communication**: As a system, I want to send an email first, and if it fails, fallback to SMS.
- **Queued Dispatching**: As a system, I want to queue notification jobs asynchronously.
- **Scalable Handling**: As an admin, I want the service to handle increasing volumes of notifications without failure.

### Functional Requirements

-  Email sending via Mailgun or SendGrid.
-  SMS fallback via Twilio.
-  Queue support with Redis and Celery (Planned).
-  Logging and error handling for failed jobs.

##  Non-Functional Requirements

-  **Performance**: API endpoints should respond within 500ms under normal load.
-  **Security**: All endpoints protected via token-based authentication. Sensitive data must be encrypted in transit.
-  **Availability**: Services should gracefully degrade if TMDb or external APIs fail.
-  **Responsiveness**: Frontend (if applicable) must be mobile-friendly.
-  **Extensibility**: Both Cinemind and Notification Gateway are designed to support future feature modules (e.g. social sharing, analytics).
-  **Scalability**: Notification Gateway must support async processing of 1000+ concurrent jobs in future versions.

---

##  Assumptions & Constraints

- TMDb API availability is essential for core features.
- Notification Gateway uses free-tier APIs (Mailgun, Twilio) with usage limits.
- Redis and Celery are planned but may be replaced with alternatives based on deployment feasibility.