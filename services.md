
---

# 📁 services.md

```md
# Services

## Auth Service

- Login  
- Token validation  
- Security  

---

## Account Service

- Wallets  
- Balances  
- Transactions  
- Updates PostgreSQL  

---

## Spot Trading Service

- Accepts orders  
- Validates input  
- Sends to engine  

---

## Spot Trading Engine

- Business logic  
- Balance checks  
- Order preparation  

---

## Matching Engine

- Matches orders  
- Writes to DynamoDB  
- Publishes events to RabbitMQ  

---

## Other Services (Reference)

- Margin Trading Service  
- Futures Trading Service  

These follow similar architecture but are not detailed here.