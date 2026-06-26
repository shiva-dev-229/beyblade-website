# Beyblade Platform — Full-Stack Web App

> A full-stack Beyblade encyclopedia and **battle simulator**. Browse a database of Beyblades and their stats, pit any two against each other and have the outcome simulated from their attributes, convert names between the Hasbro and Takara Tomy naming systems, and more — served by a custom REST API over a MongoDB database, with a responsive React front end.

---

## Overview

This project is a complete three-tier application built around competitive Beyblade Burst:

```
beyblade-website/                  ← repo root (monorepo)
├── beyblade-api/                  ← Express + MongoDB REST API (the backend)
├── beyblade-database/             ← CSV datasets + a Python ETL script
└── beyblade-website/              ← React single-page app (the frontend)
```

The frontend talks to the API over HTTP (via axios); the API reads and writes a MongoDB database; the database is seeded from CSV data through a small Python conversion script.

---

## Features

- **Beyblade database** — every Beyblade stored with its series and six battle stats: attack, burst, defense, weight, agility, and stamina.
- **Battle simulator** — submit two Beyblades and the API returns a predicted winner, computed from their stats (see [How the battle engine works](#how-the-battle-engine-works)).
- **Name converter** — translate Beyblade names between the **Hasbro** and **Takara Tomy** naming systems, which differ between regions.
- **Search** — look up Beyblades in the database.
- **Music** — a collection of Beyblade-related songs.
- **Users** — user account support.
- **Responsive front end** — the React app renders distinct desktop and mobile layouts, with sections covering how to use the site, curated shopping links (Hasbro, Amazon, eBay, Walmart, Target), recommended YouTube creators, and an "About the Maker" page.

---

## How the battle engine works

The battle logic (`beyblade-api/routes/Battle/Check.js`) decides a winner in two stages:

1. **Decisive matchup.** It first compares each Beyblade's combined `attack + weight + agility`. If one is clearly higher, that Beyblade wins outright.
2. **Drawn-out battle.** If the two are evenly matched, the engine simulates the fight turn by turn. Each turn is chosen at random; the attacker deals damage equal to the difference in `defense + stamina + agility` between the two blades, subtracted from the defender's `burst` value. The first Beyblade whose burst drops below zero loses. Identical Beyblades return a tie ("the match will depend on the player").

It's a compact, stat-driven model that turns six numbers into a plausible match outcome.

---

## Tech stack

**Backend (`beyblade-api/`)**
- Node.js + **Express** — REST API and routing
- **MongoDB** + **Mongoose** — database and schema modeling
- **morgan** — HTTP request logging
- **dotenv** — environment configuration

**Frontend (`beyblade-website/`)**
- **React** + **react-router-dom** — SPA with client-side routing
- **axios** — API requests
- **Firebase** — app services
- **SCSS** (Sass) and **react-icons** — styling and icons

**Data (`beyblade-database/`)**
- CSV datasets + a **Python** script for converting them into database seed statements

---

## Getting started

### Prerequisites
- [Node.js](https://nodejs.org/)
- A running [MongoDB](https://www.mongodb.com/) instance (local or hosted, e.g. Atlas)
- Python 3 (only needed to regenerate database seed data)

### 1. Start the API

```bash
cd beyblade-api
npm install
```

Create a `.env` file in `beyblade-api/` with:

```
DATABASE_URL=mongodb://localhost:27017/beyblade   # your MongoDB connection string
HOST=localhost
PORT=5000
```

Then run:

```bash
npm start          # production
npm run dev-start  # development, with nodemon auto-reload
```

The API will connect to MongoDB and listen on the host/port you set.

### 2. Seed the database

The Beyblade data lives in `beyblade-database/`. The included Python script reads `BEYBLADE.csv` and prints MongoDB insert statements:

```bash
cd beyblade-database
python3 convert.py
```

Run the generated `db.beyblades.insert({...})` statements against your MongoDB database to populate it.

### 3. Start the front end

```bash
cd beyblade-website          # the inner frontend folder
npm install
npm start                    # runs at http://localhost:3000
```

The front end expects the API to be reachable at the host/port configured above (CORS on the API is set to allow the front end's origin on port 3000).

---

## API routes

| Route | Purpose |
| --- | --- |
| `GET /beyblades` | List / retrieve Beyblades |
| `GET /battle?bey1=<id>&bey2=<id>` | Simulate a battle between two Beyblades |
| `GET /search` | Search the Beyblade database |
| `/names` | Convert names between Hasbro and Takara Tomy |
| `/music` | Beyblade songs |
| `/users` | User accounts |

---

## Notes

This is a personal project built out of an interest in competitive Beyblade Burst. It brings together a REST API, a database with a real data pipeline, a battle-simulation algorithm, and a responsive React client — the data and stats are drawn from the Beyblade community and official sources, used here for a fan project.
