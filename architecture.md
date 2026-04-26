
---

# 📁 architecture.md

```md
# Architecture

## Overview

This architecture represents a crypto exchange system designed using microservices and event-driven communication.

The system supports multiple trading types such as spot, margin, and futures.

This document focuses on **spot trading architecture in detail**, while other trading types follow similar patterns.

---

## High-Level Flow

Client → API Gateway → Trading Service → Trading Engine → Matching Engine → DynamoDB → RabbitMQ → Account Service → PostgreSQL

---

## Core Components

### API Gateway

- Routing
- Rate limiting
- Validation

---

### Trading Services

The system supports multiple trading types:

- Spot Trading (detailed)
- Margin Trading (reference)
- Futures Trading (reference)

Each trading type typically has its own service and engine.

---

## Spot Trading Architecture (Detailed)

### Spot Trading Service

- Accepts user orders  
- Validates request  
- Sends to engine  

---

### Spot Trading Engine

- Applies business rules  
- Validates balance  
- Sends order to matching engine  

---

### Matching Engine

- Reads/writes orders in DynamoDB  
- Matches buy/sell orders  
- Generates execution records  
- Publishes events to RabbitMQ  

---

## Databases

### DynamoDB

Primary store for trading:

- Orders  
- Matching  
- Execution  

---

### PostgreSQL

Business data:

- Users  
- Wallets  
- Balances  
- Transactions  

---

### Redis

Cache layer:

- Coins  
- Trading pairs  
- Roles  
- Config data  

---

## Event Flow

Matching Engine → RabbitMQ → Account Service → PostgreSQL

---

## Design Goals

- Low latency  
- High throughput  
- Scalable services  
- Clear separation of concerns  