# Simulation Engine

Football Sim uses a play-by-play simulation engine that resolves every snap through multi-phase pipelines. Every player rating directly affects outcomes — there are no decorative stats.

---

## Pass Engine (5 Phases)

Each pass play flows through these phases in order:

1. **Protection** — Offensive line blocking ratings vs. defensive line pass rush. Determines the pocket time window (clean, pressured, collapsing, sacked).
2. **Separation** — Receiver route running vs. cornerback/safety coverage. Creates coverage windows (wide open, open, contested, blanketed) for each eligible receiver.
3. **Decision** — QB processing and awareness evaluate coverage windows. Selects a target based on read progressions, tendencies, and pressure state. Under pressure, decision quality degrades.
4. **Throw** — QB accuracy rating determines ball placement within the coverage window. Arm strength affects deep ball velocity and trajectory.
5. **Catch** — Receiver hands rating vs. defender ball skills. Contested catches factor in both. Interception probability scales with defender ball skills and coverage tightness.

## Run Engine (5 Phases)

1. **Blocking** — Offensive line run blocking vs. defensive line power. Creates initial lanes (wide, narrow, stuffed).
2. **Vision** — RB vision rating determines lane selection quality.
3. **Engagement** — First contact point. RB meets defender.
4. **Contact** — **Power OR Elusiveness** (not blended). The engine picks whichever trait is more relevant to the run type. Power backs break through; elusive backs avoid.
5. **Breakaway** — Speed only triggers in open-field situations. A slow power back can still dominate through contact; speed matters when there's daylight.

## Key Design Rules

- **Every rating affects simulation.** No decorative stats. If a rating exists, it's wired into play outcomes.
- **Ratings are position-specific.** QBs have arm strength and processing; WRs have route running and hands; CBs have man coverage and ball skills. No shared generic ratings.
- **Safety Range = Speed * 0.6 + Awareness * 0.4** (hidden formula, never exposed in UI).
- **Run contact uses Power OR Elusiveness**, never both. The run type and game state determine which matters.
- **Speed only triggers in open-field breakaway.** A 99-speed RB still gets stuffed at the line if blocking fails.

## Calibration

The engine has been calibrated against real NFL statistical ranges and is **frozen** — no play-resolution tuning is applied after calibration. Key benchmarks:

- Red zone TD rate: ~68-69% (NFL average)
- Passing/rushing yard distributions within realistic bounds
- Validated via a 10-season stress test (zero bugs, 14/14 tests pass)

## Talent Compression

A compression factor (0.62x) reduces the raw talent gap between teams. This prevents elite rosters from going undefeated while ensuring bottom-feeders can occasionally win — just like the NFL. Strategy (gameplans, play-calling, depth chart management) fills the gap that raw talent doesn't.

## Playbook Fit Scoring

Each play in your playbook is scored against your roster's ratings at the relevant positions. A ±15% impact modifier means running a play that fits your personnel gives a meaningful edge, while forcing a scheme that doesn't fit your players is a real penalty.
