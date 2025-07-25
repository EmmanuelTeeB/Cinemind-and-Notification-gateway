# Notification Gateway – System Overview

## Purpose

The Notification Gateway is a standalone microservice designed to send messages through multiple communication channels with failover support. It ensures message delivery by prioritizing Email as the primary channel and falling back to SMS as the secondary when necessary.

## Key Components

| Component             | Description                                                                 |
|-----------------------|-----------------------------------------------------------------------------|
| **Notification API**  | Accepts notification requests from external systems.                        |
| **Email Service**     | Sends messages through email (e.g., Mailgun, SendGrid).                     |
| **SMS Service**       | Sends fallback messages via SMS (e.g., Twilio).                             |
| **Failover Controller** | Manages primary → secondary channel switch based on delivery status.       |
| **Delivery Monitor**  | Logs success/failure and tracks delivery results.                           |


## Technology Stack

| Layer              | Technology               | Role                                               |
|--------------------|--------------------------|----------------------------------------------------|
| API Layer          | Python (Flask or FastAPI)| Expose RESTful endpoints for notification intake.  |
| Email Integration  | Mailgun, SendGrid        | Primary channel for sending messages.              |
| SMS Integration    | Twilio                   | Secondary/fallback channel.                        |
| Data Storage       | PostgreSQL or MongoDB    | Log all notifications and their statuses.          |
| (Optional) Queue   | Redis, RabbitMQ          | Enable asynchronous processing in future versions. |

## Key Features

- **Failover Handling**: Automatic switch from Email to SMS if the first fails.
- **Extensibility**: Built to support more channels in the future (e.g., push, WhatsApp).
- **Observability**: All events are logged for auditing and debugging.
- **Security**: API authentication and encrypted channel support.


## Non-Functional Requirements

- **Reliability**: Ensure high message delivery success.
- **Latency**: Fast response times, especially on retries.
- **Scalability**: Design allows horizontal scaling and queue integration.
- **Maintainability**: Modular components allow easy testing and deployment.

## Example Use Case

> A payment system sends a transaction alert to a user.  
> - If the Email fails to send (e.g., bounce or timeout),  
> - The system immediately sends the same message via SMS.  
> - All outcomes are logged for reporting.

## Future Improvements

- Add asynchronous message processing (via Celery or RQ).
- Include user-specific channel preferences.
- Dashboard for viewing delivery history and system metrics.
- Retry logic with exponential backoff.

