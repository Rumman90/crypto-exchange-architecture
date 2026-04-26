# Crypto Exchange System Architecture

A scalable architecture reference for a crypto exchange platform using microservices, event-driven communication, and low-latency processing.

---

## Overview

This repository demonstrates the architecture of a crypto exchange system.

The system supports multiple trading types such as:

- Spot Trading (detailed in this repository)
- Margin Trading (high-level reference)
- Futures Trading (high-level reference)

The focus of this architecture is to clearly explain **spot trading flow and system design**, while other trading types are mentioned for completeness.

---

## Architecture Focus

This repository provides **detailed architecture for Spot Trading only**.

Margin and Futures trading follow similar patterns but are not deeply covered to keep the design simple and focused.

---

## Architecture Diagram

```mermaid
flowchart TD

    User[User / Client App]

    APIGW[API Gateway]
    ALB[AWS Load Balancer]
    ECS[AWS ECS Cluster]

    Auth[Auth Service]
    Account[Account Service]
    Cron[Cron Service]

    Spot[Spot Trading Service]
    SpotEngine[Spot Trading Engine]
    Matching[Matching Engine]

    Dynamo[(DynamoDB<br/>Orders / Matching)]
    Postgres[(PostgreSQL<br/>Users / Wallets / Balances / Transactions)]
    Redis[(Redis<br/>Cache)]
    Rabbit[(RabbitMQ<br/>Async Events)]

    User --> APIGW --> ALB --> ECS

    ECS --> Auth
    ECS --> Account
    ECS --> Cron
    ECS --> Spot

    Spot --> SpotEngine
    SpotEngine --> Matching

    Matching --> Dynamo
    Matching --> Rabbit

    Rabbit --> Account

    Auth --> Postgres
    Account --> Postgres
    Spot --> Postgres

    Redis --> Auth
    Redis --> Account
    Redis --> Spot