# UrbanPulse: Your Event & Logistics Planner
## SDE Final Project Report 2025/26

<p align="center"> <img src="https://img.shields.io/badge/Python-3.11-blue?logo=python&logoColor=white" /> <img src="https://img.shields.io/badge/Flask-API-black?logo=flask&logoColor=white" /> <img src="https://img.shields.io/badge/PostgreSQL-Database-blue?logo=postgresql&logoColor=white" /> <img src="https://img.shields.io/badge/Docker-Containerization-blue?logo=docker&logoColor=white" /> <img src="https://img.shields.io/badge/Docker%20Compose-Orchestration-blue?logo=docker&logoColor=white" /> <img src="https://img.shields.io/badge/REST-Architecture-green" /> <img src="https://img.shields.io/badge/SOA-4--Layer-orange" /> <img src="https://img.shields.io/badge/Telegram-Bot-blue?logo=telegram&logoColor=white" /> </p>
<p align="center">
  <img src="https://img.shields.io/badge/Ticketmaster-Events-purple" />
  <img src="https://img.shields.io/badge/OpenWeatherMap-Weather-orange" />
  <img src="https://img.shields.io/badge/OpenRouteService-Mapping-green" />
</p>


**Team Members:** Lewis Ndambiri, Mehrab Fajar  
**Track:** 2 Process-Centric Services   
**User Interface:** Telegram Bot


---

## Executive Summary

UrbanPulse is a service-oriented architecture (SOA) application that streamlines event discovery and logistics planning through a conversational Telegram bot interface. The system integrates multiple external APIs (Ticketmaster, OpenWeatherMap, OpenRouteService) to provide intelligent event recommendations with weather-aware transport optimization.

---

## System Architecture

### 4-Layer SOA Design

```
┌─────────────────────────────────────────────────────────────────┐
│                    USER INTERFACE LAYER                         │
│  ┌───────────────────────────────────────────────────────────┐  │
│  │              Telegram Bot (Python)                        │  │
│  │  Commands: /tonight, /setup, /profile, /history           │  │
│  └───────────────────────────────────────────────────────────┘  │
└────────────────────────┬────────────────────────────────────────┘
                         │ REST API (JSON)
┌────────────────────────┴────────────────────────────────────────┐
│              LAYER 1: PROCESS-CENTRIC SERVICES                  │
│  ┌──────────────────────────┐  ┌──────────────────────────────┐ │
│  │  Event Discovery         │  │  Logistics & Commit          │ │
│  │  Orchestrator            │  │  Orchestrator                │ │
│  │  Port: 5008              │  │  Port: 5009                  │ │
│  │  Workflow: "What's       │  │  Workflow: "I want to go     │ │
│  │  happening tonight?"     │  │  to [Event ID]"              │ │
│  └──────────────────────────┘  └──────────────────────────────┘ │
└────────┬────────────────────────────────────┬───────────────────┘
         │ REST API Calls                     │
┌────────┴────────────────────────────────────┴───────────────────┐
│              LAYER 2: BUSINESS LOGIC SERVICES                   │
│  ┌──────────────────────────┐  ┌──────────────────────────────┐ │
│  │  Preference Matcher      │  │  Transport Optimizer         │ │
│  │  Port: 5006              │  │  Port: 5007                  │ │
│  │  • Score events (0-100)  │  │  • Calculate viability       │ │
│  │  • Rank by preferences   │  │  • Weather-aware routing     │ │
│  │  • Weather filtering     │  │  • Mode recommendation       │ │
│  └──────────────────────────┘  └──────────────────────────────┘ │
└────────┬────────────────────────────────────┬───────────────────┘
         │                                    │
┌────────┴────────────────────────────────────┴───────────────────┐
│              LAYER 3: ADAPTER SERVICES                          │
│  ┌─────────────┐  ┌──────────────┐  ┌────────────────────────┐  │
│  │   Events    │  │   Weather    │  │      Map Adapter       │  │
│  │   Adapter   │  │   Adapter    │  │   (OpenRouteService)   │  │
│  │ Port: 5003  │  │  Port: 5004  │  │     Port: 5005         │  │
│  │ Ticketmaster│  │ OpenWeather  │  │  • Distance calc       │  │
│  │    API      │  │     API      │  │  • Transit options     │  │
│  └─────────────┘  └──────────────┘  └────────────────────────┘  │
└────────┬──────────────────────────────────────────────────┬─────┘
         │                                                  │
┌────────┴──────────────────────────────────────────────────┴─────┐
│              LAYER 4: DATA SERVICES                             │
│  ┌──────────────────────────┐  ┌──────────────────────────────┐ │
│  │  User Profile Service    │  │  Itinerary Service           │ │
│  │  Port: 5001              │  │  Port: 5002                  │ │
│  │  • Music preferences     │  │  • Event commitments         │ │
│  │  • Home location         │  │  • Logistics history         │ │
│  │  • User metadata         │  │  • Transport records         │ │
│  └──────────────────────────┘  └──────────────────────────────┘ │
└────────┬──────────────────────────────────────────────────┬─────┘
         │                                                  │
         └──────────────┬───────────────────────────────────┘
                        │
              ┌─────────▼─────────┐
              │   PostgreSQL      │
              │    Database       │
              │   Port: 5432      │
              └───────────────────┘
```

---

## Workflow Examples

### Workflow 1: Event Discovery ("What's happening tonight?")

```
User → Telegram Bot → Event Discovery Orchestrator
                            │
        ┌───────────────────┼───────────────────┐
        │                   │                   │
        ▼                   ▼                   ▼
User Profile         Events Adapter      Weather Adapter
  Service            (Ticketmaster)      (OpenWeather)
        │                   │                   │
        └───────────────────┼───────────────────┘
                            │
                            ▼
                  Preference Matcher
                  (Business Logic)
                            │
                            ▼
                  Filter by Weather
                            │
                            ▼
              Ranked Events → User
```

**Steps:**
1. Fetch user music preferences (Jazz, Rock, etc.)
2. Query Ticketmaster API for events in city
3. Score events based on preference match (0-100)
4. Get weather forecast for event date
5. Warn about outdoor events in bad weather
6. Return top 5 ranked events

### Workflow 2: Event Commitment ("I want to go to Event #3")

```
User → Telegram Bot → Logistics & Commit Orchestrator
                            │
        ┌───────────────────┼───────────────────┐
        │                   │                   │
        ▼                   ▼                   ▼
User Profile         Events Adapter      Weather Adapter
  (Home Loc)         (Event Details)      (Forecast)
        │                   │                   │
        └───────────────────┼───────────────────┘
                            │
                            ▼
                      Map Adapter
                    (Transit Options)
                            │
                            ▼
                  Transport Optimizer
                   (Business Logic)
                            │
                            ▼
                   Itinerary Service
                      (Save Plan)
                            │
                            ▼
              Complete Plan → User
```

**Steps:**
1. Get user's home location
2. Fetch event venue coordinates
3. Calculate distance and transit options (car, bike, walk)
4. Get weather forecast
5. Apply optimization logic: *If Rain > 50% AND Distance < 5km → Suggest Car*
6. Save itinerary to database
7. Return complete logistics plan

---

## Technical Implementation

### Technology Stack

| Component | Technology | Purpose |
|-----------|-----------|---------|
| **Framework** | Flask 3.0.0 | RESTful web services |
| **Database** | PostgreSQL 15 | Persistent data storage |
| **Containerization** | Docker & Docker Compose | Service deployment |
| **Bot Framework** | python-telegram-bot 20.7 | User interface |
| **HTTP Client** | Requests 2.31.0 | Inter-service communication |
| **ORM** | SQLAlchemy 3.1.1 | Database abstraction |

### External APIs Integrated

1. **Ticketmaster API** - Event discovery and details
2. **OpenWeatherMap API** - Current weather and 5-day forecasts
3. **OpenRouteService API** - Routing and distance calculations

### Service Communication

- **Protocol:** REST APIs with JSON payloads
- **Architecture:** Synchronous request-response
- **Error Handling:** HTTP status codes with descriptive messages
- **Timeouts:** 5-30 seconds depending on complexity

---

## Key Features

### Intelligent Preference Matching
- **Genre-based scoring:** Exact match (+50 pts), Partial match (+20 pts)
- **Automatic ranking:** Events sorted by compatibility score
- **Learning capability:** Stores preferences for future recommendations

### Weather-Aware Planning
- **Rain probability tracking:** Forecasts analyzed for event times
- **Outdoor event warnings:** Alerts for high-risk conditions
- **Climate-based suggestions:** Indoor alternatives when weather is poor

### Smart Transport Optimization
- **Multi-modal routing:** Car, bicycle, walking options calculated
- **Viability scoring:** Distance + weather + time efficiency
- **Heuristic rules:** e.g., *"Rain > 50% + Distance < 5km = Drive"*

---

## SOA Compliance

✅ **Strict 4-Layer Architecture** - Clear separation of concerns  
✅ **2 Process Orchestrators** - Distinct workflow management (2-student requirement)  
✅ **REST Communication** - Standardized JSON interfaces  
✅ **Service Independence** - Each service can run standalone  
✅ **Containerization** - Docker deployment for all services  
✅ **External Integration** - Real-world APIs (Ticketmaster, OpenWeather, OpenRouteService)  
✅ **Data Persistence** - PostgreSQL with proper schema design

---

## Deployment

### Docker Compose Configuration
- **11 Containers:** 1 database + 9 services + 1 bot
- **Networking:** Internal bridge network for service communication
- **Environment Variables:** API keys and service URLs externalized
- **Health Checks:** `/health` endpoint for all services
- **Port Mapping:** Services exposed on ports 5001-5009

### Running the System
```bash
# Build and start all services
docker-compose up --build

# Test individual service
curl http://localhost:5008/api/v1/quick-discover \
  -H "Content-Type: application/json" \
  -d '{"city": "New York", "preferences": ["Jazz"]}'
```

---

## Conclusion

UrbanPulse successfully demonstrates a production-grade SOA implementation with clear layer separation, intelligent business logic, and seamless external API integration. The system provides real value by solving the fragmented event planning experience through a unified conversational interface.

**Future Enhancements:**
- Redis caching for improved performance
- Machine learning for better recommendations
- Multi-city event aggregation
- Real-time event notifications
- Collaborative filtering based on similar users

---

**GitHub Repository:**  https://github.com/lewisndambiri/lewisndambiri.github.io/new/main/projects  
**Live Demo:** Available via Telegram @EventPlanner  
**Documentation:** Complete API documentation in `/docs`
