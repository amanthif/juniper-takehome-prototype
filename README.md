# Monthly Progress Report: a working prototype

**Live prototype:** _add GitHub Pages link here_ · **Written answers:** _add Notion link here_

A clickable, adaptive prototype for a GLP-1 weight-loss subscription. It covers three take-home prompts as **one patient journey**, because to the patient they are one journey:

1. **Monthly Progress Report** (home): *"Is this working, and is it worth it?"*
2. **Non-Scale Victories**: *"What's changed that the scale doesn't show?"*
3. **Proactive Check-In with June**: *"Why am I stuck, and who can help?"*, plus a **prescriber summary** that hands a human clinician the context before they ask.

> Sarah is a fictional patient. All data is illustrative. "Typical range" bands are illustrative curves, not clinical data. June's replies are scripted, not a live model.

## How to demo it (2 minutes)

The panel beside the phone is the point. Flip the switches and watch the report rewrite itself:

| Switch | What changes |
|---|---|
| **Data: Rich / Light / None** | Rich shows the full report. Light shows the core report plus *one* ask ("add a waist measurement to unlock your wins"). None means only intake, prescription and orders: benchmarks are labelled "people at your stage…", and a **30-second check-in inside the report** personalises it as soon as it's answered. That's the moment the data gets paid back. |
| **Stage: Early / Middle / Plateau** | The headline and the *lead visual* change: dose-step timeline (early), you vs the typical-range band (middle), non-scale wins (plateau). |
| **Progress: On track / Below range** | Below range never gets false reassurance. The tone shifts, the dose journey shows "paused", and the report leads to **Check in with June**. |

Suggested path: *Middle + On track* (the happy path) → flip to *Below range* → **Check in with June** → answer "Nausea most days" → **Ask a prescriber to review** → **See what your prescriber sees**. Then try *Data: None* and do the 30-second check-in.

## The thinking behind it

**"I'm not seeing results" is really two problems:**

|  | **Feels like progress** | **Doesn't feel like progress** |
|---|---|---|
| **Objectively progressing** | Healthy | **Perception gap** (value problem: make it felt) |
| **Objectively stalled** | **Hidden risk** (feels fine, but stalled) | **True stall** (results problem: route to care) |

The report handles the value problem (making real progress visible). The check-in handles the results problem (finding the cause and routing to a human). The demo panel labels which quadrant and persona each state represents.

**Design principles in the build**
- **Never lead with a flat weight graph, but never falsely reassure.** The weight chart only appears once real loss is recorded, and it's a drill-down outside month 3. Stalled patients are routed to care, not cheered on.
- **Reward the process, not the outcome.** Streaks and countdowns track behaviours that drive results and retention: dose steps on schedule, orders on time, weekly weigh-ins (with a forgiving streak freeze). No points for kilos, no leaderboards.
- **Infer before you ask.** No patient has zero data. Intake, prescription and order history drive the "None" report. Things June learned in chat are reused, with a transparency line ("Based on what you told June…").
- **Every piece of data is paid back.** Adding a measure instantly unlocks something visible. The data becomes a flywheel, not a form.
- **June never diagnoses.** She surfaces *likely factors*, labels them Prescriber or Coach, and hands off with one tap. The prescriber sees the answers, so the patient never repeats themselves.
- **Patient control.** Progress photos are opt-in and blurred until tapped. Weight numbers can be hidden everywhere.

## Screens

| Screen | What it shows |
|---|---|
| Monthly report | Stage-aware headline · lead visual · check-in prompt (if below range) · countdowns ("9 days to your next dose step", "2.4kg to your first 10%") · process streaks · "Your why" (progress on the reasons given at intake) · coach note (AI-drafted, coach-approved) |
| Your wins | Then-vs-now cards: food noise, evening snacking, nausea days/week, waist, sleep, blood pressure in plain English, private photos. Only cards with enough data show. The rest are one-tap "Add this". |
| June check-in | Conversational, 6 tap-to-answer questions (doses, side effects, appetite, protein, other meds, how you feel). Ends with **Here's what we found** and routing to a prescriber review and/or a coach plan. |
| Prescriber summary | Flags with severity, patient-reported answers, record data, and *suggested for consideration* prompts (not orders). |

## How I built it with AI

Built with Claude Code from a written brief. I wrote the product thinking, the states and the guardrails; the AI wrote most of the code. I reviewed every screen in a browser at each state and pushed back where it drifted.

**Where I overrode the AI**
- **Softened "everything is a value problem".** The early framing treated all "not seeing results" churn as perception. It isn't: some patients are genuinely stalled and need clinical care. That's why the prototype has two paths.
- **Challenged a "5% non-responder" figure.** It had no source I could stand behind, so I used the 9–15% range from trial data in my written answers. The prototype itself avoids inventing clinical stats: bands are labelled illustrative.
- **Dropped a fake-door test.** A fake "talk to a prescriber" button is a bad trade in a health context. Patients who tap it need a real response.
- **Added the "reward the process, not the outcome" guardrail.** Early ideas included points for weight lost. Rewarding kilos punishes plateaus and encourages unhealthy behaviour, so streaks only track actions.

## Prototype: Non-Scale Victories (`/nsv/`)

A standalone redesign of the in-app **Progress tab**. Today the app defines a "win" as kilos ("2.8kg away from your next win"), so a plateau means weeks with nothing to celebrate. Here, **a win is anything that changed**.

- **Hero carousel:** on a good week the weight leads and a non-scale win sits one swipe away. On a flat or up week, a non-scale win leads and the weight follows with context ("Weight drops in steps, not a straight line").
- **Since you started:** then-vs-now cards (food noise, evening snacking, nausea, waist, sleep, energy, blood pressure, clothes fit, doses on time). Tap a card for its monthly trend, where the data came from, and what's helping.
- **Weight, with context:** current weight, 8-week trend and a calm explanation. Weight numbers can be hidden.
- **What's changed?** A 3-tap check-in compared with intake answers. The answers instantly become new or updated win cards.
- **Habits → wins:** each habit links to the outcome it drives ("Protein 5/7 days → evening snacking down to 1–2 a week").
- **Honesty guardrail:** below range *and* flat or up after month 1 → the hero stops celebrating and routes to the care team (the Proactive Check-In prototype).
- **No data:** the first win is a process win inferred from orders ("10 weeks in, every dose on time").

Demo controls: this week's weigh-in (down / flat / up), stage, data level, overall progress.

## Tech

- One static `index.html` (plain HTML/CSS/JS, no build step, no backend) served by GitHub Pages.
- Mobile-first. Shown in a phone frame on desktop, full-screen on a real phone.
- Accessible: real buttons, 44px touch targets, visible focus, live regions for chat, reduced-motion support.
- **June is scripted** (branching responses). A live-LLM version is possible, but it would need a **server-side proxy** so no API key ever ships to the browser. There is deliberately no key in this repo.

## Run locally

```bash
python3 -m http.server 8080
```

Then open http://localhost:8080.
