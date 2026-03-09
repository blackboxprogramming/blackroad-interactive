# BlackRoad Cloud

The unified web platform for BlackRoad OS — 21 page templates deployed across 99 Cloudflare Pages projects, Railway, 3 Raspberry Pis, and GitHub.

## Live Status (2026-03-09)

**99/99 Pages projects deployed** | **74/74 pages.dev URLs returning 200** | **18/41 custom domains healthy**

### Custom Domains — Working (200)

| Domain | Type |
|--------|------|
| blackroad.io | Primary |
| blackroadai.com | Brand |
| blackroadqi.com | Brand |
| blackroadquantum.info | Brand |
| blackroadquantum.net | Brand |
| blackroadquantum.shop | Brand |
| blackroadquantum.store | Brand |
| lucidia.earth | Lucidia |
| lucidiaqi.com | Lucidia |
| dashboard.blackroad.io | Subdomain |
| status.blackroad.io | Subdomain |
| console.blackroad.io | Subdomain |
| analytics.blackroad.io | Subdomain |
| api.blackroad.io | Worker |
| earth.blackroad.io | Subdomain |
| education.blackroad.io | Subdomain |
| finance.blackroad.io | Subdomain |
| legal.blackroad.io | Subdomain |

### Custom Domains — Issues

| Domain | Status | Issue |
|--------|--------|-------|
| blackroadinc.us | 521 | Origin down |
| blackroadquantum.com | 521 | Origin down |
| app.blackroad.io | 522 | Connection timeout |
| demo.blackroad.io | 522 | Connection timeout |
| roadcoin.io | 525 | SSL handshake failed |
| roadchain.io | 403 | Forbidden |
| stripe.blackroad.io | 404 | Worker route |
| creator-studio.blackroad.io | 530 | Origin DNS error |
| research-lab.blackroad.io | 530 | Origin DNS error |
| admin.blackroad.io | 000 | DNS/tunnel misconfigured |
| content.blackroad.io | 000 | DNS/tunnel misconfigured |
| customer-success.blackroad.io | 000 | DNS/tunnel misconfigured |
| design.blackroad.io | 000 | DNS/tunnel misconfigured |
| engineering.blackroad.io | 000 | DNS/tunnel misconfigured |
| healthcare.blackroad.io | 000 | DNS/tunnel misconfigured |
| hr.blackroad.io | 000 | DNS/tunnel misconfigured |
| marketing.blackroad.io | 000 | DNS/tunnel misconfigured |
| operations.blackroad.io | 000 | DNS/tunnel misconfigured |
| product.blackroad.io | 000 | DNS/tunnel misconfigured |
| resume.blackroad.io | 000 | DNS/tunnel misconfigured |
| sales.blackroad.io | 000 | DNS/tunnel misconfigured |
| signup.blackroad.io | 000 | DNS/tunnel misconfigured |
| support.blackroad.io | 000 | DNS/tunnel misconfigured |

## Stack

| Layer | Technology |
|-------|-----------|
| Framework | React 19.2 + Vite 7.3 |
| Routing | react-router-dom 7.13 |
| Charts | Recharts 3.8 |
| Payments | Stripe (via `stripe.blackroad.io` Worker) |
| Auth | Clerk (planned) |
| Hosting | Cloudflare Pages (99) + Railway + 3 Pis + GitHub |
| Build | 1.0 MB total (`dist/`) |
| Source | 12,506 lines across 21 pages + 4 libraries |

## Routes (22)

| Path | Component | Description |
|------|-----------|-------------|
| `/` | BlackRoadLanding | Landing page with pricing tiers |
| `/dashboard` | BlackRoadDashboard | Internal metrics and charts |
| `/os` | BlackRoadOS | Desktop OS with 9 apps |
| `/status` | BlackRoadStatus | System status monitor |
| `/chat` | BlackRoadChat | Chat interface |
| `/chat2` | BlackRoadChat2 | Chat v2 |
| `/terminal` | LucidiaTerminal | Lucidia terminal emulator |
| `/explorer` | BlackRoadExplorer | File/data explorer |
| `/chain` | RoadChainExplorer | RoadChain blockchain explorer |
| `/docs` | BlackRoadDocs | Documentation |
| `/about` | AboutPage | Company info |
| `/leadership` | LeadershipPage | Leadership team |
| `/auth` | BlackRoadAuth | Authentication |
| `/settings` | BlackRoadSettings | Settings panel |
| `/onboarding` | BlackRoadOnboarding | User onboarding flow |
| `/roadmap` | BlackRoadRoadmapPage | Product roadmap |
| `/brand` | BlackRoadBrandSystem | Brand system reference |
| `/brand-kit` | BrandTemplate | Brand template kit |
| `/animations` | BlackRoadAnimations | Animation showcase |
| `/command` | BlackRoadCommand | Command palette |
| `/pricing` | BlackRoadPricing | Stripe pricing + checkout |
| `/billing` | BlackRoadPricing | Billing management |

## Brand System

- **Background**: `#000000` (pure black)
- **Gradient stops**: `#FF6B2B` → `#FF2255` → `#CC00AA` → `#8844FF` → `#4488FF` → `#00D4FF`
- **Fonts**: Space Grotesk (headings), Inter (body), JetBrains Mono (code)

## Libraries

| File | Purpose | Lines |
|------|---------|-------|
| `src/lib/config.js` | Central config (Stripe keys, endpoints, price IDs) | — |
| `src/lib/hybrid-memory.js` | 12-layer hybrid memory engine (x2.18B multiplier) | 501 |
| `src/lib/pixel-memory.js` | Binary pixel memory (x4,096 multiplier) | — |
| `src/lib/trinary-memory.js` | Base-3 trinary memory (x531,441 multiplier) | — |

## Stripe Integration

- **Worker**: `stripe.blackroad.io` (Cloudflare Worker)
- **Endpoints**: `/checkout`, `/portal`, `/webhook`, `/prices`
- **Plans**: Operator ($0), Pro ($49/mo), Sovereign ($299/mo), Enterprise (custom)
- **Add-ons**: Lucidia Enhanced ($29), RoadAuth ($99), Context Bridge ($10), Knowledge Hub ($15)
- **Mode**: Live (not test)

## Deployment

All platforms deploy the same SPA build from `dist/`. SPA routing handled by `public/_redirects`.

### Platforms (all live, tested 2026-03-09)

| Platform | URL | Status |
|----------|-----|--------|
| **Cloudflare Pages** | 99 projects (74 pages.dev + 18 custom domains) | 200 |
| **Railway** | https://blackroad-cloud-production.up.railway.app | 200 |
| **GitHub** | https://github.com/blackboxprogramming/blackroad-cloud | Public |
| **Gitea** | http://192.168.4.97:3100/platform/blackroad-cloud | Internal |
| **Alice (Pi 400)** | http://192.168.4.49:8080 | 200 |
| **Cecilia (Pi 5)** | http://192.168.4.96:8080 | 200 |
| **Lucidia (Pi 5)** | http://192.168.4.38:8081 | 200 |

### CI/CD

GitHub Actions workflow (`.github/workflows/deploy.yml`) auto-deploys on push to `main`:
- Builds with Node 20
- Deploys to Cloudflare Pages
- Deploys to Railway
- Deploys to Pis via rsync (self-hosted runner)

```bash
npm run build                    # Build to dist/
npx wrangler pages deploy dist --project-name <name> --commit-dirty=true
railway up --detach              # Deploy to Railway
```

## Infrastructure

- **99 Cloudflare Pages projects** — all deployed
- **10 Cloudflare Workers** — api, stripe, verify, fleet, operator, core, dashboard-api, auth, quantum, road
- **3 Pi web servers** — Alice (:8080), Cecilia (:8080), Lucidia (:8081)
- **1 Railway service** — blackroad-cloud (production)
- **1 GitHub repo** — blackboxprogramming/blackroad-cloud (public)
- **1 Gitea repo** — platform/blackroad-cloud (Octavia)
- **23 Railway projects** — across the account
- **2 DigitalOcean droplets** — gematria, anastasia
- **WireGuard mesh** — 10.8.0.x overlay network
- **2x Hailo-8 AI accelerators** — 52 TOPS total (Cecilia + Octavia)
