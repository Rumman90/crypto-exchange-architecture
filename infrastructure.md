# Infrastructure

This document explains the infrastructure components used in the crypto exchange architecture.

---

## API Gateway

Handles incoming API requests.

Responsibilities:

- Routing
- Rate limiting
- Request validation
- Forwarding traffic to services

---

## AWS Load Balancer

Distributes traffic across backend services.

Responsibilities:

- Load balancing
- Health checks
- High availability

---

## AWS ECS

Runs backend services as containers.

Example services:

- Auth Service
- Account Service
- Cron Service
- Trading Services
- Trading Engines
- Matching Engine

---

## DynamoDB

Primary data store for matching-related data.

Used for:

- Orders
- Matching data
- Execution records
- Order status updates

Used by:

- Matching Engine

---

## PostgreSQL

Primary data store for core business data.

Used for:

- Users
- Wallets
- Balances
- Transactions
- Deposits
- Withdrawals
- Trade history

Used by:

- Auth Service
- Account Service
- Trading Services

---

## Redis

Caching layer for frequently accessed data.

Used for:

- Coins
- Trading pairs
- Roles
- Permissions
- Configuration data
- Frequently accessed reference data

Redis is not used for order matching.

---

## RabbitMQ

Message broker for asynchronous communication.

Used for:

- Trade execution events
- Balance update events
- Position update events
- Retry workflows
- Async processing

---

## Infrastructure Flow

```txt
Client
  ↓
API Gateway
  ↓
AWS Load Balancer
  ↓
AWS ECS Services
  ↓
DynamoDB / PostgreSQL / Redis / RabbitMQ