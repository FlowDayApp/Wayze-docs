# Wayze 🗺️

**Intelligent daily route planner for Colombian cities.**

Wayze helps users organize their daily agenda and get smart route suggestions based on real-time weather, safety data, and AI-powered scheduling — starting with Medellín.

---

## Team

| Name | Role |
|---|---|
| Valeria | Scrum · Frontend Developer · Backend Support |
| Isabella | Backend Lead · Database · DevOps |
| Juan José | AI Lead · Python Microservice |
| Karen | Data Analytics · Automation · QA |

---

## Stack

| Layer | Technology |
|---|---|
| Frontend | React |
| Backend | ASP.NET Core 8 |
| Database | PostgreSQL |
| ORM | Entity Framework Core |
| AI Service | FastAPI (Python) + OpenAI |
| Automation | n8n |
| Maps | Google Maps API |
| Weather | OpenWeatherMap API |
| Containers | Docker |

---

## Repositories

| Repository | Description |
|---|---|
| [wayze-backend](../wayze-backend) | ASP.NET Core 8 REST API |
| [wayze-frontend](../wayze-frontend) | React web application |
| [wayze-ai-service](../wayze-ai-service) | Python FastAPI microservice |
| [wayze-n8n](../wayze-n8n) | n8n automation flows |
| [wayze-docs](../wayze-docs) | Technical documentation (this repo) |

---

## Documentation

- [System Architecture](./architecture/01-system-overview.md)
- [Backend API](./architecture/02-backend-api.md)
- [AI Service](./architecture/03-ai-service.md)
- [n8n Automation](./architecture/04-n8n-automation.md)
- [External APIs](./architecture/05-external-apis.md)
- [Database](./database/README.md)

---

## Architecture Overview

[React Frontend]
↕
[ASP.NET Core 8 — REST API] ←→ [PostgreSQL]
↕                              ↕
[FastAPI Python — AI Service]   [n8n Automation]
↕                              ↕
[OpenAI API]              [WhatsApp / Email]
↕
[Google Maps API · OpenWeatherMap · datos.gov.co]

---

## Category

Transportation · Safety · Smart City · Colombia
