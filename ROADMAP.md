# StudentFlow — Build Roadmap

A step-by-step plan. Steps 1–10 ship the **web app** and validate with real users; step 11 adds **mobile** (reusing shared logic). This ordering is deliberate: shipping one polished platform first is faster to validate than building two UIs before any product exists — even though the architecture supports both.

## Phase 0 — Design (current)
- [x] Decide vision, audience, MVP scope, tech stack
- [x] Draft database schema
- [x] Generate primary design system (teal/orange flat)
- [x] Build mobile prototype (6 screens)
- [x] Build 2 alternates (web + mobile each) — `design/alternate-a-aurora.html`, `design/alternate-b-dark-focus.html`
- [x] Build primary web dashboard — `design/web-dashboard-primary.html`
- [ ] Finalize design direction with owner
- [ ] Design all screens for chosen direction (web + mobile)

## Phase 1 — Foundation
1. **Setup** — create Supabase project + monorepo scaffold (`apps/web`, `apps/mobile`, `shared`, `supabase`).
2. **Auth** — sign up / login (email + Google) via Supabase Auth.
3. **Database** — run `docs/DATABASE.md` schema + enable RLS + enable real-time.

## Phase 2 — Core features
4. **Assignments CRUD** — the core screen (list, add, edit, complete). 
5. **Daily tasks** — the "Today" view.
6. **Subjects** — color-coded organization.
7. **Calendar / agenda view** — everything by due date.
8. **Real-time** — wire Supabase subscriptions so edits sync live.

## Phase 3 — Engagement + launch web
9. **Reminders** — push/email notifications for due dates.
10. **Deploy web** (Vercel) → get real high-schoolers using it and gather feedback.

## Phase 4 — Mobile
11. **Build mobile (Expo)** — reuse `shared/` types + hooks, add push notifications. Submit to App Store / Play Store.

## Phase 5 — Polish
12. **Test + launch** both platforms. Begin v2 features (grades, focus timer, gamification) based on feedback.

## Guiding principle
Validate the web app with real users (step 10) before investing heavily in mobile polish. The shared-backend architecture means mobile is largely a reuse exercise once the web logic is proven.
