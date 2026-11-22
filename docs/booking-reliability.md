# Reliable Booking Architecture

## Booking Workflow

1. Client submits a reservation request.
2. ASP.NET Core validates the request.
3. Service checks the idempotency key.
4. PostgreSQL transaction validates availability.
5. Reservation is stored atomically.
6. Confirmation event is published.
7. Background worker sends notifications.

## Idempotency

Use unique idempotency keys to prevent duplicate
bookings when clients retry requests.

Persist each key with its request status and result.

## Database Reliability

Recommended practices:

- Use PostgreSQL transactions.
- Enforce database constraints.
- Handle concurrent reservation attempts.
- Use appropriate isolation and locking.

## Messaging

Use Azure Service Bus for asynchronous workflows.

Important considerations:

- Retry transient failures.
- Implement idempotent message handlers.
- Configure dead-letter queues.
- Monitor failed message delivery.

## Performance

- Cache suitable read-only data with Redis.
- Optimize frequently executed SQL queries.
- Monitor API response times.
- Measure database connection utilization.
