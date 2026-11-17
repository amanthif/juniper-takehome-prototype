# Three retention prototypes for a GLP-1 program

**Start here:** https://amanthif.github.io/juniper-takehome-prototype/

| Prototype | Question it answers | Live link |
|---|---|---|
| **Monthly Progress Report** | "Is this working, and is it worth it?" | https://amanthif.github.io/juniper-takehome-prototype/report/ |
| **Non-Scale Victories** | "What's changed that the scale doesn't show?" | https://amanthif.github.io/juniper-takehome-prototype/nsv/ |
| **Pre-emptive Check-In** | "We know something's wrong before she does." | https://amanthif.github.io/juniper-takehome-prototype/check-in/ |

Each prototype opens with demo controls beside a phone, so you can watch it adapt. They work on a real phone too.

> Sarah is a fictional user. All data is illustrative. "Expected range" bands are illustrative curves, not clinical data. June's replies are scripted, not a live model.

## The thinking behind them

**"I'm not seeing results" is really two problems:**

|  | **Feels like progress** | **Doesn't feel like progress** |
|---|---|---|
| **Objectively progressing** | Healthy | **Perception gap** (value problem: make it felt) |
| **Objectively stalled** | **Hidden risk** (feels fine, but stalled) | **True stall** (results problem: route to care) |

Non-Scale Victories and the Monthly Report make real progress visible. The Pre-emptive Check-In catches hidden risk and true stalls early and routes them to a human.

**Design principles across all three**
- **Never lead with a flat weight graph, but never falsely reassure.** Stalled users are routed to care, not cheered on.
- **Reward the process, not the outcome.** Streaks and progress bars track the behaviours that drive results: dose steps on schedule, side effects managed, weekly weigh-ins (with a forgiving streak freeze). No points for kilos, no leaderboards.
- **Infer before you ask.** No user has zero data. Intake, prescription and orders always give something real. Things learned in chat are reused, with a transparency line ("Based on what you told June…").
- **Every piece of data is paid back.** Any input instantly changes something the user can see.
- **June never diagnoses.** She surfaces likely factors and hands off to a prescriber or coach, who already has the answers.

## Prototype: Monthly Progress Report (`/report/`)

A monthly moment, a few days before renewal, told as a six-page story she taps through: the answer, one question, last month and this month, why, a signed note from her care team, and "Is it worth it for you right now?". Use the toggles on the left to change how much data we have, the stage and how she's progressing.

## Prototype: Non-Scale Victories (`/nsv/`)

The same data the app already collects, shown back as progress. The Today screen leads with one real win at a time, and weight sits in context, one tap away. Use the toggles on the left to change the case, the stage and what she logs.

## Prototype: Pre-emptive Check-In (`/check-in/`)

We notice something is off before she does, and June reaches out. The left side shows the signals building week by week; the phone shows what she sees. In the chat she can tap to answer, or hold the button and say it in her own words. Scenarios: stalled but feels fine, gone quiet, and doing everything right but not responding.

## How I built it with AI

Built with Claude Code from a written brief. I wrote the product thinking, the states and the guardrails; the AI wrote most of the code. I reviewed every screen in a browser at each state and pushed back where it drifted.

**Where I overrode the AI**
- **Softened "everything is a value problem".** The early framing treated all "not seeing results" churn as perception. It isn't: some users are genuinely stalled and need clinical care. That's why there are two paths.
- **Challenged a "5% non-responder" figure.** It had no source I could stand behind, so my written answers cite the trial data instead. The prototypes avoid inventing clinical stats: bands are labelled illustrative.
- **Dropped a fake-door test.** A fake "talk to a prescriber" button is a bad trade in a health context. Users who tap it need a real response.
- **Added the "reward the process, not the outcome" guardrail.** Early ideas included points for weight lost. Rewarding kilos punishes plateaus and encourages unhealthy behaviour, so streaks only track actions.

## Tech

- Static HTML/CSS/JS, one file per prototype, no build step and no backend, served by GitHub Pages.
- Mobile-first. Shown in a phone frame on desktop, full-screen on a real phone.
- Accessible: real buttons, 44px touch targets, visible focus, live regions for chat, reduced-motion support.
- **June is scripted.** A live-LLM version is possible, but it would need a **server-side proxy** so no API key ever ships to the browser. There is deliberately no key in this repo.

## Run locally

```bash
python3 -m http.server 8080
```

Then open http://localhost:8080.
