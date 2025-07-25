# Notification Gateway – Flow Description

This document outlines the logical flow of how the Notification Gateway handles message delivery, with failover support between email and SMS. The goal is to ensure users reliably receive critical messages even when the primary method fails.


## 1. Overview of Flow

The gateway operates on a **priority-based delivery mechanism**:

1. Attempt to send a notification via Email (primary method).
2. If the email fails (due to timeout, delivery error, or provider issue), automatically fallback to SMS.
3. Log the outcome (success or failure) of each attempt.
4. Return a response to the originating service (e.g., backend or task queue) with the final delivery status.


## 2. High-Level Steps

1. **Trigger Event**  
   A service (e.g., backend API or task queue) sends a message payload to the Notification Gateway.

2. **Validation**  
   The gateway validates:
   - Recipient contact information
   - Message type (transactional, alert, etc.)
   - Delivery priority rules

3. **Primary Attempt (Email)**  
   - Gateway sends the message via Mailgun or SendGrid.
   - If successful, logs delivery and ends flow.
   - If failure detected, proceeds to fallback.

4. **Fallback Attempt (SMS)**  
   - Sends the message via Twilio.
   - Logs success or failure.

5. **Response + Logging**  
   - Logs full delivery trail.
   - Sends response back to caller with success/failure status and metadata.


## 3. Failure Scenarios

| Failure Point      | Handling Strategy                             |
|--------------------|-----------------------------------------------|
| Email timeout      | Trigger SMS fallback                          |
| Email service down | Trigger SMS fallback                          |
| SMS failure        | Log failure, alert admin if critical          |
| Both fail          | Persist failed state, queue for manual retry  |


## 4. Visual Flow Summary

```plaintext```
[Trigger Event]
      |
      v
[Validate Payload]
      |
      v
[Send Email] -- success --> [Log + Done]
      |
    fail
      v
[Send SMS] -- success --> [Log + Done]
      |
    fail
      v
[Log Failure + Return Error]

## 5. Dependencies

- **Mailgun / SendGrid** – Email delivery providers
- **Twilio** – SMS provider
- **Redis + Celery** *(optional)* – For async job handling (retry queues)
- **PostgreSQL / Logging System** – To store delivery status and error logs


## 6. Assumptions

- Internet connectivity is available to external providers.
- At least one delivery method (Email or SMS) is functional at a given time.
- Message content is already formatted before arriving at the gateway.
- Logging and monitoring systems are operational.

