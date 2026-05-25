# Fitness App — Spring Boot Microservices

A fitness tracking platform built as a set of Spring Boot microservices with a
React frontend. Users log workouts and activities; an AI service generates
personalised recommendations from that activity data.

## Architecture

| Service | Port | Responsibility |
|---------|------|----------------|
| **eureka** | 8761 | Service discovery / registry |
| **configserver** | 8888 | Centralised configuration for all services |
| **gateway** | — | API gateway, routing, Keycloak/OAuth2 security, user sync |
| **userservice** | — | User registration and profiles (PostgreSQL / JPA) |
| **activityservice** | — | Activity & workout logging (MongoDB) |
| **aiservice** | — | AI recommendations from activity data (Gemini + MongoDB) |
| **fitness-app-frontend** | 5173 | React 19 + Vite + MUI + Redux Toolkit UI |

Services communicate over RabbitMQ (activity → AI) and REST via the gateway.
Authentication is handled with Keycloak using OAuth2 / PKCE on the frontend.

## Tech stack

- **Backend:** Java 17, Spring Boot, Spring Cloud (Eureka, Config, Gateway),
  Spring WebFlux, Spring Data JPA & MongoDB, RabbitMQ
- **AI:** Google Gemini for recommendation generation
- **Frontend:** React 19, Vite, Material UI, Redux Toolkit, react-oauth2-code-pkce
- **Infra:** Keycloak (auth), PostgreSQL, MongoDB, RabbitMQ

## Running locally

Start the services in order:

1. `eureka` (service registry)
2. `configserver` (configuration)
3. `userservice`, `activityservice`, `aiservice`
4. `gateway`
5. Frontend: `cd fitness-app-frontend && npm install && npm run dev`

Each service is a standalone Maven module — build and run with `./mvnw spring-boot:run`.
