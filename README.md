# SafeCity AI — Ambulance Green Corridor

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)
[![Next.js](https://img.shields.io/badge/Next.js-14-black.svg)](https://nextjs.org/)
[![TailwindCSS](https://img.shields.io/badge/TailwindCSS-3.4-38bdf8.svg)](https://tailwindcss.com/)
[![TypeScript](https://img.shields.io/badge/TypeScript-5.0-blue.svg)](https://www.typescriptlang.org/)
[![Status](https://img.shields.io/badge/Status-Hackathon--Ready-brightgreen.svg)]()

> **Intelligent Emergency Preemption Dashboard for Abbottabad, Pakistan.**  
> CCTV-based computer vision detects approaching emergency vehicles, computes optimal paths to City Hospital, and dynamically pre-empts traffic signals to green ahead of the ambulance—saving critical golden-hour minutes.

---

> **SIMULATION NOTICE:** SafeCity AI is a simulation dashboard created for educational and hackathon demonstration purposes. It models emergency vehicle preemption (EVP) logic and **does not control or manipulate physical traffic signal hardware**.

---

## Live Demo & Preview
- **Production URL:** [https://safecity-ai.vercel.app](https://safecity-ai.vercel.app) *(TBD upon deployment)*
- **Demo Prototype:** Open [prototype/safecity-frontend.html](file:///c:/Users/ATECH/Desktop/Hachathon/prototype/safecity-frontend.html) directly in any web browser.

### Preview Screenshots
| Live Detection & CCTV Feed | Green Corridor & Signal Map |
|:---:|:---:|
| ![CCTV Detection Placeholder](https://placehold.co/600x340/0f172a/ffffff?text=CCTV+Detection+Feed) | ![Route Map Placeholder](https://placehold.co/600x340/0f172a/ffffff?text=Green+Corridor+Map) |

---

## Demo-Critical Feature & Differentiator
- **Demo-Critical Flow:** When an ambulance appears in camera `CCTV-01` (Main Boulevard), AI detection triggers an immediate route calculation to City Hospital, dynamically pre-empting all 4 downstream traffic intersections to Green.
- **The Differentiator:** A real-time synchronized map showing the ambulance marker navigating along Main Boulevard, signal countdown timers switching ahead of the vehicle, instant dispatch alert dispatched to Rescue 1122, and live calculation of "ETA with vs. without corridor" (highlighting minutes saved).

---

## Architecture Overview

```mermaid
graph TD
    CCTV[CCTV Camera Stream / Demo Video Clip] -->|Frames| DETECT[AI Detection Engine / Mock /api/detect]
    DETECT -->|Ambulance Confirmed >= 0.85| CORE[SafeCity Corridor Engine]
    CORE -->|Route & ETA Calculation| ROUTE[OSRM / Leaflet Map Coordinates]
    CORE -->|Signal Preemption Request| SIGNALS[Signal Controller / Mock /api/signals]
    CORE -->|Automated Alert| RESCUE[Rescue 1122 Emergency Dispatch Alert]
    SIGNALS -->|Green Wave Status & Countdowns| DASH[SafeCity Operations Dashboard]
    ROUTE -->|Live Marker & Polyline| DASH
    RESCUE -->|Event Log & Audit Trail| DASH
```

---

## Tech Stack

| Layer | Technology | Purpose |
|---|---|---|
| **Frontend Framework** | Next.js 14 (App Router) + TypeScript | Responsive, accessible emergency operations dashboard |
| **Styling & System** | Tailwind CSS + Solid Design Tokens | Precision high-contrast UI (No gradients, WCAG AA compliant) |
| **Mapping & GIS** | Leaflet + OpenStreetMap | Interactive corridor tracking & intersection markers |
| **Icons** | Lucide React | Consistent, lightweight vector iconography (No emojis) |
| **State & Data Fetching** | React Hook Form, Zod, SWR / React State | Predictable contract parsing and mock-first state |
| **Backend & Storage** | Next.js Server Actions / Supabase (Optional) | Signal state orchestration and historical event logging |
| **Deployment** | Vercel | Instant global edge preview and production hosting |

---

## Quick Start Guide

### 1. Prerequisites
- Node.js 18.17+ or 20+
- npm or pnpm

### 2. Installation
```bash
git clone https://github.com/safecity-ai/safecity-green-corridor.git
cd safecity-green-corridor
npm install
```

### 3. Environment Configuration
Copy the template environment file:
```bash
cp .env.example .env.local
```
*(All frontend features run with 100% functional mock-first fallbacks if backend env vars are empty).*

### 4. Running Locally
```bash
npm run dev
```
Open [http://localhost:3000](http://localhost:3000) in your browser.

---

## Project Repository Structure
```
├── /app                  # Next.js App Router (Dashboard pages & API routes)
├── /brain                # Complete Project Brain (PRD, Architecture, Decisions, etc.)
│   ├── 00-START-HERE.md  # Reading roadmap & phase tracking
│   ├── changes/          # Changelog, current-state, and session logs
│   └── prompts/          # AI prompt templates for auditing and features
├── /components           # Reusable atomic UI components (Tokens compliant)
├── /prototype            # Standalone single-file HTML prototype reference
├── /public               # Static assets, camera test clips, map markers
└── CLAUDE.md             # AI Agent master operational entrypoint
```

---

## Team SafeCity AI

| Member | Role | Primary Ownership |
|---|---|---|
| **Abdul Wahid** | Lead Frontend Engineer | Responsive UI, Design Tokens, Map & Dashboard Components (`/app`, `/components`, `/styles`) |
| **Zeeshan Maqsood** | Backend & DevOps Lead | Data Contracts, Signal Orchestration API, Supabase, Vercel Deployments (`/app/api`, `/lib`, `/supabase`, `/ml`) |
| **Malik Faseeh Awan** | Product & Demo Lead | Project Brain, Demo Video, Pitch Deck, Testing Checklist, Submission Package (`/brain`, `/demo`, `/docs`) |

---

## License
This project is open-source software licensed under the [MIT License](file:///c:/Users/ATECH/Desktop/Hachathon/LICENSE).
