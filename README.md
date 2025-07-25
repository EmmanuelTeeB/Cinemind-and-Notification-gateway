# Cinemind & Notification Gateway System

Welcome to the system documentation for **Cinemind**, a movie journaling platform, and its companion microservice, the **Notification Gateway**.

This repository showcases the **system design thinking, modular architecture, and business logic documentation** behind the two key modules:


## Modules Overview

### 1. Cinemind (Movie Guide & Journaling Platform)
- Built around TMDb API for seamless movie data integration.
- Enables users to:
  - Search and browse movies
  - Maintain a personalized watchlist
  - Journal thoughts after viewing
  - Receive timely reminders via email/SMS

### 2. Notification Gateway (Scalable Messaging Service)
- Microservice responsible for:
  - Asynchronous email and SMS dispatch
  - Failover from email → SMS when needed
  - Queue-based architecture (Celery + Redis planned)
  - Logging and error tracking


##  Repository Contents

| File/Folder         | Description                                                                 |
|---------------------|-----------------------------------------------------------------------------|
| `architecture.md`   | System overview and component interaction diagrams                          |
| `flow.md`           | Step-by-step process flows (Auth, Journal, Notification, etc.)              |
| `usecase.md`        | Detailed use case documentation for Notification Gateway                    |
| `functional-requirements.md` | User stories and technical requirements for both modules            |
| `assets/`           | Visual diagrams (.png + .drawio): architecture, data flows, system logic    |

## Recommended Tools:
- **VS Code** – Markdown-friendly editing
- **draw.io** – To view or modify architecture diagrams
- **Git** – Version control and collaboration


##  Usage

- All markdown files are viewable in any Markdown renderer or IDE.  
- To edit diagrams, open `.drawio` files with the [draw.io desktop app](https://draw.io).  

---

## License

This project is published for learning and demonstration purposes only. Attribution appreciated.





