# LifeLine — Build Documentation

**TS Academy · Phoenix Cohort · Group 39 · Capstone**
*Personal-safety check-in app for Nigerian users*
*Status: MVP shipped · May 2026*

---

## 1 · MVP Scope

### Problem
Nigerians — especially women, professionals working late, and students — face daily safety friction: there's no fast, low-friction way to tell trusted contacts "I'm on my way home" or "I need help" without taking out your phone, unlocking it, finding the right person, and sending a long message. Existing solutions (WhatsApp share-location, calling a friend) are slow, social, and don't scale to emergencies.

### Target user
**Primary:** Ada, 28, project manager in Lagos, takes Bolt rides home after late meetings, has two trusted contacts (sister + close friend).
**Secondary:** Parents of working young adults, university students.

### Value proposition
*"Tell your circle you made it home safely — before they have to ask."*
Prevention-first safety. The app is used **every day** (safe arrival), not just in emergencies — because the daily use is what makes the SOS work when it matters.

### MVP (what shipped)
| # | Capability | Why it's in MVP |
|---|---|---|
| 1 | Phone-OTP auth | Identity without passwords; ubiquitous on Nigerian phones |
| 2 | Trusted contacts (2-3) with consent | Network is the product |
| 3 | Safe-arrival trip with live map + ETA | Daily-use anchor; trains user habit |
| 4 | 3-second hold SOS with auto-escalation | Single primary safety action |
| 5 | Real OpenStreetMap with self-hosted library | Works on poorest networks |
| 6 | Three failure paths | Realistic UX, not just happy path |
| 7 | Two delighters (confetti, shake-to-SOS) | Emotional payoff + accessibility |

### Out of scope (V2)
- Backend persistence (Supabase/Firebase) — current build is front-end only
- Actual SMS delivery to contacts (uses simulated notifications)
- Voice activation, audio recording, panic word
- Family-plan tier with shared dashboard
- Integration with local emergency services (LASEMA, FRSC)

### Success metrics (post-launch)
- **Activation:** % of installs that complete onboarding + add 1+ contact (target: 70%)
- **Daily habit:** # of safe-arrival sessions per user per week (target: 3+)
- **Emergency effectiveness:** % of SOS alerts where contact responded ≤2 min (target: 80%)
- **False-positive rate:** % of SOS cancelled before escalation (target: <15%)

---

## 2 · Architecture

### Stack
- **Frontend:** Vanilla HTML, CSS, JavaScript (no framework)
- **Map:** Leaflet 1.9.4 — embedded inline, no CDN
- **Map tiles:** OpenStreetMap (standard tile.openstreetmap.org)
- **Geolocation:** Browser `navigator.geolocation`
- **Haptics:** Browser `navigator.vibrate`
- **Shake detection:** `DeviceMotionEvent`
- **Deployment:** GitHub Pages (single file)

### File structure
```
lifeline/
├── lifeline-app.html       — full app (single file, ~210 KB)
├── lifeline-wireframes.html — low-fidelity wireframes
└── lifeline-build-docs.md   — this file
```

### Architecture diagram
```
┌─────────────────────────────────────────────────────────────┐
│                    USER PHONE (browser)                     │
│                                                             │
│  ┌────────────┐    ┌────────────┐    ┌─────────────────┐  │
│  │  UI Layer  │    │   State    │    │  Browser APIs   │  │
│  │ 12 screens │◄──►│  (in-mem)  │◄──►│  GPS, Vibrate,  │  │
│  │ Dark navy  │    │  history   │    │  DeviceMotion   │  │
│  └─────┬──────┘    │  selETA    │    └────────┬────────┘  │
│        │           │  tripSecs  │             │           │
│        ▼           │  otpAttmpt │             ▼           │
│  ┌────────────┐    └────────────┘    ┌─────────────────┐  │
│  │  Leaflet   │                       │   OSM Tiles    │  │
│  │ (embedded) │──── HTTP tiles ──────►│  load          │  │
│  │  ~147 KB   │                       │  progressively │  │
│  └────────────┘                       └─────────────────┘  │
└─────────────────────────────────────────────────────────────┘
```

### Network resilience strategy (critical for Nigerian mobile)
| Concern | Solution |
|---|---|
| CDN reliability on MTN/Airtel | **Leaflet JS + CSS embedded inline** — zero external library calls |
| Tile fetch failures | `errorTileUrl` set to transparent 1×1 GIF — failed tiles show clean grey, never broken-image icon |
| Slow tile loading | Tiles load progressively from `tile.openstreetmap.org` — partial map (2-3 tiles) is enough to be useful |
| Leaflet marker images | All Leaflet image assets base64-inlined in CSS — no broken-icon risk |
| GPS unavailable | Falls back to Lagos default coordinates silently; manual entry path via modal |

### Data flow (key flows)

**Safe arrival flow:**
```
User taps "Start safe arrival"
  → Pick destination + ETA (15/30/60 min)
  → Tap "Share with contacts"
    → Location permission requested
      → granted: proceeds to tracking
      → denied: modal opens, user enters manually
  → Live tracking screen loads
    → Leaflet map initialised with current + dest coords
    → Countdown timer starts (decrements 1/sec)
    → Map marker animates from origin to destination
  → User taps "I've arrived safely"
    → Trip closes, confetti animation, contacts notified
  ─── OR ───
  → ETA hits 0:00
    → Overdue banner appears
    → Contacts auto-notified
```

**SOS flow:**
```
User holds SOS button (mousedown/touchstart)
  → 3-second SVG ring fills
  → After 3 seconds: navigator.vibrate([200,100,200])
  → Navigate to SOS Active screen
  → 2:45 countdown starts (165 seconds)
    → "GPS Status: Live · {lat,lng}" shows real coords
    → "Contacts Alerted" message displayed
  → Timer hits 0 → auto-navigate to Contact View screen
  ─── OR ───
  → User taps "I'm safe — cancel"
    → Navigate to Resolved screen
```

---

## 3 · Build & Run

### Quick start (local)
```bash
# Just open the file in any modern browser
open lifeline-app.html
```

### Deploy to GitHub Pages
```bash
cd /path/to/your/lifeline-repo
git init
git add lifeline-app.html
git commit -m "Initial LifeLine build"

# Push to GitHub, then in repo Settings → Pages:
# Source: main branch, root folder
# Your app will be live at:
# https://{your-username}.github.io/{repo-name}/lifeline-app.html

# OR rename to index.html for cleaner URL:
mv lifeline-app.html index.html
git mv lifeline-app.html index.html
git commit -m "Rename to index.html"
git push
```

### Demo cheatsheet (for the pitch)
- **OTP correct code:** `8484` · any other code shows the failure state
- **Demo nav bar (bottom):**
  - 🔑 Onboard — start from splash
  - 🏠 Safe Arrival — jump to home
  - 🚨 SOS — jump straight to active SOS screen
  - ⚠️ Failures — jump to OTP error state
- **Shake your phone** (on a real device) to trigger the shake-to-SOS hint toast
- **SOS button** — press and hold for 3 seconds to activate emergency

### Browser support
- iOS Safari 14+
- Android Chrome 90+
- Desktop Chrome/Firefox/Safari (latest)
- *Internet Explorer not supported (no one uses it on a phone)*

---

## 4 · Manual Test Plan & Results

Tested on Chrome (desktop) and iOS Safari (iPhone 13 mini) on MTN 4G and 3G (forced).

### Test matrix

| ID | Flow | Steps | Expected | Result |
|---|---|---|---|---|
| T01 | Splash → Onboarding | Tap "Get started" | Splash exits, onboarding 1 appears | ✅ PASS |
| T02 | Onboarding navigation | Tap "Continue" twice | Reach OTP screen | ✅ PASS |
| T03 | OTP send | Enter `08123456789`, tap Send | OTP block appears, resend timer starts at 0:48 | ✅ PASS |
| T04 | OTP wrong code | Type `1111` | Error message, attempts decrements, boxes shake red, clear | ✅ PASS |
| T05 | OTP correct code | Type `8484` | Advance to onboarding 2 | ✅ PASS |
| T06 | OTP retry | Wrong code 3x, then `8484` | Each wrong shows error, correct succeeds | ✅ PASS |
| T07 | Contacts screen | Tap "Finish setup" | Land on home screen | ✅ PASS |
| T08 | Home — start arrival | Tap "Start safe arrival" card | Share trip screen loads | ✅ PASS |
| T09 | ETA selection | Tap each ETA button | Only selected has teal border | ✅ PASS |
| T10 | Share trip first time | Tap "Share with contacts" | Location modal slides up | ✅ PASS |
| T11 | Manual location | Tap "Continue with manual" | Modal closes, tracking screen loads | ✅ PASS |
| T12 | Live tracking countdown | Wait 5 seconds | Counter decrements correctly | ✅ PASS |
| T13 | Live tracking map | (on real device with GPS) | Real OSM map shows with marker at GPS coords | ✅ PASS |
| T14 | Map on 3G (throttled) | Force 3G in Chrome devtools | Library loads instantly, tiles load progressively | ✅ PASS |
| T15 | Map with no internet | Disable network | Library loads (embedded), tiles show grey, app still navigates | ✅ PASS |
| T16 | Arrived safely | Tap "I've arrived safely" | Safe screen with confetti animation | ✅ PASS |
| T17 | Confetti delighter | Land on safe screen | 30 confetti pieces fall, varied colours | ✅ PASS |
| T18 | Trip overdue | Set ETA 15, wait 15:01 mins | Overdue banner shows, countdown shows "OVERDUE" red | ✅ PASS |
| T19 | SOS hold-to-activate | Press SOS 1 second, release | Nothing happens, ring resets | ✅ PASS |
| T20 | SOS full hold | Press SOS 3+ seconds | Vibration, navigate to SOS Active | ✅ PASS |
| T21 | SOS escalation timer | Wait on SOS Active | 2:45 ticks down each second | ✅ PASS |
| T22 | SOS auto-escalate | Wait 2:45 full | Auto-navigates to Contact View | ✅ PASS |
| T23 | SOS cancel | Tap "I'm safe — cancel" | Resolved screen, alerts cancelled | ✅ PASS |
| T24 | Contact view map | Land on s11 | Red-tinted OSM map with pulsing marker | ✅ PASS |
| T25 | Shake-to-SOS | (on phone) Shake firmly | Toast appears bottom | ✅ PASS |
| T26 | Demo nav — SOS | Tap 🚨 button | Jump direct to SOS Active | ✅ PASS |
| T27 | Demo nav — Failures | Tap ⚠️ button | Land on OTP with error state visible | ✅ PASS |
| T28 | Back navigation | From any screen, tap ← | Returns to previous | ✅ PASS |
| T29 | Phone field validation | Enter `123`, tap Send | Input shakes red, OTP doesn't show | ✅ PASS |
| T30 | Resend OTP | Tap "Resend" | Timer resets to 0:48 | ✅ PASS |

**Result: 30/30 PASS**

### Known limitations
1. Map tiles still require some internet to render — the embedded *library* is offline-safe, but tiles come from OSM. Mitigation: error tiles fall back gracefully to grey.
2. Shake-to-SOS only triggers a hint toast — full SOS activation still requires the 3-second hold (intentional, prevents false alarms).
3. No persistence — refresh resets all state. V2 will add Supabase like SafeSignal.
4. Test devices were limited to iPhone 13 mini and one Android (Tecno Camon 19). Need broader Android coverage.

---

## 5 · Iteration Log

### Iteration 1 — From design artefact → first build

**What we started with:**
The Figma design artefact had 12 screens documenting the happy path for all 3 flows (onboarding, safe arrival, emergency), but:
- No failure paths defined
- No delighters
- No specification for low-network resilience
- ChatGPT-generated first build used CDN'd Leaflet + had basic styling for screens 7-12

**What changed in Iteration 1:**
1. Self-hosted Leaflet inline (CSS + JS + base64 images) — eliminated CDN dependency
2. Built all 12 screens to design-system specification (Navy + Teal + Mint palette)
3. Implemented real countdown timers (tracking + SOS escalation)
4. Implemented SVG hold-to-activate ring for SOS button
5. Added the demo nav bar for pitch-day flow jumping

**Why:** SafeSignal experience showed CDN failures on MTN are real. We were not going to lose the demo to a tile.openstreetmap.org slowdown.

### Iteration 2 — Failure paths + delighters

**Trigger:** Group review — "this feels too perfect. Real users will hit errors."

**What changed in Iteration 2:**

*Failure paths added:*
1. **OTP wrong code** — Visual shake animation, red error message, attempts counter ("2 attempts left"), input clearing. Resend timer restarts when user taps Resend.
2. **Location permission denied** — Bottom-sheet modal slides up, lets user enter address manually instead of blocking the flow.
3. **Trip overdue** — When the ETA countdown reaches 0:00, the countdown becomes "OVERDUE" in red, and a banner notifies the user that contacts have been auto-alerted.

*Delighters added:*
1. **Confetti on safe arrival** — 30 colourful confetti pieces with randomized colour, size, rotation, and timing. Plays immediately after "✓ I've arrived safely" tap.
2. **Shake-to-SOS hint** — On real devices, shaking the phone triggers a toast showing the SOS hint. (Full SOS activation still requires the deliberate 3-second hold — prevents false alarms from pocket-bumps.)

**Why:** Failure paths build trust — they show the team thought about real users on bad networks with denied permissions. The confetti delighter creates a positive feedback loop that makes safe-arrival the *daily* anchor habit — which is what makes the emergency feature work when it matters.

### Iteration 3 (post-pitch / future) — Backend
- Wire to Supabase like SafeSignal: persist trips, contacts, alerts
- Real SMS via Termii or Africa's Talking
- Tile caching via service worker (truly offline maps)
- Apple Watch / Android Wear companion for SOS without phone

---

## 6 · Vibe-Coding Evidence

This app was vibe-coded across two iterations with the assistance of Claude (Anthropic).

**Process:**
1. Started from design artefact (12 screens in Figma) + ChatGPT scaffold
2. First iteration: Claude rebuilt all screens to design system spec, embedded Leaflet inline, added countdown timers
3. Discovered runtime bugs via headless DOM testing (jsdom) — caught `undefined function` errors that visual inspection missed
4. Second iteration: added 3 failure paths + 2 delighters based on group review
5. 30 manual test cases, all passing

**Prompt patterns used:**
- "Build this design, but make it work on the worst Nigerian mobile networks like you did for SafeSignal"
- "I tested it, it's not working. Plus where are the other artifacts?" *(led to honest reset and full ship)*

**What worked:**
- Embedding Leaflet inline (167KB) — solved the CDN problem definitively
- Demo nav bar at bottom — lets the team show any flow in 1 tap during pitch
- Real OTP failure path with attempts counter — concrete proof we thought about edge cases

**What didn't work first time:**
- Byte-offset surgical editing of HTML to add Leaflet — introduced silent function reference bugs (called `drawSosMap()` after renaming it to `buildSosMap()`). Lesson: when changing structure, rewrite the file as one coherent string, don't splice.
- Initial reliance on substring checks for verification — passed all checks but the app didn't work. Lesson: use actual JS parsing + DOM simulation (jsdom) to validate, not text matching.

---

## 7 · Capstone Rubric Mapping

| Rubric Section | Where it lives |
|---|---|
| Problem & user research | This doc § 1 + Group39 Direction Exploration |
| PRD / requirements | (separate PRD document) |
| Wireframes / low-fi | `lifeline-wireframes.html` |
| Hi-fi design | `LifeLine_Product_Design.pdf` (Figma export) |
| Build / MVP | `lifeline-app.html` (deployed to GitHub Pages) |
| Failure paths | This doc § 5 + interactive in app |
| Delighters | This doc § 5 + interactive in app |
| Manual test plan | This doc § 4 (30 test cases) |
| Iterations (2+) | This doc § 5 |
| Architecture | This doc § 2 |

---

*Built by Group 39 · TS Academy Phoenix Cohort · May 2026*
