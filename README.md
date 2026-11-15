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

A monthly moment, a few days before renewal. It opens from a notification into a scrolling report with the standard structure used by health apps (headline → this month vs last → where you are → what you did → what changed → what's next).

- **A different report for each phase,** because the question in her head changes:
  - **Start (month 1), "Is this normal?"** Treatment progress and what's typical on the starter dose come before weight.
  - **Middle (month 3), "Is it working?"** Weight against the expected range leads, then what's driving it.
  - **Plateau (month 6), "Is it still worth it?"** What she has kept and her health markers lead, and a flat month is never shown as slowing. No fear of regain.
- **The full-data report uses the data to explain, not just report:** an insight that connects her logs (protein, snacking, nausea), blood markers against her baseline, and her own reflections then and now.
- **Scales down by data level.** Rich: weekly weigh-ins, side-effect log, wearable, a personal insight. Light: 2 weigh-ins and June chats, plus one ask to unlock more. None: a real report from orders and prescription only, with benchmarks clearly labelled "people at your stage".
- **What you did:** the three hypothesised retention drivers as progress bars and streaks: reaching the effective dose, side effects managed, weekly weigh-ins.
- **Your 30 seconds:** 3 taps that update the headline, "What you did" and "What changed" straight away, then a list of exactly what the answers changed.
- **The flywheel:** "Next month" shows that answering this month makes next month's report richer (None → Light → Rich). Skipping it keeps the report the same.
- **Success measures, built in:** "Was this useful?" and "Is treatment worth it for you right now?". "Not sure" or "No" offers a conversation with the care team.
- **Three segments, three jobs:** on track shows progress, behind but feeling fine gets a calm early warning with a review offered, and stalled gets plain facts and the get-help flow.
- **Honesty guardrail:** below range after month 1, the phase framing is dropped. The headline says so plainly and offers **Get help now**. Concern is also raised from her own answers (weight up, side effects most days, appetite unchanged).
- **Get help flow:** a 3-step sheet inside the report. (1) What we can already see, so she doesn't have to explain it, plus two taps: what's getting in the way and how she feels. (2) Who can help, with the best fit recommended (prescriber for side effects or dose, coach for missed doses, support team for cost) and a red-flag line for urgent symptoms. (3) What they'll see, when they'll reply, and what to do in the meantime. It also opens from "Not sure" or "No" on the worth-it question.

## Prototype: Non-Scale Victories (`/nsv/`)

The same data the app already collects, shown back as progress. The Today screen leads with one real win at a time, and weight sits in context, one tap away. Use the toggles on the left to change the case, the stage and what she logs.

## Prototype: Pre-emptive Check-In (`/check-in/`)

Users who are quietly stalling rarely ask for help. They feel fine until the day they decide "it's not working" and cancel. This acts on early signals instead.

- **The system's view:** press play to watch Sarah's weeks. Small signals appear, none alarming alone. Together they cross a threshold, weeks before she'd likely cancel.
- **Sarah's view:** an ordinary week, then a gentle notification from June.
- **Tap to answer, or hold to talk.** One button in the chat. A tap gives quick answer buttons. Holding it lets her say it in her own words, and one sentence can answer everything June needs.
- **"Here's what I heard":** June shows what she picked up as chips. Sarah removes anything that's wrong before it's saved, and June asks only for what's still missing. Her own words go to the care team with the case.
- **Routing and closing the loop:** one tap sends a pre-drafted case to a prescriber or coach. The next day they reply and the treatment tracker updates.

Scenarios:
- **Stalled, feels fine:** she logs everything and feels good, but she's below the expected range and still on the starter dose. June leads with what's going well, then the gap.
- **Gone quiet:** she's stopped logging, so there's nothing to see. June doesn't list what she hasn't done: "No need to log anything. How's it going?" What she says sorts her into one of three paths: fine and busy (a win is added to her home screen), avoiding the scale (weigh-in reminders paused, no weigh-in needed), or struggling (prescriber review).
- **Doing it all, not responding:** a true stall at full dose, which goes to a prescriber.

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
