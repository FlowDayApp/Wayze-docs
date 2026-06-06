# Wayze 

> **Intelligent daily route planner for Colombian cities.**
> Plan your day. Own your city.

Wayze is a smart web application that helps users organize their daily agenda and get intelligent route suggestions based on real-time weather data, public safety analytics, and AI-powered scheduling — built for Medellín, designed to scale across Colombia.

---

##  The Problem

Every day, millions of Colombians navigate their cities without knowing if it will rain during their commute, which routes are safer at certain hours, or whether they'll arrive on time. Wayze solves this by combining route planning, weather intelligence, and safety analytics into a single, seamless experience.

---

##  Key Features

| Feature | Description |
|---|---|
|  **Smart Day Planner** | Create your daily agenda with activities and locations in natural language |
|  **Intelligent Routes** | Get 2–3 route alternatives evaluated by time, safety score, and weather |
|  **AI Scheduling** | Parse your agenda using natural language — just type what you need to do |
|  **Weather Integration** | Real-time weather per route segment with rain alerts and departure suggestions |
|  **Safety Analytics** | Safety score per zone based on open crime data from datos.gov.co |
|  **Smart Reminders** | Automated notifications via WhatsApp and email — "Leave in 30 minutes" |
|  **Analytics Dashboard** | Visualize your most-used routes, risky zones, and daily patterns |

---

##  System Architecture

```
┌─────────────────────────────────────────────┐
│              React Frontend                  │
│     (Agenda · Map · Dashboard · Weather)     │
└──────────────────┬──────────────────────────┘
                   │ REST API
┌──────────────────▼──────────────────────────┐
│         ASP.NET Core 8 — Web API             │
│   (Routes · Auth · Agenda · Weather · Safety)│
└────┬─────────────┬──────────────────┬────────┘
     │             │                  │
┌────▼────┐  ┌─────▼──────┐  ┌───────▼───────┐
│PostgreSQL│  │FastAPI (Py)│  │  n8n Automation│
│(Main DB) │  │ AI Service │  │ (Reminders)   │
└──────────┘  └─────┬──────┘  └───────┬───────┘
                    │                  │
             ┌──────▼──────┐   ┌───────▼──────┐
             │  OpenAI API  │   │WhatsApp/Email│
             └─────────────┘   └──────────────┘
                    │
     ┌──────────────┼──────────────┐
     │              │              │
┌────▼────┐  ┌──────▼─────┐  ┌────▼──────────┐
│Google   │  │OpenWeather │  │ datos.gov.co   │
│Maps API │  │    API     │  │ (Crime Data)   │
└─────────┘  └────────────┘  └───────────────┘
```
---

##  Tech Stack

| Layer | Technology | Purpose |
|---|---|---|
| Frontend | React 18 | User interface — agenda, map, dashboard |
| Backend | ASP.NET Core 8 | REST API, business logic, auth |
| Database | PostgreSQL | Persistent data storage |
| ORM | Entity Framework Core | Database abstraction layer |
| AI Service | FastAPI (Python) | ML scoring + OpenAI integration |
| Automation | n8n | Smart reminders via WhatsApp and email |
| Maps | Google Maps API | Route calculation and map rendering |
| Weather | OpenWeatherMap API | Hourly weather forecasts per location |
| Crime Data | datos.gov.co | Open public safety datasets |
| Containers | Docker + Docker Compose | Full stack containerization |

---

##  Architecture Decisions

| Decision | Choice | Reason |
|---|---|---|
| Backend framework | ASP.NET Core 8 | Strong typing, EF Core ORM, native Docker support |
| Database | PostgreSQL | Open source, Docker-native, full EF Core support |
| AI integration | FastAPI microservice | Decoupled from main API, independent Python ecosystem |
| LLM provider | OpenAI GPT-4o-mini | Structured output support, cost-efficient for scheduling tasks |
| Automation | n8n | Visual workflow builder, supports WhatsApp via Twilio and email via SMTP |
| Frontend | React 18 | Best ecosystem for Google Maps and data visualization libraries |
| Containerization | Docker Compose | Single command deployment, environment parity across team |
| Safety data | datos.gov.co + Policía Nacional | Official open data, free, covers Medellín at neighborhood level |

---

##  Repositories

| Repository | Description | Tech |
|---|---|---|
| [wayze-backend](https://github.com/wayze-app/wayze-backend) | REST API, business logic, database models | ASP.NET Core 8 · EF Core · PostgreSQL |
| [wayze-frontend](https://github.com/wayze-app/wayze-frontend) | Web application, map, agenda, dashboard | React 18 |
| [wayze-ai-service](https://github.com/wayze-app/wayze-ai-service) | AI scheduling + safety scoring microservice | FastAPI · Python · OpenAI |
| [wayze-n8n](https://github.com/wayze-app/wayze-n8n) | Automation flows for reminders | n8n |
| [wayze-docs](https://github.com/wayze-app/wayze-docs) | Full technical documentation | Markdown · Diagrams |

---

##  Team

| Name | Role | Responsibilities |
|---|---|---|
| **Valeria** | Scrum Master · Frontend Lead · Backend Support | React UI, API integration, sprint management, pitch lead |
| **Isabella** | Backend Lead · DevOps | ASP.NET Core API, PostgreSQL , Docker deployment |
| **Juan José** | AI Lead · Backend Support | FastAPI microservice, OpenAI integration, safety scoring |
| **Karen** | Data Analytics · Automation · QA | Dashboard, n8n flows, test coverage, open data pipelines |

---

##  Documentation Structure

```
wayze-docs/
│
├── README.md                        ← You are here
│
├── architecture/
│   ├── 01-system-overview.md        ← Full architecture description
│   ├── 02-backend-api.md            ← ASP.NET Core endpoints and design
│   ├── 03-ai-service.md             ← FastAPI microservice and AI pipeline
│   ├── 04-n8n-automation.md         ← Reminder flows and notification logic
│   └── 05-external-apis.md          ← Google Maps, OpenWeatherMap, crime data
│
├── diagrams/
│   ├── 01-system-architecture.png   ← Full system diagram
│   ├── 02-database-schema.png       ← PostgreSQL ERD
│   ├── 03-user-flow.png             ← End-to-end user journey
│   ├── 04-ai-pipeline.png           ← AI scheduling and scoring flow
│   └── 05-deployment.png            ← Docker Compose container map
│
└── database/
    └── README.md                    ← Schema, tables, indexes, migrations
```
---

##  User Flow Example

```
1. User opens Wayze and types:
   "Go to mom's house in Laureles at 10am, then market in El Poblado at 3pm"

2. AI parses the schedule and creates:
   ├── 10:00 AM → Mom's house (Laureles)
   ├── 03:00 PM → Market (El Poblado)
   └── 06:00 PM → Home (Envigado)

3. System evaluates each route:
   ├── Route A: 20 min · Safety:  Safe · Weather:  Clear
   └── Route B: 15 min · Safety:  Caution · Weather:  Rain at 3pm

4. At 9:25 AM, user receives:
   " Leave in 35 minutes to reach mom's house on time"

5. Dashboard shows daily summary and neighborhood safety stats
```
---

##  Getting Started

> Full deployment instructions available in each repository's README.

**Quick start with Docker Compose:**

```bash
git clone https://github.com/wayze-app/wayze-backend
git clone https://github.com/wayze-app/wayze-frontend
git clone https://github.com/wayze-app/wayze-ai-service

cd wayze-backend
docker-compose up --build
```

**Required environment variables:**

```env
OPENAI_API_KEY=your_key
GOOGLE_MAPS_API_KEY=your_key
OPENWEATHER_API_KEY=your_key
POSTGRES_CONNECTION_STRING=your_connection
```

---

##  Project Category

**Technology & Innovation · Smart City · Social Inclusion**
Built for the RIWI Tech & Business Showcase — Advanced Track.

---

##  License

This project was developed as part of the RIWI Advanced Training Program.
