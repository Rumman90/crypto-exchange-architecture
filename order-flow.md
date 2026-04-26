# Order Flow (Spot Trading)

## Steps

1. User places order  
2. API Gateway receives request  
3. Spot Trading Service validates request  
4. Trading Engine processes order  
5. Matching Engine reads/writes DynamoDB  
6. Order is matched  
7. Event published to RabbitMQ  
8. Account Service consumes event  
9. PostgreSQL updated  

---

## Diagram

```mermaid
sequenceDiagram
    participant User
    participant API
    participant Spot
    participant Engine
    participant Match
    participant DB1 as DynamoDB
    participant MQ
    participant Account
    participant DB2 as PostgreSQL

    User->>API: Place Order
    API->>Spot: Forward
    Spot->>Engine: Validate
    Engine->>Match: Send Order
    Match->>DB1: Read / Write
    Match->>MQ: Publish Event
    MQ->>Account: Update Balance
    Account->>DB2: Save