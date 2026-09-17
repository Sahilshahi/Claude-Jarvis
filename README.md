# Claude Jarvis

A personal AI assistant that tracks revenue, handles email, publishes
content, and tells you what to focus on every morning — with a mission
control screen you talk to out loud, backed by three agents: a **Scout**
that gathers intelligence, an **Operator** that does the work, and an
**Advisor** that tells you what actually matters.

## What's here

- `mission-control/index.html` — the JARVIS HUD dashboard. Self-contained
  (HTML/CSS/JS inline, no build step, no dependencies). Open it directly in
  a browser.
- `agents/scout.md`, `agents/operator.md`, `agents/advisor.md` — the routine
  prompts for each agent, meant to be set up as Claude routines against your
  real connectors (Gmail, Buffer, RevenueCat, Meta Ads, Claude in Chrome).
- `faq.md` — the Operator's knowledge base. Fill this in with your real
  customer questions and answers before turning the Operator loose on email.

## Running the dashboard

```
open mission-control/index.html
```

or serve it locally:

```
npx http-server mission-control
```

Click the orb (or hold Space) to talk to it using your browser's speech
recognition; it answers both on-screen and out loud via speech synthesis.
The **MORNING BRIEF** button plays a spoken summary plus the Advisor's top 3
recommendations. There's a text input at the bottom as a fallback when voice
isn't available.

All numbers on the dashboard come from one object, `JARVIS_DATA`, at the top
of the `<script>` in `index.html`. It's mock data today — wire it up to real
data by replacing those fields (or by having a Scout/Advisor routine write
into it) without touching any of the layout or animation code.

## Build order

1. **Mission control**, even on fake data — a system you can see is a system
   you keep using.
2. **Scout** — read-only, can't break anything, safest place to learn how
   routines behave.
3. **Operator** — watch everything it drafts for a week before letting it
   send anything on its own.
4. **Advisor** — once the Scout has enough history to reason about.
5. Wire mission control to real data, field by field.

## Safety rules

- Nothing sends, spends, or publishes without you until it's earned that —
  drafts first, always.
- Every number carries its source and date; anything unverifiable is labeled
  `UNAVAILABLE` rather than estimated.
- `faq.md` is the boundary: if the answer isn't in it, the Operator
  escalates instead of improvising, and you add the line afterward.
- Read the Advisor's recommendations even on days you do nothing with them.
