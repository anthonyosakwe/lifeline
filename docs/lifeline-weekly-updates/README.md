# LifeLine — Weekly Product Updates

**Group 39 · Phoenix Cohort · TS Academy PM Capstone**
*Rubric section G — Team Process & Execution Evidence*

---

## Week 1 Update — 2 May to 7 May 2026

**Theme: Direction locked. Discovery underway.**

### What we shipped this week

| Task | Owner | Status |
|---|---|---|
| Direction vote — SafetyTech / LifeLine selected | All | ✅ Done |
| Problem statement v1 drafted | PM | ✅ Done |
| 8 interviewees recruited | Research | ✅ Done |
| 5 discovery interviews conducted | Research | ✅ Done |
| Insight synthesis started | Research | ⏳ In Progress |

### Key decisions made

**D-01 — Product direction: LifeLine (Personal Safety & Check-In).**
Rationale: Group vote after evaluating 3 options (mental health, safety, finance). Safety had the clearest user pain that maps to a concrete product primitive — the journey check-in.

**D-02 — Primary persona: female campus students, not working professionals.**
Discovery interviews #1–3 consistently pointed to campus students as the highest-frequency, highest-pain user. The professional "Bolt ride at night" scenario is secondary — it's the same pain, but campus students face it daily.

### What we heard from users this week

- "Whenever I'm entering Bolt at night, I always send my live location to at least two people. Even after that, I still feel anxious till I reach home." — Amaka O., 22, student
- "There was one time my phone almost died while I was on a bike home. My sister kept calling because she was scared." — Tunde A., 24, NYSC
- "I usually pretend I'm on a call with someone so nobody thinks I'm alone." — Blessing E., 27, banker

### What changed our thinking

We started the week expecting to build an SOS-first product (panic button). Interview #2 (Tunde) flipped this: the real daily pain isn't emergencies — it's the anxiety of routine journeys with no structured check-in. **Prevention-first, not emergency-first.**

### Next week

- Complete remaining 3 interviews + synthesise all 8
- Draft user stories (10+) with acceptance criteria
- Define MoSCoW priorities
- Sketch lo-fi wireframes

---

## Week 2 Update — 10 May to 13 May 2026

**Theme: PRD locked. Design pack started.**

### What we shipped this week

| Task | Owner | Status |
|---|---|---|
| Write 10+ user stories with acceptance criteria | PM | ✅ Done |
| Define MoSCoW priorities | PM | ✅ Done |
| Sketch lo-fi wireframes (12 screens) | Design | ✅ Done |
| Build Figma design system (colour, type, components) | Design | ✅ Done (Should Have) |
| Complete insight synthesis from all 8 interviews | Research | ✅ Done |

### Key decisions made

**D-03 — Pattern 2A: two flows (Safe Arrival + SOS), not one.**
Early designs had a single SOS button as the product. Discovery evidence forced us to build Safe Arrival as the primary daily-use anchor. This is what makes the SOS credible when it actually fires.

**D-04 — OTP-only auth (no social login, no password).**
Rationale: password fatigue is real on Nigerian phones. OTP to a Nigerian number is universally understood and keeps onboarding under 90 seconds.

**D-05 — 3-second hold for SOS activation.**
Pocket-bump false alarms would destroy user trust immediately. Three seconds is deliberate enough to prevent accidents but fast enough in a real emergency.

### PRD snapshot (this week's output)

- 12 user stories written, including 4 in full Gherkin format
- MoSCoW: 8 Must Haves, 3 Should Haves, 2 Could Haves, 3 Won't Haves (now)
- NFRs defined: HTTPS, sub-3s load on 3G, WCAG 2.1 AA partial
- 10 edge cases documented (GPS denied, wrong OTP × 3, offline during SOS, etc.)

### Design decisions

- Dark-first palette selected (Navy #0A1E3F as primary) — night safety use case
- Helvetica throughout (no web fonts = faster load on poor networks)
- Touch targets ≥ 48dp on all emergency actions

### What's at risk

Figma prototype scope is ambitious — 12 hi-fi screens by end of week. Design team will prioritise the 3 critical flows (onboard, safe arrival, SOS) and leave secondary screens at lo-fi if time runs short.

### Next week

- Set up dev environment (GitHub repo, GitHub Pages)
- Define North Star metric formally
- Start build — screen 1 (Splash) to screen 5 (Trusted Contacts)

---

## Week 3 Update — 15 May to 17 May 2026

**Theme: Build environment live. North Star locked. First screens shipped.**

### What we shipped this week

| Task | Owner | Status |
|---|---|---|
| Set up GitHub repo + GitHub Pages deployment | Build | ✅ Done |
| Define North Star Metric (formal) | PM | ✅ Done |
| Build screens 1–5 (onboarding flow) | Build | ✅ Done |
| Embed Leaflet 1.9.4 inline (no CDN) | Build | ✅ Done |
| First group review + feedback session | All | ✅ Done |

### Key decisions made

**D-06 — Self-host Leaflet JS + CSS inline, no CDN.**
jsDelivr and unpkg are unreliable on MTN 3G in Nigeria. Our SafeSignal experience proved this definitively. Embedding Leaflet (~147KB) directly into the HTML means the map library loads from the same origin as the app — zero CDN risk on demo day.

**D-07 — Demo OTP code: 8484.**
Memorable on pitch day. Any other code deliberately triggers the failure path (visual shake, attempts counter, error message) — which is itself good demo material showing edge case handling.

### North Star Metric (locked)

**% of journeys ending in successful safe-arrival confirmation.**
Formula: (Trips where "I've arrived safely" tapped before ETA expired) ÷ (Trips started) × 100
Target: ≥ 90% at MVP review.

Rationale: directly tied to the core promise, observable from day one, demo-able on pitch day, cannot be gamed by superficial engagement metrics.

### Build progress

- Screens 1–5 built and matching Figma: Splash, Onboarding 1, OTP Verify, Onboarding 2, Trusted Contacts
- Countdown timer working correctly (decrements 1/sec, shows "OVERDUE" at 0:00)
- OTP failure path working: shake animation, red error, attempts counter

### Group review feedback

"This feels too perfect. Real users will hit errors." — Prompted us to prioritise failure paths and delighters for Week 4.

### What's at risk

One week left. Build team needs to ship screens 6–12 (4 flows) plus 3 failure paths plus delighters. Scope is tight. Deprioritising: animation polish, advanced contact management UI.

### Next week

- Complete screens 6–12 (Safe Arrival + SOS flows)
- Add 3 failure paths (wrong OTP, location denied, ETA overdue)
- Add 2 delighters (confetti, shake-to-SOS)
- Demo nav bar for pitch day
- Draft pitch deck v1

---

## Week 4 Update — 19 May to 25 May 2026 (Final Week)

**Theme: All 12 screens shipped. 30/30 tests passing. Deck done.**

### What we shipped this week

| Task | Owner | Status |
|---|---|---|
| Screens 6–12 (Safe Arrival + SOS flows) | Build | ✅ Done |
| Failure path 1: wrong OTP (shake + counter) | Build | ✅ Done |
| Failure path 2: GPS location denied (modal) | Build | ✅ Done |
| Failure path 3: trip ETA overdue (red OVERDUE banner) | Build | ✅ Done |
| Delighter 1: confetti on safe arrival | Build | ✅ Done |
| Delighter 2: shake-to-SOS hint toast | Build | ✅ Done |
| Demo navigation bar (bottom) | Build | ✅ Done |
| 30 manual test cases — all passing | Build | ✅ Done |
| Deployed to GitHub Pages | Build | ✅ Done |
| Pitch deck v4 (10 slides + speaker notes) | GTM | ✅ Done |
| PRD v3 FINAL | PM | ✅ Done |
| One-Pager v3 FINAL | PM | ✅ Done |
| Discovery Evidence v2 + Qualitative Notes | Research | ✅ Done |
| Survey Responses (n=52) | Research | ✅ Done |
| GTM Mini-Plan v2 | GTM | ✅ Done |
| Metrics & Tracking Plan v2 | PM | ✅ Done |
| Decision Log v2 (8 decisions) | PM | ✅ Done |
| Roadmap v5 HTML (Product + Architecture tabs) | PM | ✅ Done |
| README updated + persona aligned | Build | ✅ Done |

### Key decisions this week

**D-08 — Pitch deck format: PPTX.**
Team consensus — judges and judges only. PPTX is the standard expected format at TS Academy pitches.

### Live demo confirmed working

URL: `https://tsa-phoenix-safetytech-39.github.io/lifeline/lifelineapp`
- Tested on iPhone 13 mini (iOS Safari) ✅
- Tested on Tecno Camon 19 (Android Chrome) ✅
- Tested on MTN 3G throttled (Chrome devtools) ✅
- 30/30 manual test cases passing ✅

### What changed in Iteration 2 (this week)

Before: Only happy paths implemented. No delighters. No failure states.
After: 3 failure paths + 2 delighters shipped.

**Why this matters for the rubric:** Failure paths prove the team thought about real users on real networks. The confetti delighter creates an emotional reward loop that makes safe-arrival the daily habit — which is what makes the SOS credible when it fires.

### Iteration log summary

| | Before | After |
|---|---|---|
| Architecture | CDN-dependent Leaflet | Self-hosted inline (zero CDN) |
| Screen coverage | Screens 1–5 (happy path only) | All 12 screens, 3 failure paths, 2 delighters |
| OTP | Worked but no error state | Shake animation, counter, resend timer |
| Map offline | Broken icon tiles | Graceful grey fallback |
| Demo experience | Linear — had to show in order | Demo nav bar — jump to any flow in 1 tap |

### Rubric mapping (final)

| Rubric Section | Points | Our evidence |
|---|---|---|
| A: Problem & Discovery | 15 | Discovery Evidence v2, 8 interviews, n=52 survey |
| B: Product Strategy & MVP | 15 | PRD v3, One-Pager v3, MoSCoW priorities |
| C: UX/UI Design Quality | 20 | Design Pack (Figma), Product Design HTML |
| D: Build Quality | 20 | Working demo, 30 test cases, architecture, README |
| E: Metrics & Measurement | 10 | Metrics & Tracking Plan v2 |
| G: Team Process | 10 | RACI, Sprint Board v3, Roadmap, these weekly updates |
| **Total** | **90+** | |

### Lessons for next cohort

1. Let discovery lead — our SOS-first product became prevention-first after interview #2.
2. Network constraints are a product requirement, not a DevOps problem.
3. Honest scope beats aspirational scope — judges can tell.

---

*LifeLine · Group 39 · Phoenix Cohort · TS Academy PM Capstone · May 2026*
