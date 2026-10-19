# Environment Variables Reference — SafeCity AI

> **Rule:** Never commit live secrets or `.env.local` files to source control. This dictionary defines every variable, its security classification, and how to acquire it.

---

## 1. Environment Variables Dictionary

| Variable Name | Purpose | Where Used | Secret? | Source / Acquisition |
|---|---|---|---|---|
| `NODE_ENV` | Sets execution mode (`development` or `production`) | Next.js Core / Build | No | Set automatically by runtime |
| `NEXT_PUBLIC_APP_URL` | Base canonical application URL | SEO, metadata, callbacks | No | Set to Vercel production domain or `http://localhost:3000` |
| `NEXT_PUBLIC_ENABLE_MOCK_FALLBACK` | If `true`, system serves scripted Abbottabad data even without DB | Client State / APIs | No | Set to `true` by default in `.env.example` |
| `NEXT_PUBLIC_CITY_NAME` | Display city name for municipal branding | Header / Map / Meta | No | Defaults to `"Abbottabad"` |
| `NEXT_PUBLIC_DEFAULT_HOSPITAL` | Target medical destination label | Header / Stat Cards | No | Defaults to `"City Hospital"` |
| `NEXT_PUBLIC_EMERGENCY_SERVICE` | Dispatch agency name | Sidebar / Alerts | No | Defaults to `"Rescue 1122"` |
| `NEXT_PUBLIC_SUPABASE_URL` | Supabase API Gateway endpoint | Client DB queries | No | Supabase Project Settings -> API |
| `NEXT_PUBLIC_SUPABASE_ANON_KEY` | Public anonymous JWT token for client reads | Client Supabase Client | No (Public) | Supabase Project Settings -> API |
| `SUPABASE_SERVICE_ROLE_KEY` | Admin bypass key for server migrations/seeding | Server Actions / Seed | **YES** | Supabase Project Settings -> API -> Service Role |
| `ML_DETECTION_SERVICE_URL` | Optional remote YOLO FastAPI endpoint | `/api/detect` proxy | No | Hugging Face Space or Render URL (COULD item) |
| `ML_DETECTION_API_KEY` | Bearer token for remote ML inference | `/api/detect` proxy | **YES** | Hugging Face User Access Token |
| `RESCUE_1122_WEBHOOK_URL` | Endpoint for dispatch webhook simulation | `/api/events` route | No | SafeCity webhook mock or external testing hook |

---

## 2. Environment Verification Command
To verify that environment variables are properly mapped in local development without printing secret values:
```bash
npm run env:check
```
*(Implemented as a script that asserts keys exist in `process.env` and prints a green checkmark table).*
