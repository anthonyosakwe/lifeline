# LifeLine — Decision Log v2 (FINAL)

<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="assets/lifeline-logo-dark.png">
    <source media="(prefers-color-scheme: light)" srcset="assets/lifeline-logo-light.jpg">
    <img src="assets/lifeline-logo-dark.png" alt="LifeLine logo: navy shield with red location pin" width="200">
  </picture>
</p>

**Personal Safety & Check-In · Safety in one tap**
**Group 39 · Phoenix Cohort · TS Academy PM Capstone**
**Document version:** 2.0 (FINAL — supersedes v1)
**Last updated:** 22 May 2026 · **Owner:** Group 39 Ops squad

---

## Purpose

This log captures every meaningful team decision made during the LifeLine capstone build, with full context: who proposed it, what was considered, why we chose what we chose, and which deliverables it affects. Decisions are not relitigated unless new evidence appears.

## Methodology

Per our decision rules (D-03): sync decisions need majority of those present; async decisions need ≥4 explicit "agree" responses in WhatsApp within 12 hours, or default to the proposer's call. Faith has hard veto on new features after Day 14. Tony has hard veto on architecture changes after Day 18.

---

## Decision log

### D-01 — Team structure: 5-team model

| Field | Detail |
|---|---|
| **Date** | 2 May 2026 |
| **Proposed by** | Faith |
| **Approved by** | Sync majority |
| **Status** | ✅ Active |
| **Context** | Faith initially proposed 4 teams. Review showed Roadmap and Metrics deliverables belonged to Product Management, not Design or Research. |
| **Options considered** | (a) Stick with 4 teams · (b) Move to 5 teams · (c) Move to 3 large teams |
| **Chosen option** | 5 teams with cross-contribution allowed |
| **Reasoning** | Aligns with capstone rubric ownership; lets each team focus; cross-contribution allowed for slack capacity |
| **Affects deliverables** | 1 (One-Pager) · 2 (Discovery) · 3 (PRD) · 4 (Design Pack) · 5 (Build) · 6 (Metrics) · 7 (GTM) · 8 (Roadmap & Team Execution) · 9 (Pitch Deck) |

### D-02 — Collaboration tool: Notion + Google Drive hybrid

| Field | Detail |
|---|---|
| **Date** | 6 May 2026 |
| **Proposed by** | Anthony Osakwe (Osanthon / Tony) |
| **Approved by** | Sync majority |
| **Status** | ✅ Active |
| **Context** | Team needed a single source of truth with authorship visibility and structure protection. |
| **Options considered** | (a) Notion only · (b) Google Docs only · (c) Hybrid · (d) Coda |
| **Chosen option** | Hybrid — Google Docs (Suggesting mode) for documents, Notion for sprint board, decision log, dashboard |
| **Reasoning** | Most members new to Notion; reduces learning curve; keeps document writing experience familiar; Notion's database superpowers used only where they matter |
| **Affects deliverables** | 8 (Roadmap & Team Execution) · all processes |

### D-03 — Decision rules: Sync / Async / Veto framework

| Field | Detail |
|---|---|
| **Date** | 7 May 2026 |
| **Proposed by** | Anthony Osakwe (Osanthon / Tony) |
| **Approved by** | Sync majority |
| **Status** | ✅ Active |
| **Context** | Team needed structured rules to ensure constant progress on deliverables without chaos or random brainstorming. A suggestion for formal meeting rules was put up by Tony. |
| **Options considered** | (a) No formal rules (default proposer call) · (b) Strict sync-only · (c) Hybrid sync + async with vetoes |
| **Chosen option** | **SYNC:** Simple majority of those present. **ASYNC:** 4 or more explicit "agree" responses in WhatsApp within 12 hours, or it defaults to the proposer's call. **LOG:** Every decision lives in the Decision Log inside the Master Folder. **VETO-PM:** Faith has a hard veto on any new feature added after Day 14. **VETO-BUILD:** Tony has a hard veto on architecture changes after Day 18. |
| **Reasoning** | Encourages quick and organised sync flows while protecting against silent over-commitment and late-stage scope creep |
| **Affects deliverables** | All deliverables · all processes |

### D-04 — Meeting passivity and silent members

| Field | Detail |
|---|---|
| **Date** | 8 May 2026 |
| **Proposed by** | Group members (post-Chimdinma meeting) |
| **Approved by** | Sync consensus |
| **Status** | ✅ Active |
| **Context** | The rules on how to handle silent / non-responsive members needed to be outlined to protect active members' workload and morale. |
| **Options considered** | (a) Tolerate silence (no action) · (b) Private follow-up only · (c) Public reassignment after warnings |
| **Chosen option** | Following first-day notice of inactivity, passive members are sidelined from their squad's critical path. Their role is reassigned without drama. Re-entry possible if they engage proactively within 48 hours. |
| **Reasoning** | Protects momentum; rewards engagement; avoids carrying inactive members across deadlines |
| **Affects deliverables** | All deliverables · all processes |

---

### D-05 — Product name and identity locked

| Field | Detail |
|---|---|
| **Date** | 21 May 2026 |
| **Proposed by** | Anthony Osakwe (Osanthon / Tony) |
| **Approved by** | Sync majority |
| **Status** | ✅ Active |
| **Context** | The PRD originally listed three candidate names (Beacon / Lifeline / Watchlink). To prevent brand drift across deliverables, one name needed to be locked across PRD, One-Pager, Build Doc, Metrics, README, and Pitch Deck. |
| **Options considered** | (a) Beacon · (b) Lifeline · (c) Watchlink · (d) Continue with placeholder |
| **Chosen option** | **LifeLine** (single-word brand, capitalised L's). Tagline: *"Safety in one tap."* Descriptor: *"Personal Safety & Check-In."* |
| **Reasoning** | Strongest emotional resonance with the safety mission; tagline tests well; descriptor accurately captures both flows (safe-arrival check-in + SOS); already adopted in design pack and demo app |
| **Affects deliverables** | All deliverables |

### D-06 — Primary persona narrowed to female campus student

| Field | Detail |
|---|---|
| **Date** | 21 May 2026 |
| **Proposed by** | Anthony Osakwe (Osanthon / Tony) |
| **Approved by** | Sync majority |
| **Status** | ✅ Active |
| **Context** | The PRD listed 7 user segments. Capstone rubric rewards a single sharp persona, not a broad audience. Discovery data (6 interviews) included examples across multiple segments, but the wireframe persona (Ada Umeh) is a student. |
| **Options considered** | (a) Campus female student · (b) NYSC corper · (c) Young urban professional women, broadly · (d) Multi-persona generic |
| **Chosen option** | **Campus female student** (Ada Umeh, 20, 300-level Biochemistry, UNN). Other 6 segments listed as "Future personas for V2+ expansion." |
| **Reasoning** | Sharpest framing for rubric; matches our existing wireframe persona; strongest demo story; validated by Amaka O. (student) in discovery; clean expansion path documented in PRD §5.2 |
| **Affects deliverables** | 1 (One-Pager) · 3 (PRD) · 7 (GTM) · 9 (Pitch Deck) |

### D-07 — Roadmap structure: Two separate roadmaps (Product + Architectural)

| Field | Detail |
|---|---|
| **Date** | 22 May 2026 |
| **Proposed by** | Anthony Osakwe (Osanthon / Tony) |
| **Approved by** | Sync majority |
| **Status** | ✅ Active |
| **Context** | The team had multiple roadmap artifacts (Gantt HTML, PRD section, README), with timelines that didn't match. Risk: judges would spot the inconsistency. Discussion clarified Product Roadmap (user value over time) and Architectural Roadmap (technical capability over time) are two different artifacts — not interchangeable. |
| **Options considered** | (a) Update gantt to match PRD timeline · (b) Update PRD/README to match gantt's slower timeline · (c) Keep both — gantt becomes Architectural-only; add a separate Product Roadmap view |
| **Chosen option** | **Option C** — Two separate roadmaps. The interactive HTML keeps the gantt as the Architectural Roadmap (technical capability layers) and adds a new tab for the Product Roadmap (V2/V3/V4/V5 user-visible milestones from PRD §17.1). |
| **Reasoning** | Most rigorous PM answer; matches the canonical distinction taught in PM literature; demonstrates the team understands the difference; preserves work already done; earns Team Process points by showing mature thinking |
| **Affects deliverables** | 3 (PRD) · 8 (Roadmap) · 9 (Pitch Deck) · 11c (Roadmap HTML) |

### D-08 — Pitch deck format: PPTX

| Field | Detail |
|---|---|
| **Date** | 22 May 2026 |
| **Proposed by** | Anthony Osakwe (Osanthon / Tony) |
| **Approved by** | Sync majority |
| **Status** | ✅ Active |
| **Context** | Pitch deck could be delivered as a Word doc (content for layout later) or as PPTX (presentable directly). Format affects both delivery flexibility and rubric perception. |
| **Options considered** | (a) PPTX (presentable from day one) · (b) Word (content for GTM team to lay out in Canva/Slides) |
| **Chosen option** | **PPTX** with LifeLine brand palette (Navy / Teal / Mint / Red / Green) and Helvetica typography. Imports cleanly to Google Slides as backup. |
| **Reasoning** | Single-source-of-truth deck; presentable from day one with no extra layout work; consistent brand experience; allows speaker notes per slide for the presenter |
| **Affects deliverables** | 9 (Pitch Deck) |

---

## Decisions affecting code/assets (for reference)

These were design and engineering decisions made during the build, captured here for completeness even though they didn't go through the formal sync/async process.

- **Demo OTP code = 8484** (any other code triggers the failure path) — chosen for memorability during pitch day
- **3-second SOS hold-to-activate** — prevents pocket-bump false alarms while remaining one-handed-operable under stress
- **2:45 SOS escalation timer** — long enough to cancel an accidental trigger, short enough to feel urgent
- **Leaflet 1.9.4 embedded inline (no CDN)** — eliminates CDN failure risk on Nigerian mobile networks (lesson from SafeSignal)
- **OpenStreetMap tiles** (not Google Maps) — free, no API key, works progressively on slow networks
- **Single-file HTML deployment** — works on any static host (GitHub Pages, Netlify, Vercel); no build step
- **Pattern 2A two-flow design** — Safe Arrival (daily habit driver) + SOS (high-stakes safety net), each with its own happy/failure paths

---

## Removed (corrupted entries from v1)

Five rows in the original Decision Log v1 contained corrupted text (likely accidental keyboard input): `Gdbd`, `Bdbjdd`, `Gdhhd`, `Gdhgd`, `Gdgggd`. All five had no Date, Proposed by, Context, Options, or Reasoning fields populated. They have been removed in v2 as they contained no usable decision data.

---

## How to use this log

- **Before proposing a new decision:** check this log first to ensure it doesn't conflict with an active prior decision
- **When a decision is made:** the proposer adds a new D-## entry immediately; status defaults to "Active"
- **When a decision is reversed:** mark the original entry as "Superseded by D-XX" and create a new entry; do not delete history
- **Reviewers:** every decision in the "Affects deliverables" column should be cross-checked against that deliverable's current state at submission

---

*Document v2.0 · 22 May 2026 · Owner: Group 39 Ops squad · Reviewed by: full team*
