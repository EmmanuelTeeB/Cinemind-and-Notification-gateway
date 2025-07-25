# Use Case – Notification Gateway Failover Handling

## Use Case: High-Reliability Notification Delivery

### Objective
Ensure reliable delivery of user notifications by attempting Email first, and automatically falling back to SMS if Email fails.

## Actors

| Actor                | Role                                                                               |
|----------------------|------------------------------------------------------------------------------------|
| External System      | Any client system that triggers a notification (e.g., billing service, movie app). |
| Notification Gateway | The microservice that manages delivery logic and failover.                         |
| User                 | The intended recipient of the notification.                                        |


## Pre-Conditions

- The Notification Gateway is up and reachable.
- User contact information includes both Email and Phone Number.
- External system is authorized to use the gateway (e.g., via API key).

---

## Main Flow (Email First)

1. External System sends a POST request to `/api/notify` with:
   - Message content
   - Recipient details (email and phone)
   - Notification type (e.g., alert, info, error)

2. Notification Gateway:
   - Logs the incoming request.
   - Attempts to deliver the message using the Email Service (Mailgun, SendGrid).
   - Waits for delivery confirmation or failure response.

3. If Email is successful:
   - Logs success.
   - Responds to the external system with `200 OK`.


## Alternate Flow (Email Fails → SMS Fallback)

1. If the Email Service responds with failure (e.g., timeout, bounce):
   - Notification Gateway logs the failure.
   - Immediately attempts to send the same message via the SMS Service (e.g., Twilio).

2. If SMS is successful:
   - Logs fallback success.
   - Responds to external system with `207 Multi-Status` (partial success), or custom status indicating fallback used.

3. If both Email and SMS fail:
   - Logs total failure.
   - Responds with `500 Internal Server Error` or `422 Unprocessable Entity` depending on failure type.

---

##  Post-Conditions

- All delivery attempts and outcomes are logged (Email success, SMS fallback, or failure).
- Optional: delivery status stored in a database for retry or reporting.

##  Example Request Payload

```json```
{
  "to": {
    "email": "user@example.com",
    "phone": "+1234567890"
  },
  "message": "Your OTP is 384920",
  "type": "transaction_alert"
}

## Success Criteria
- At least one channel (Email or SMS) successfully delivers the message.
- External system receives timely feedback.
- System maintains delivery traceability via logs or database entries.

## Future Enhancements
- Retry logic with backoff.
- User-defined channel priority (e.g., SMS first).
- Delivery confirmation callbacks (webhooks).
- Multilingual message templates.