
---

# 📁 STEP 3 — architecture.md

```md
# Architecture

## Overview

This architecture represents a scalable crypto exchange system designed using microservices and event-driven communication.

## Flow

Client → API Gateway → Services → Engine → Matching → Events → Database

---

## Components

### API Gateway

- Request routing
- Rate limiting
- Request validation

### Services

- Auth Service
- Account Service
- Trading Service

### Trading Engine

- Validates orders
- Locks balance
- Sends to matching engine

### Matching Engine

- Matches buy/sell orders
- Generates trades

### Redis

- Order book
- Cache
- Fast access

### RabbitMQ

- Async processing
- Event communication

### DynamoDB

- Orders
- Trades
- Transactions

---

## Design Goals

- Low latency  
- High throughput  
- Scalable services  
- Async processing  