# Order Flow

This document explains how an order moves through the crypto exchange system.

---

## Main Order Flow

1. User places an order from web or mobile app.
2. API Gateway receives the request.
3. Trading Service validates the request.
4. Trading Engine applies business rules.
5. Matching Engine processes the order.
6. Matching Engine reads/writes orders in DynamoDB.
7. Order is matched.
8. Matching Engine publishes event to RabbitMQ.
9. Account Service consumes the event.
10. Account Service updates wallets, balances, and transactions in PostgreSQL.

---

## Flow Diagram

```mermaid
sequenceDiagram
    participant User
    participant API as API Gateway
    participant Trading as Trading Service
    participant Engine as Trading Engine
    participant Match as Matching Engine
    participant Dynamo as DynamoDB
    participant MQ as RabbitMQ
    participant Account as Account Service
    participant PG as PostgreSQL

    User->>API: Place Order
    API->>Trading: Route Request
    Trading->>Engine: Validate Request
    Engine->>Match: Send Order
    Match->>Dynamo: Read / Write Order
    Match->>Match: Match Order
    Match->>MQ: Publish Execution Event
    MQ->>Account: Consume Event
    Account->>PG: Update Wallet / Balance / Transaction