# Contributing to SafeCity AI

Thank you for contributing to SafeCity AI! Because this project is developed within a fast-paced 4-hour hackathon environment, adherence to these workflow rules is mandatory for both human teammates and AI coding agents.

---

## Folder Ownership & Responsibilities

| Team Member | Role | Dedicated Ownership | Primary Responsibilities |
|---|---|---|---|
| **Abdul Wahid** | Frontend / UI Lead | `/app/(dashboard)`, `/components`, `/styles` | Building fully responsive Next.js + Tailwind components, Leaflet map integration, CCTV monitor, route progress, and Design Token adherence. |
| **Zeeshan Maqsood** | Backend / Data / DevOps | `/app/api`, `/lib`, `/supabase`, `/ml` | Defining mock and production API routes, Supabase migrations, data models, and is the **Single Production Deploy Owner**. |
| **Malik Faseeh Awan** | Product & Demo Lead | `/brain`, `/demo`, `/docs` | Maintaining the project "Brain", writing demo script, recording 60–90s fallback demo video, session logging, and pitch deck. |

---

## Branching Strategy
- **Base Branch:** `main` (always deploy-ready and passing build).
- **Branch Naming Scheme:** `<member-name>/<feature-or-fix-name>`
  - Examples:
    - `wahid/map-corridor-animation`
    - `wahid/camera-feed-detection-boxes`
    - `zeeshan/signals-priority-api`
    - `faseeh/demo-video-recording`

---

## Pull Request & Review Rules
1. **No Direct Pushes to `main`:** All changes must go through a pull request.
2. **Cross-Review Requirement:** Every PR must be reviewed and approved by a teammate *other* than the author before merging.
   - Example: A PR from Abdul Wahid (`wahid/*`) must be reviewed by Zeeshan Maqsood or Malik Faseeh Awan.
3. **Single Deployer Rule:** Only **Zeeshan Maqsood** merges approved PRs into `main` and triggers production deployments on Vercel to prevent deployment race conditions.
4. **Mock-First Contract Verification:** Before merging frontend or backend PRs, verify that the `/api/detect`, `/api/signals`, and `/api/events` JSON contracts match the schemas defined in [brain/API_SPEC.md](file:///c:/Users/ATECH/Desktop/Hachathon/brain/API_SPEC.md).

---

## Commit Message Convention
We adhere strictly to [Conventional Commits](https://www.conventionalcommits.org/):
- `feat:` A new user-facing feature
- `fix:` A bug fix
- `docs:` Documentation updates only (e.g., changes in `/brain`)
- `style:` Formatting or design token adjustments (no logic change)
- `refactor:` Code change that neither fixes a bug nor adds a feature
- `chore:` Tooling, dependencies, or configuration updates

**Commit Message Structure:**
```
feat(monitor): implement responsive CCTV detection overlays

- Render bounding boxes with confidence scores (Ambulance 0.94)
- Add camera offline simulation toggle
- Refs: brain/changes/sessions/2026-10-15-02-cctv-monitor.md
```

---

## Hackathon Timebox & Freeze Rules
- **0:00 – 0:20:** Setup, repo initialization, empty app deployed to Vercel, API contracts agreed.
- **0:20 – 1:00:** Prototype ported to Next.js shell + tokens; seed scripts drafted.
- **1:00 – 2:30:** Demo-critical feature (detect → route → green corridor → moving marker).
- **2:30 – 3:00:** Secondary panels, signal overrides, event logs, responsive polish.
- **3:00 DEPENDENCY FREEZE:** Zero new npm packages or external APIs may be introduced.
- **3:00 – 3:15:** Hard deadline: demo account and seed data verified.
- **3:30:** Fallback demo video pre-recorded.
- **3:40 – 4:00:** Final production freeze, smoke test, and presentation rehearsal.
