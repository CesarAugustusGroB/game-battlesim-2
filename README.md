# BattleSim.io

A high-performance 2D battle simulator inspired by .io games. Red and Blue armies fight in real time using custom physics, flocking/squad behavior, and a spatial-partitioning grid that supports massive unit counts. Spawn soldiers, tanks, archers, cavalry, and HQs; edit the terrain with hills and capture points; issue team orders; and consult a Gemini-powered strategic advisor with deep-reasoning analysis.

## Features

- Real-time 2D simulation kept in a ref to avoid per-tick React re-renders, with lower-frequency UI stat updates (`App.tsx`).
- Spatial-partitioning grid for fast neighbor queries on large unit counts (`services/simulation.ts`).
- Five unit types — Soldier, Tank, Archer, Cavalry, and HQ — each with configurable mass, defense, speed, acceleration, health, damage, range, and cooldown (`types.ts`, `constants.ts`).
- Squad system with per-squad centroids used for movement and "attack nearest" targeting.
- Team orders: Attack, Defend, and Capture, switchable per team.
- Map editor: place Hills (elevation zones) and HQs, or erase with the Eraser tool. Units on high ground deal more damage and knockback.
- Capturable HQs with capture progress; losing an HQ typically means defeat.
- Keyboard shortcuts for fast team/unit selection.
- Adjustable spawn count and team selection for rapid deployment.
- AI Strategy Advisor: sends live army composition to Gemini and returns concise, commander-style tactical advice (`services/geminiService.ts`).

## Tech Stack

- React 19 + TypeScript
- Vite 6 (dev server, build, preview)
- HTML5 Canvas 2D rendering
- `@google/genai` (Gemini) for the strategic advisor
- `lucide-react` for icons

## Getting Started

### Prerequisites

- Node.js

### Installation

```bash
npm install
```

### Configure the Gemini API key

This app uses the Gemini API for the strategy advisor. Create a `.env.local` file in the project root and set your key:

```bash
GEMINI_API_KEY=your_api_key_here
```

(Vite maps `GEMINI_API_KEY` to `process.env.API_KEY` at build time via `vite.config.ts`.)

### Run

```bash
npm run dev      # start the dev server (http://localhost:3000)
npm run build    # production build
npm run preview  # preview the production build
```

## Project Structure

```
.
├── App.tsx                       # Root component: simulation ref, render loop, UI/editor state
├── index.tsx                     # React entry point
├── components/
│   ├── BattleCanvas.tsx          # Canvas renderer + map-editing interactions
│   ├── Controls.tsx              # Deployment, orders, and map-editor controls
│   └── StrategyAdvisor.tsx       # Gemini advisor panel
├── services/
│   ├── simulation.ts             # SimulationEngine: physics, squads, spatial grid, elevation
│   └── geminiService.ts          # Gemini strategic-advice calls
├── constants.ts                  # World size, unit configs, flocking & elevation tuning
├── types.ts                      # Enums and interfaces (Team, UnitType, OrderType, MapTool, ...)
└── metadata.json
```
