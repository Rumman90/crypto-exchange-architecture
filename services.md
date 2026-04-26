
---

## services.md

```md
# Services

This document explains the services used in the crypto exchange architecture.

---

## Auth Service

Handles authentication, authorization, and security.

Responsibilities:

- User login
- User registration
- Token validation
- Role-based access control
- Permission validation

Data storage:

- PostgreSQL for user data
- Redis for frequently accessed roles and permissions

---

## Account Service

Handles wallets, balances, and transactions.

Responsibilities:

- Wallet management
- Available balance
- Locked balance
- Deposits
- Withdrawals
- Transaction history
- Balance updates after trade execution

Data storage:

- PostgreSQL

Consumes events from:

- RabbitMQ

---

## Cron Service

Handles scheduled and background jobs.

Responsibilities:

- Cleanup jobs
- Retry jobs
- Reconciliation jobs
- Liquidation checks
- Funding calculations

---

## Spot Trading Service

Handles spot trading APIs.

Responsibilities:

- Place spot orders
- Cancel spot orders
- Validate spot trading requests
- Forward valid orders to Spot Trading Engine

---

## Spot Trading Engine

Handles spot trading business logic.

Responsibilities:

- Validate spot order rules
- Check available balance
- Prepare order for matching
- Send order to Matching Engine

---

## Margin Trading Service

Handles margin trading APIs.

Responsibilities:

- Place margin orders
- Cancel margin orders
- Validate margin trading requests
- Forward valid orders to Margin Trading Engine

---

## Margin Trading Engine

Handles margin trading business logic.

Responsibilities:

- Validate margin order rules
- Check margin requirements
- Check risk rules
- Send order to Matching Engine

---

## Futures Trading Service

Handles futures trading APIs.

Responsibilities:

- Place futures orders
- Cancel futures orders
- Validate futures trading requests
- Forward valid orders to Futures Trading Engine

---

## Futures Trading Engine

Handles futures trading business logic.

Responsibilities:

- Validate leverage
- Validate margin
- Validate position rules
- Send order to Matching Engine

---

## Matching Engine

Handles order matching and trade execution.

Responsibilities:

- Read orders from DynamoDB
- Write order updates to DynamoDB
- Match buy and sell orders
- Generate execution records
- Publish execution events to RabbitMQ

Important:

- DynamoDB is the primary data store for matching.
- Redis is not used for matching logic.

---

## RabbitMQ Consumers

Consumers listen to events and update downstream systems.

Example consumers:

- Account Service
- Sync Service
- Notification Service
- Reporting Service

Example events:

- OrderMatched
- TradeExecuted
- BalanceUpdateRequested
- PositionUpdated