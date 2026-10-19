# ROLE
You are a senior full-stack engineer and technical project manager at a 4-hour hackathon. Create the complete project "brain" (documentation + rules + tool choices) BEFORE writing any app code, so any AI agent can resume work at any time with full context of the project, from start to end.

# PROJECT INPUTS (FILLED)

- **Idea:** SafeCity AI – Ambulance Green Corridor. CCTV-based AI detects an approaching ambulance, calculates the shortest route to the hospital, and switches traffic signals to green along that route so the ambulance is not delayed. A live dashboard shows the camera feed with detection boxes, the route map, signal states, ETA, speed, route progress and an event log.
- **Team (3 people, folder ownership):**
  | Member | Role | Owns |
  |---|---|---|
  | Abdul Wahid | Frontend / UI (fully responsive) | `/app/(dashboard)`, `/components`, `/styles` |
  | Zeeshan Maqsood | Backend / deploy / data | `/app/api`, `/lib`, `/supabase`, `/ml` (detection service or mock), production deploys |
  | Malik Faseeh Awan | Presentation, demo and other tasks | `/brain`, `/demo`, `/docs`, pitch deck, demo script, fallback video, submission summary, testing checklist, session logging |
  - Zeeshan is the single deploy owner. Every PR is reviewed by a different member before merging into `main`.
  - Detection (ambulance model) has no separate owner: Zeeshan owns the `/api/detect` contract and starts with a scripted mock; Faseeh prepares the demo clip and test frames. A real model (e.g. YOLO on Hugging Face Spaces) is a COULD item, started only if the backend is done before the 3:00 freeze.
- **Preferred stack:** Stack C (ML/AI), scaled down: Next.js + TypeScript + Tailwind on Vercel; Supabase (Postgres, Auth, Realtime); optional FastAPI detection service in `/ml` (Hugging Face Spaces or Render). Mock-first: `/api/detect` returns scripted results from a pre-recorded clip until a real model works. If the model slips, fall back to Stack A with detection fully mocked. Map: Leaflet + OpenStreetMap. Icons: Lucide. Justify in DECISIONS.md.
- **Judging criteria:** Not provided (hackathon name and theme: TBD, needs human decision). Assume innovation, technical execution, design, impact, demo quality. Impact angle: faster emergency response, lives saved.
- **Demo-critical feature (one sentence):** When an ambulance appears in the CCTV feed, the system detects it, computes the route to the hospital, and turns the signals along that route green in real time on the dashboard.
- **Wow factor / differentiator:** A simulated live green corridor: the ambulance marker moves along the map while signals ahead flip to green with countdowns, an auto-alert goes to Rescue 1122, and the dashboard shows ETA with vs. without the corridor (time saved).
- **Mode:** LEAN. Fully write PRD, ARCHITECTURE, DESIGN, BUILD_PLAN, TOOLS, WORKFLOW, DEPLOYMENT, CLAUDE.md, README. CONTRIBUTING.md is also written in full (team project). Create short stubs (headings + TBD) for the rest.
- **Time budget:** 4 hours total, deploy-ready.
- **Demo setting (assumed, change if wrong):** Abbottabad, Khyber Pakhtunkhwa, Pakistan; emergency service Rescue 1122; one hospital called "City Hospital" (placeholder, verify real names); 4 intersections; camera CCTV-01 "Main Boulevard". The system SIMULATES signal control and never controls real hardware.
- **Language / license (assumed):** English-only UI, MIT license.

# EXISTING WORK (read before planning)
A frontend prototype already exists: a single-file, fully responsive HTML dashboard (`safecity-frontend.html`, mock data, no backend). It is the visual and behavioral reference for the real frontend. Place a copy under `/prototype/` and treat it as a reference asset, not production code.

What the prototype contains (Verified):
- Header: logo, nav, live clock, "System active" status, dark-mode toggle.
- Sidebar (drawer on <1100px): Live monitor, Route & map, Signal control, Event history, Analytics, CCTV sources, Hospital locations, System settings; Emergency mode and Rescue 1122 notes.
- Live monitor: CCTV frame with detection boxes (Ambulance 0.94, Car 0.82, Car 0.76, Motorcycle 0.71), stat cards (Ambulance detected + confidence, Estimated arrival + distance, Current speed), "Simulate camera offline" and "Alert Rescue 1122" actions.
- Ambulance route map (SVG) with moving marker, signal icons with minute badges, legend.
- Traffic signals status (Intersections 1–4 with countdowns), Route progress, Event log (with empty state and Clear).
- Design tokens as CSS variables: solid colors, one blue accent, semantic red/green/amber, 4 shadow levels, 4px spacing, radius scale, Helvetica Neue → Helvetica → Arial stack, Lucide icons, WCAG-minded focus rings, reduced-motion support, light/dark theme.

Known gaps (Verified): no Modal, Table or Input components; no separate pages for Analytics, Event History, Signal Control; no real data; not yet ported to Next.js + Tailwind.

Adjustments to the original rules because code already exists:
- Do NOT write app code in this phase. Documentation only.
- Initialize `current-state.md` with: "Project initialized. Frontend prototype exists (single HTML file, mock data). No backend yet." Label claims Verified / Inferred / Unknown.
- The first frontend task is porting the prototype to Next.js + TypeScript + Tailwind components using the DESIGN.md tokens.

# TASK
Create ONLY documentation files now. Do NOT write app code. Create this structure:

```
/CLAUDE.md                  ← agent entry point: summary, "read /brain/00-START-HERE.md first", hard rules, commands
/AGENTS.md                  ← one line pointing to CLAUDE.md
/README.md                  ← what, live demo link, GIF/screenshot placeholders, badges, architecture diagram, setup, env vars, scripts, tech stack, team credits (Abdul Wahid, Zeeshan Maqsood, Malik Faseeh Awan), license
/CONTRIBUTING.md            ← branch/PR rules (<name>/<feature>), folder ownership table above
/.env.example               ← all env var names, no real values
/prototype/                 ← copy of safecity-frontend.html (reference only)
/brain/
  00-START-HERE.md          ← reading order, one-liner, current phase, links to all files
  PRD.md                    ← opens with the demo-critical feature sentence; problem, target users, goals, non-goals, user stories, MUST/SHOULD/COULD scope, wow factor, success criteria, acceptance criteria per feature, post-hackathon roadmap
  ARCHITECTURE.md           ← stack, folder structure, data flow, auth flow, components, services, Mermaid diagrams, code conventions
  DATA_MODEL.md             ← tables/entities, relations, indexes, RLS/access rules, seed data + demo account plan
  API_SPEC.md               ← endpoints/server actions, request/response, auth, error format, rate limits
  DESIGN.md                 ← design system (rules below)
  TOOLS.md                  ← chosen services, why, free-tier limits, setup links, accounts checklist, fallbacks (rules below)
  BUILD_PLAN.md             ← 4-hour timeboxed plan with checkboxes, owners, cut list (below)
  TESTING.md                ← strategy, critical-path manual checklist, minimal automated tests, Lighthouse targets, definition of done
  DEPLOYMENT.md             ← deploy steps per service, env vars, domains, DB setup, preview vs prod, rollback, post-deploy smoke test
  ENV.md                    ← every env var: name, purpose, where used, secret?, where to get it (NO real values)
  WORKFLOW.md               ← humans + agents: roles, branching, commit format, task loop, logging rules, freeze rules
  DECISIONS.md              ← ADR log: decision → options → why → date
  SECURITY.md               ← auth, secrets, RLS, validation, rate limiting, CORS, security headers, dependency checks
  PRODUCTION_READINESS.md   ← checklist (below), each item tagged MUST / SHOULD / SKIP-FOR-HACKATHON with status
  RISKS.md                  ← top risks + fallback for each (API down, deploy fails, scope creep, free-tier limits, Wi-Fi failure, detection model fails)
  DEMO_PITCH.md             ← 3-min demo script, pitch deck outline (problem, solution, demo, tech, future), judging-criteria mapping, Devpost-style submission summary, backup demo plan
  GLOSSARY.md               ← domain terms (green corridor, preemption, intersection, ETA, detection, confidence), naming conventions
  ETHICS_PRIVACY.md         ← REQUIRED (AI + CCTV video used): faces/plates data minimization, no storage of raw video, model limits/false positives, simulation-only disclaimer, consent, bias
  /changes/
    changelog.md            ← verified changes only
    current-state.md        ← what actually exists right now
    /sessions/              ← one file per work session/feature
  /prompts/
    audit-changes.md        ← reusable read-only audit prompt (below)
    new-feature.md          ← template to start a feature
    bugfix.md               ← template for debugging
    refactor.md             ← template for safe refactors
    review.md               ← template for code review
    deploy-fix.md           ← template for failed deploys
    ui-polish.md            ← template for design-token-compliant UI polish
```

# PROJECT-SPECIFIC CONTENT TO USE (be concrete, no generic filler)

**Entities (DATA_MODEL.md):** `cameras` (id, name, location, stream_url, status), `intersections` (id, name, lat, lng, signal_state, timer_seconds, priority_mode), `hospitals` (id, name, lat, lng), `routes` (id, ambulance_session_id, polyline, distance_km, eta_seconds), `detections` (id, camera_id, class, confidence, bbox, detected_at), `ambulance_sessions` (id, camera_id, hospital_id, status, speed_kmh, progress, started_at), `events` (id, session_id, type, title, detail, created_at), `profiles` (demo admin). Seed: 1 camera, 4 intersections, 1 hospital, 1 demo session, 5 events, 1 demo account.

**Screens (PRD.md / ARCHITECTURE.md):** Live Monitor (MUST), Route & Map (MUST), Signal Control (SHOULD), Event History (SHOULD), Analytics (COULD), CCTV Sources, Hospital Locations, System Settings (COULD/stubs).

**Endpoints (API_SPEC.md):**
- `POST /api/detect` → `{class, confidence, bbox[]}` (mock-first)
- `GET /api/route?session=` → `{polyline, distance_km, eta_seconds, stops[]}`
- `POST /api/signals/priority` → sets green along route, returns signal states + countdowns
- `GET /api/signals` → states of 4 intersections
- `GET /api/events` and `POST /api/events/alert-rescue` (simulated Rescue 1122 alert)
- `GET /api/health`
- Realtime channels: `signals`, `events`, `ambulance_sessions`.
- Contract rule: Zeeshan and Abdul Wahid agree the JSON shapes for `/api/detect`, `signals` and `events` in the first 20 minutes so the frontend builds against mocks.

**Frontend (ARCHITECTURE.md):** feature-based folders, components ported from the prototype: `Header`, `Sidebar` (drawer on <1100px), `CameraFeed` (+ offline error state), `StatCards`, `RouteMap`, `SignalsPanel`, `RouteProgress`, `EventLog` (+ empty state), `ThemeToggle`, `Toast`, plus missing Modal, Table, Input, Skeleton. Fully responsive (breakpoints 640 / 1100), mobile menu, skip-to-content.

# DESIGN RULES (DESIGN.md)
- Solid colors only. NO gradients, NO "AI-style" purple/blue glow palettes, no glassmorphism.
- Palette tokens: background, surface, border, text-primary, text-secondary, accent, success, warning, danger, each with 3–5 shades (50–900) as hex values. Start from the prototype tokens (accent blue `#1d4ed8` / `#2563eb`; red, green, amber reserved for emergency, success and warning meanings, never decoration).
- Black/white base + ONE accent color. Depth comes from shadows only: 4 levels (sm/md/lg/xl) as tokens.
- Typography: Helvetica Neue → Helvetica → Arial system stack (no font files to license or host). State this and why.
- Define type scale, weights, line heights, spacing scale (4px base), radius scale, breakpoints, grid, and ONE icon library (Lucide).
- Components with default/hover/focus/disabled/loading states: button, input, card, modal, toast, table, nav, empty state, skeleton, error state.
- Accessibility: WCAG AA contrast, visible focus, alt text, keyboard navigation.
- Output tokens as CSS variables + a Tailwind config snippet.
- UI libraries (shadcn/ui, Radix) must be restyled to these tokens, with no default gradients.

# TOOLS RULES (TOOLS.md)
- Pick ONE tool per category from the catalog. Prefer the fewest services possible (each adds setup time and failure points).
- For each pick, record: purpose, free-tier limits (VERIFY on the official pricing page, limits change), env vars, setup time estimate, fallback.
- Include an "Accounts to create in the first 15 minutes" checklist (GitHub, Vercel, Supabase; Hugging Face only if a real model is attempted).
- Flag every free-tier gotcha that could break the demo.
- Add a short cost/scaling note: how this works beyond the free tier.
- Log each choice in DECISIONS.md.

## CATALOG
| Category | Free options |
|---|---|
| Code hosting / CI | GitHub + GitHub Actions |
| Frontend hosting | Vercel, Netlify, Cloudflare Pages |
| Backend hosting | Next.js API routes/server actions on Vercel (default), Render, Railway (trial credits), Fly.io, Cloudflare Workers, Supabase Edge Functions |
| Database (SQL) | Supabase (Postgres), Neon (Postgres), Turso (SQLite) |
| Database (NoSQL) | MongoDB Atlas, Firebase Firestore |
| Cache / rate limit / queues | Upstash Redis, Upstash QStash |
| Auth | Supabase Auth, Clerk, Auth.js, Firebase Auth |
| File uploads / storage | Supabase Storage, Cloudinary, UploadThing, Cloudflare R2 |
| Email (transactional) | Resend, Brevo, SendGrid, Mailtrap (testing only) |
| Realtime | Supabase Realtime, Pusher, Ably, Socket.io on Render |
| Payments (test mode) | Stripe test mode, Lemon Squeezy, Paddle sandbox (not needed here: SKIP) |
| AI / LLM APIs | Google Gemini API, Groq, OpenRouter (free models), Hugging Face Inference, Ollama (local) |
| Search | Supabase full-text search, Algolia, Meilisearch, Typesense |
| Background jobs / cron | Vercel Cron, GitHub Actions schedule, Inngest, cron-job.org |
| Analytics | Vercel Analytics, PostHog, Plausible (trial), Umami, Google Analytics |
| Error tracking | Sentry, PostHog |
| Uptime / keep-alive | UptimeRobot, Better Stack, cron-job.org |
| Maps | Leaflet + OpenStreetMap, Mapbox |
| Domains / DNS / CDN | Cloudflare, free *.vercel.app subdomain, GitHub Student Pack domains |
| UI components | shadcn/ui, Radix UI, Headless UI |
| Icons | Lucide, Phosphor, Heroicons (pick ONE: Lucide) |
| Fonts | Inter, Geist, system Helvetica stack |
| Images / assets | Unsplash, Pexels, undraw (check licenses) |
| Forms / validation | React Hook Form + Zod |
| Data fetching / state | TanStack Query, Zustand |
| Testing | Vitest, Playwright, Postman/Bruno |
| API docs | OpenAPI/Swagger, Scalar |
| Design / mockups | Figma, Excalidraw, Mermaid |
| Secrets | Vercel/Render env vars, GitHub Secrets, .env.local (never commit) |
| Legal templates | Termly, iubenda, or generated drafts (verify for your jurisdiction) |

## DEFAULT STACKS (pick one, justify in DECISIONS.md)
- A. Fastest: Next.js + TypeScript + Supabase (DB + Auth + Storage + RLS) + Resend + Vercel. 3 accounts, no separate backend.
- B. Separate API: React/Vite on Vercel + Express/FastAPI on Render + Neon + Clerk.
- C. ML/AI project: Next.js on Vercel + FastAPI on Render/Hugging Face Spaces + Supabase + Gemini/Groq.
- **Chosen for this project:** C scaled down, with A as the fallback (see Preferred stack).

## GOTCHAS TO DOCUMENT IN TOOLS.md
- Render free web services sleep after inactivity (slow first request). Add a keep-alive ping or warm up before the demo.
- Railway has no permanent free plan (trial credits only). Never a hard dependency.
- Supabase free projects pause after inactivity. Open the dashboard before the demo.
- Vercel Hobby is non-commercial only, and serverless functions have execution time limits.
- Resend/email free tiers need a verified domain to send to arbitrary recipients, otherwise only to your own email.
- Hugging Face Spaces free hardware can sleep and be slow; keep the mock as the default demo path.
- Record exact free-tier numbers for storage, bandwidth, and emails/day after checking official pages. Do not guess them.

# BUILD_PLAN.md (4 hours)
Timeboxed phases with checkboxes, owner (Abdul Wahid / Zeeshan Maqsood / Malik Faseeh Awan), and "done when" per task:
- 0:00–0:20 setup: repo, stack, accounts, env, deploy an EMPTY app to Vercel FIRST; agree JSON contracts for `/api/detect`, `signals`, `events`
- 0:20–1:00 data model + auth + seed script skeleton (Zeeshan); port prototype shell, tokens and layout to Next.js + Tailwind against mock data (Abdul Wahid); demo script draft and clip preparation (Faseeh)
- 1:00–2:30 demo-critical feature + wow factor (build these FIRST, mock-first): detection → route → green corridor → moving marker
- 2:30–3:00 secondary features + polish (Signal Control, Event History, remaining components and states)
- 3:00 DEPENDENCY FREEZE
- 3:00–3:15 seed data + demo account ready (hard deadline 3:15)
- 3:15–3:30 production-readiness MUSTs, mobile, error/empty/loading states
- 3:30 pre-record a 60–90s fallback demo video (Faseeh)
- 3:40–4:00 final deploy (Zeeshan), smoke test, demo rehearsal led by Faseeh with all three, submission summary

Rules:
- Scope-cut rule: if a phase runs >20% over, cut SHOULD/COULD items.
- Include an explicit CUT LIST (items dropped first, in order): real detection model → Analytics → Event History filters → Signal Control manual overrides → dark mode polish.
- Split work by folder/owner to avoid merge conflicts.
- Mock-first: build UI against stubbed data, then wire the backend.
- At each phase end the agent reports: on track / behind / cut list applied.
- Keep the deployed app working at all times (deploy early, deploy often).

# PRODUCTION_READINESS.md
Merge, dedupe, and prioritize for a 4h hackathon. Tag each MUST / SHOULD / SKIP-FOR-HACKATHON.
- **Auth/Account:** real login/logout, password reset, email verification, delete account, onboarding flow.
- **UX states:** loading, empty, clear error messages, form validation + success/error states, custom 404, confirmation modals, hover states.
- **UI features:** mobile layout + mobile menu, dark mode toggle, sticky header, skip-to-content, password visibility toggle, back-to-top, site search, copy button, scroll progress bar, expandable FAQ, floating contact button, last-updated date, print stylesheet.
- **Backend/Security:** rate limiting, DB backups, row-level security, API keys never on frontend, input validation, data minimization, audit third-party SDKs, data deletion requests, unsubscribe link in emails.
- **Observability:** analytics, error tracking, UTM tracking.
- **Legal/Compliance** (flag "not legal advice, verify for your jurisdiction"): privacy policy, terms, refund policy, cookie policy + consent banner, form consents, age consent for kids' data, no dark patterns/hidden fees, no fake reviews/unsupported claims, licensed fonts and images, business details.
- **Accessibility:** alt text, color contrast, keyboard navigation.
- **Also add anything missing:** SEO meta/OG tags, favicon, robots/sitemap, env separation (dev/prod), health-check endpoint, seed/demo data, CORS, security headers, image optimization, performance budget, git hygiene (.gitignore, no secrets committed), CI check, license, dependency audit, verified email sender, keep-alive for sleeping servers.
- **Project-specific:** clear "simulation only, no real signal control" notice in the UI and README; no raw CCTV video stored; the demo clip must be licensed or self-recorded.

# ARCHITECTURE.md: CODE CONVENTIONS
- TypeScript strict, no `any`, consistent naming, feature-based folders.
- One error-handling pattern (typed errors, consistent API error format).
- Validate all input with Zod at boundaries.
- No hardcoded colors; use DESIGN.md tokens only.

# TESTING.md: TARGETS
- Manual critical-path checklist (login → camera detects ambulance → route calculated → corridor activated → marker reaches hospital → logout) run before every deploy.
- Minimal automated tests for the core feature only (detect → route → priority).
- Lighthouse targets: Performance ≥ 90, Accessibility ≥ 95, LCP < 2.5s (adjust if justified).
- Responsive checks at 360, 768, 1100 and 1440px widths.

# WORKFLOW.md: AGENT ROLES AND RULES
- Roles (separate sessions, no overlap): Planner (updates docs/plan), Builder (implements one task), Reviewer (checks against PRD, DESIGN, SECURITY).
- Task-size rule: max 30 minutes per task, commit after each, deploy at least once per phase.
- Dependency freeze after 3:00. No new packages or services without human approval.
- Token budget: every /brain file stays under 300 lines. Agents read only files relevant to the current task, plus the mandatory start-of-work files.
- Humans: branches `<name>/<feature>`, PRs reviewed by a different member, Zeeshan deploys production.

# LOGGING SYSTEM (/brain/changes): "git for conversations"
WORKFLOW.md and CLAUDE.md must make this a HARD RULE for every agent:
1. Before work: read 00-START-HERE.md, current-state.md, and the last 3 session files.
2. After EVERY feature/fix/decision, create `/brain/changes/sessions/YYYY-MM-DD-NN-short-title.md` containing:
   - Goal / user request (summarized, key prompts quoted)
   - What was done (files touched)
   - Decisions + reasoning
   - Problems hit + fixes
   - Status (Done / Partial / Blocked) + next steps
   - Related commit hash
3. Append a verified entry to changelog.md: `Change → Reason → Affected Area → Impact → Evidence → Status`
4. Update current-state.md (what exists now, incomplete work, inconsistencies, deprecated/removed items).
5. Update BUILD_PLAN.md checkboxes, and DECISIONS.md / TOOLS.md if relevant.
6. Commit with Conventional Commits (`feat:`, `fix:`, `docs:`, `chore:`), referencing the session file.
7. Never invent history. Tag claims as Verified / Inferred / Unknown.

Write /brain/prompts/audit-changes.md containing this read-only audit prompt:
"Analyze the project read-only and create/update only /brain/changes/changelog.md and current-state.md. Do not modify, delete, refactor, rename, or move source code; do not change dependencies, config, database, APIs, or behavior. Inspect the project structure first, then read only the files needed. Never invent history; label every claim Verified / Inferred / Unknown. Preserve existing docs and update instead of overwriting. Detect contradictions between docs and implementation. changelog.md: significant verified changes (added/removed/modified, behavior, architecture/API/DB, security/deployment, bug fixes, breaking changes, migrations), each as 'Change → Reason → Affected Area → Impact → Evidence → Status'. current-state.md: what exists now, active features, deprecated/removed components, incomplete changes, pending migrations, inconsistencies. Finish with a Change Audit: files created/updated, major verified changes, inconsistencies, unknown history, items needing human confirmation. Stop after documentation. Do not fix or implement anything."

# CLAUDE.md MUST CONTAIN
- 5-line project summary, demo-critical feature, wow factor, current phase
- Reading order of /brain files
- Hard rules: use DESIGN.md tokens only (no hardcoded colors, no gradients); never commit secrets; validate all input; keep the deployed app working; log every change per WORKFLOW.md; mock-first; dependency freeze after 3:00; ask before adding dependencies, new services, or changing architecture; keep tasks under 30 minutes; signal control is simulation only
- Commands: install, dev, build, test, lint, seed, deploy
- Definition of done for any task

# OUTPUT RULES
- Be specific to the idea: concrete entities, routes, tables, screens. No generic filler or lorem ipsum.
- Concise bullets and tables over prose. Mermaid for diagrams.
- Mark unknowns as "TBD (needs human decision)" instead of guessing. Known unknowns: hackathon name/theme/judging criteria, real vs. mocked detection, real city/hospital names, GitHub repo name and live URL.
- Never invent free-tier numbers or URLs; mark as "verify on official page".
- Map every MUST feature to at least one judging criterion in DEMO_PITCH.md.
- Initialize changelog.md and current-state.md as described in EXISTING WORK, and write the first session file documenting this scaffolding.
- At the end, output: files created, open questions for me (max 5), accounts I must create now, and the exact next step to start Phase 0.
- STOP after documentation. Do not scaffold code.
