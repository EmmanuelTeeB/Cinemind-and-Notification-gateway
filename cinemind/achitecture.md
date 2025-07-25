# 🎬 Cinemind MVP – System Architecture

## Overview

Cinemind MVP is a lightweight movie guide and tracker that helps users search for films, manage a personal watchlist, and reflect on what they’ve watched through journaling. It integrates with The Movie Database (TMDb) API for dynamic movie data and sends email notifications to keep users engaged.

This architecture document outlines the key components of the MVP, how they interact, and the technologies chosen to deliver a functional, secure, and extensible foundation.

---

## Purpose
The goal of the MVP is to validate Cinemind’s core value:
- Helping users discover movies, track what they want to watch, and record their thoughts in one place.
- Deliver a working version with essential features and leave room for scalable enhancements in future releases.

---

## User Roles

 **End Users**:  
- Can search movies, create a watchlist, write journal entries, and receive email reminders.

## Key Components (MVP Scope)

| Component                   | Description                                                                           |
|-----------------------------|---------------------------------------------------------------------------------------|
| **Frontend UI**             | Web interface (React planned) for movie search, watchlist management, and journaling. |
| **Backend API (Flask)**     | Handles user authentication, movie-related operations, journaling, and notifications. |
| **Database (PostgreSQL)**   | Stores users, watchlists, journal entries, and user preferences.                      |
| **TMDb API**                | External API used to fetch real-time movie metadata.                                  |
| **Notification Handler**    | Sends notification emails to users (e.g., via Mailgun).                               |


## omponent Interactions

1. **User Interaction**  
   The user interacts with the Frontend UI to search for movies or manage their profile.

2. **Backend Processing**  
   The Flask API receives the user request, verifies their authentication using JWT tokens, and either fetches data from the database or queries the TMDb API.

3. **Watchlist & Journaling**  
   Actions such as adding a movie or submitting a journal entry are persisted to PostgreSQL and optionally trigger an email notification.

4. **Notification Handling**  
   For the MVP, notifications are sent synchronously via Mailgun when a user adds a movie or journal entry. Asynchronous background tasks will be introduced later.

## System Boundaries

| Internal Components        | External Dependencies            |
|----------------------------|----------------------------------|
| Frontend UI (React)        | TMDb API (Movie data provider)   |
| Flask API                  | Mailgun (Email service)          |
| PostgreSQL Database        |                                  |

---

## Technology Stack (MVP)

| Layer              | Technology                | Purpose                                      |
|--------------------|---------------------------|----------------------------------------------|
| Backend API        | Python (Flask)            | Core application logic and routing           |
| Database           | PostgreSQL                |Persistent storage for user and app data      |
| External API       | TMDb API                  |Access to rich, real-time movie metadata      |
| Notification       | Mailgun                   |Email delivery service                        |
| Authentication     | JWT                       | Stateless, secure session handling           |
| Frontend (Planned) | React (or HTML prototype) | User interface for all interactions          |


## Non-Functional Considerations

- **Scalability (Planned):**  
  Backend is designed to support transition to Celery and Redis for background task processing in future phases.

- **Security (Basic):**  
  JWT tokens secure user sessions. All communication is expected to occur over HTTPS.

- **Maintainability:**  
  Clear separation of frontend, backend, and data layers allows future iteration and testing.

- **Performance (Acceptable):**  
  TMDb API is queried on demand; caching and async improvements are deferred for now. Emails are sent directly without queuing.


## Architecture Diagrams

The following diagrams provide visual insight into the MVP system architecture:

- **Component Diagram** – Shows core services, integrations, and modules at a high level.
- **Data Flow Diagram (DFD)** – Depicts the flow of data between modules and external systems.

These diagrams are stored in the [`docs/assets/`](./docs/assets/) folder and embedded below for reference.

![Component Diagram](./docs/assets/component-diagram.png)
![Data Flow Diagram](./docs/assets/dataflow-diagram.png)


## Future Enhancements (Post-MVP)

- Introduce Redis + Celery to handle background tasks like notifications and journaling analysis.
- Add SMS and Push Notifications through Twilio or Firebase.
- Include AI-powered journaling (e.g., tag suggestions, emotion detection).
- Launch Analytics Dashboard for tracking movie trends and user engagement.
- Expand Frontend to mobile (React Native or PWA).
- Add user notification preferences and reminder customization.


## Summary

Cinemind’s MVP delivers the foundation for a personalized, movie-centric journaling experience. By focusing on essential features, search, watchlist, journaling, and notifications, the architecture stays lightweight, testable, and ready to grow into a more advanced platform over time.
