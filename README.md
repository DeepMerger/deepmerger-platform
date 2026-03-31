<div align="center">

<img src="https://raw.githubusercontent.com/deepmerger/deepmerger-brand/main/assets/logo-dark.svg" width="64" height="64" alt="DeepMerger" />

# deepmerger-platform

**The Common Operating Picture. One screen. Zero noise.**

[![Status](https://img.shields.io/badge/status-active%20development-00C9A7?style=flat-square)](https://github.com/deepmerger/deepmerger-platform)
[![TRL](https://img.shields.io/badge/TRL-4%20→%206-0D1B2A?style=flat-square)](https://github.com/deepmerger/deepmerger-platform)
[![iDEX](https://img.shields.io/badge/iDEX-Open%20Challenge%202026-orange?style=flat-square)](https://idex.gov.in)
[![License](https://img.shields.io/badge/license-MIT-blue?style=flat-square)](LICENSE)
[![Made in India](https://img.shields.io/badge/Made%20in-India-FF9933?style=flat-square)](https://www.startupindia.gov.in)

*India's sovereign battlefield intelligence platform — built for the Indian Army's infantry brigade.*

</div>

---

## What is DeepMerger

An infantry brigade commander — responsible for 3,000–5,000 soldiers across a 20–50 km front — currently makes critical decisions from fragmented, disconnected intelligence. Weather in one system. Terrain on paper maps. OSINT by phone call. Unit positions updated every 4–6 hours.

**Decision latency: 45–90 minutes. In modern warfare, that is too slow.**

DeepMerger solves this by fusing all available intelligence streams into a single, real-time **Common Operating Picture** — with an AI engine generating situation briefs every 30 minutes, entirely offline, on a single server at brigade HQ.

```
Weather + Terrain + Satellite + OSINT + Units + Logistics
                          ↓
              DeepMerger Fusion Engine
                          ↓
         One screen. One truth. One commander.
```

---

## Architecture

```
┌─────────────────────────────────────────────────────┐
│                   deepmerger-platform                │
│                                                     │
│  ┌──────────────┐    ┌──────────────────────────┐  │
│  │   React.js   │    │     Leaflet.js Tactical   │  │
│  │  Dashboard   │◄───│     Map + Overlays         │  │
│  └──────┬───────┘    └──────────────────────────┘  │
│         │                                           │
│  ┌──────▼───────────────────────────────────────┐  │
│  │              FastAPI Backend                  │  │
│  │   /api/weather  /api/threats  /api/units      │  │
│  │   /api/brief    /api/alerts   /api/satellite  │  │
│  └──────┬───────────────────────────────────────┘  │
│         │                                           │
│  ┌──────▼──────┐  ┌──────────┐  ┌──────────────┐  │
│  │  PostgreSQL  │  │  Redis   │  │   Ollama AI  │  │
│  │  + PostGIS  │  │  Cache   │  │   (LLaMA 3)  │  │
│  └─────────────┘  └──────────┘  └──────────────┘  │
└─────────────────────────────────────────────────────┘
```

Full architecture: [`deepmerger-fusion`](https://github.com/deepmerger/deepmerger-fusion) · AI engine: [`deepmerger-ai`](https://github.com/deepmerger/deepmerger-ai) · Deployment: [`deepmerger-deploy`](https://github.com/deepmerger/deepmerger-deploy)

---

## Features

| Module | Status | Description |
|--------|--------|-------------|
| Tactical Map | ✅ Live | Leaflet.js COP — units, contacts, range rings, sectors |
| Weather Intelligence | ✅ Live | Real-time AOR weather — visibility, wind, ops window |
| OSINT Threat Feed | ✅ Live | GDELT conflict signals — severity classified |
| AI Situation Brief | ✅ Live | LLaMA 3 local — offline, 30-min cadence |
| Alert Engine | ✅ Live | Compound signal detection — no false positives |
| Unit Tracking | ✅ Live | Friendly/hostile/unknown with status |
| Satellite Overlay | 🔨 In progress | Sentinel-2 10m imagery |
| Offline Mode | 🔨 In progress | 72h zero-internet operation |
| Role-Based Access | 📋 Planned | Commander / Ops / Intel / Logistics views |

---

## Quick Start

```bash
# Clone
git clone https://github.com/deepmerger/deepmerger-platform
cd deepmerger-platform

# One command deploy (requires Docker)
cp .env.example .env        # Add your API keys
docker compose up -d        # Full stack in < 10 minutes

# Open dashboard
open http://localhost:3000
```

### Environment Variables

```env
OPENWEATHERMAP_API_KEY=your_key_here
MAPBOX_TOKEN=your_token_here          # Optional — OSM works without
ANTHROPIC_API_KEY=your_key_here       # Optional — Ollama runs locally
```

---

## Data Sources

| Source | Data | Frequency | Cost |
|--------|------|-----------|------|
| OpenWeatherMap | Temp, wind, visibility, pressure | 15 min | Free |
| Open-Meteo | High-altitude weather, fog probability | 15 min | Free |
| GDELT Project | Conflict event signals, OSINT | 15 min | Free |
| ESA Sentinel-2 | 10m satellite imagery | 4–6 hr | Free |
| NASA SRTM | 30m elevation data | Static | Free |
| OpenStreetMap | Roads, terrain, infrastructure | Daily | Free |
| OpenSky Network | Aircraft tracking (ADS-B) | Real-time | Free |

**Total API cost to run this platform: ₹0/month.**

---

## Tech Stack

```
Frontend    React.js 18 + Leaflet.js + Tailwind CSS
Backend     Python 3.12 + FastAPI + SQLAlchemy
Database    PostgreSQL 16 + PostGIS 3.4
Cache       Redis 7
AI Engine   Ollama + LLaMA 3 7B (local inference)
Deploy      Docker Compose
OS          Ubuntu 22.04 LTS (Maya OS compatible)
```

---

## Why This Exists

The Indian Army Chief declared 2026 the **Year of Networking and Data Centricity** and acknowledged the force is *"not prepared"* in this domain. Project Samvahak (CIDSS) has faced years of delays and integration failures. Project Sanjay cost ₹2,402 crore and ran years behind schedule.

DeepMerger is the lean, open-source, one-command alternative — built by Indian engineers, for Indian soldiers, owned by India.

Palantir Gotham is geopolitically locked out of India. This is what fills that gap.

---

## Roadmap

```
Month 1–2   Live API integration, real data, interactive map
Month 3     Ollama AI briefs, compound alert engine  
Month 4     Docker air-gap mode, offline satellite cache
Month 5     Brigade HQ pilot deployment, operator training
Month 6     Security audit, validation report, MoD submission
Year 2      Division scale, DRDO partnership, Navy variant
Year 3      Programme of Record, tri-service expansion
```

---

## Contributing

DeepMerger is an active, early-stage project. If you have experience in defence software, geospatial engineering, or AI inference — open an issue or reach out.

Security vulnerabilities: `security@deepmerger.in` (do not open public issues)

---

## License

MIT — see [LICENSE](LICENSE)

*Built under iDEX Open Challenge 2026 · Dipanshu Dixit · UDYAM-HR-02-0050012*

---

<div align="center">
<sub>Three streams. One truth. · deepmerger.in</sub>
</div>