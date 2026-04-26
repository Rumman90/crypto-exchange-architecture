# Crypto Exchange System Architecture

A scalable architecture reference for a crypto exchange platform using microservices, event-driven communication, and low-latency processing.

---

## Overview

This repository demonstrates how to design a high-performance trading system with:

- Real-time order processing
- Low-latency execution
- Scalable microservices
- Event-driven architecture

---

## Architecture Diagram

```mermaid
flowchart TD

    User[User]

    APIGW[API Gateway]
    ALB[AWS Load Balancer]
    ECS[AWS ECS]

    Auth[Auth Service]
    Account[Account Service]
    Cron[Cron Service]

    Spot[Spot Trading Service]
    SpotEngine[Spot Engine]

    Matching[Matching Engine]

    Redis[(Redis)]
    Dynamo[(DynamoDB)]
    Rabbit[(RabbitMQ)]

    User --> APIGW --> ALB --> ECS

    ECS --> Auth
    ECS --> Account
    ECS --> Cron

    ECS --> Spot
    Spot --> SpotEngine --> Matching

    Matching --> Redis
    Matching --> Dynamo
    Matching --> Rabbit

    Rabbit --> Account