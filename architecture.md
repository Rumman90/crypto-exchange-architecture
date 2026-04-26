
---

## architecture.md

```md
# Architecture

## Overview

This architecture represents a scalable crypto exchange system using microservices and event-driven communication.

The system separates trading execution, account management, caching, and asynchronous processing into independent components.

---

## High-Level Flow

Client → API Gateway → Trading Service → Trading Engine → Matching Engine → DynamoDB → RabbitMQ → Account Service → PostgreSQL

---

## Main Components

### API Gateway

The API Gateway handles incoming requests from clients.

Responsibilities:

- Request routing
- Rate limiting
- Request validation
- Forwarding requests to backend services

---

### AWS Load Balancer

The load balancer distributes traffic across services running inside AWS ECS.

Responsibilities:

- Traffic distribution
- Health checks
- High availability

---

### AWS ECS

AWS ECS runs backend services as containers.

Services include:

- Auth Service
- Account Service
- Cron Service
- Spot Trading Service
- Spot Trading Engine
- Margin Trading Service
- Margin Trading Engine
- Futures Trading Service
- Futures Trading Engine
- Matching Engine

---

## Core Services

### Auth Service

Handles authentication and security.

Responsibilities:

- User login
- User registration
- Token validation
- Role-based access control
- Permission validation

Auth Service stores user-related data in PostgreSQL and may use Redis for frequently accessed role or permission data.

---

### Account Service

Handles wallets, balances, and transactions.

Responsibilities:

- Wallet management
- Available balance
- Locked balance
- Deposit records
- Withdrawal records
- Transaction records
- Balance updates after trade execution

Account Service stores business data in PostgreSQL.

---

### Cron Service

Handles scheduled background jobs.

Responsibilities:

- Cleanup jobs
- Retry jobs
- Reconciliation jobs
- Funding calculations
- Liquidation checks

---

## Trading Services

Trading services receive and validate trading requests.

Responsibilities:

- Validate trading pair
- Validate order type
- Validate price and quantity
- Forward valid orders to trading engine

---

## Trading Engines

Trading engines apply trading-specific business rules.

Examples:

### Spot Trading Engine

- Validates spot order rules
- Checks available balance
- Sends order to matching engine

### Margin Trading Engine

- Validates margin rules
- Checks margin requirements
- Sends order to matching engine

### Futures Trading Engine

- Validates leverage rules
- Checks position requirements
- Sends order to matching engine

---

## Matching Engine

The Matching Engine is responsible for matching buy and sell orders.

Responsibilities:

- Read orders from DynamoDB
- Write order updates to DynamoDB
- Match buy and sell orders
- Generate execution records
- Publish execution events to RabbitMQ

DynamoDB is the primary data store for matching-related data.

Redis is not used for matching logic.

---

## Databases

### DynamoDB

DynamoDB is used by the Matching Engine.

Use cases:

- Orders
- Matching data
- Execution records
- Order status updates

---

### PostgreSQL

PostgreSQL is used for core business data.

Use cases:

- Users
- Wallets
- Balances
- Transactions
- Deposits
- Withdrawals
- Trade history

---

### Redis

Redis is used as a cache layer.

Use cases:

- Coins
- Trading pairs
- Roles
- Permissions
- Frequently accessed configuration data

Redis improves read performance for frequently used data but does not participate in order matching.

---

## RabbitMQ

RabbitMQ is used for asynchronous communication between services.

Example events:

- OrderMatched
- TradeExecuted
- BalanceUpdateRequested
- PositionUpdated
- LiquidationTriggered
- FundingCalculated

After the Matching Engine completes execution, it publishes an event to RabbitMQ. The Account Service consumes the event and updates wallets and balances in PostgreSQL.

---

## Design Goals

- Low latency
- High throughput
- Scalable services
- Clear service boundaries
- Async processing
- Reliable account updates
- Separation between trading data and business data