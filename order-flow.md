# Order Flow

## Step by Step

1. User places order  
2. API Gateway receives request  
3. Trading Service validates request  
4. Trading Engine processes order  
5. Matching Engine matches orders  
6. Event published to RabbitMQ  
7. Account Service updates balance  
8. Data stored in database  

---

## Diagram

```mermaid
sequenceDiagram
    participant User
    participant API
    participant Engine
    participant Match
    participant MQ
    participant Account

    User->>API: Place Order
    API->>Engine: Forward
    Engine->>Match: Process
    Match->>MQ: Publish Event
    MQ->>Account: Update Balance