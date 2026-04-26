# Infrastructure

## API Gateway

Handles routing and incoming requests.

## AWS ECS

Runs containerized services.

## Load Balancer

Distributes traffic across services.

## Redis

- Cache
- Order book

## RabbitMQ

- Event-driven communication

## DynamoDB

- Orders
- Trades
- Transactions

---

## Flow

Client → API Gateway → ECS → Services → DB / Cache / MQ