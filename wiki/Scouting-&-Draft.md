# Scouting & Draft

Football Sim features a confidence-based scouting system with a pre-rolled 18-week college football season. You're not just clicking a "scout" button — you're making strategic decisions about where to invest your attention, and the intel drips in over time.

---

## The College Season

When a new draft class is created, the game pre-rolls an entire 18-week college football season:

- **50 schools** across **5 conferences**
- ~300 prospects distributed by school quality (top programs get more/better players)
- Standings, stat leaders, weekly headlines, and Top 25 rankings
- One college week is revealed per NFL week, so you're watching the college season unfold alongside your own

## 4-Stage Scouting Pipeline

Each stage has a deadline. Miss it, and defaults are applied automatically (AI teams always make their picks on time).

### Stage 1: School Scouting
**When:** Offseason through Week 1
**What you do:** Choose between "Powerhouse" schools (proven programs) or "Dark Horse" schools (hidden gems)
**Intel delivery:** Drips from Week 1 through Week 10

### Stage 2: Position Scouting
**When:** Weeks 1-10, locked at Week 11
**What you do:** Allocate percentages across 10 positions (QB, RB, WR, TE, OL, DL, LB, DB, K, P). Preset templates available.
**Intel delivery:** Drips from Week 11 through Week 18

### Stage 3: Targeted Scouting
**When:** Weeks 11-18, locked at Wild Card
**What you do:** Pick up to 5 specific schools to deep-scout
**Intel delivery:** Drips from Wild Card through Conference Championship

### Stage 4: Interviews
**When:** Playoffs through Offseason Week 1
**What you do:** Select up to 10 individual prospects for interviews
**Intel delivery:** Immediate. This is the **only** way to reveal a prospect's development trait and character flags.

## Confidence System

Every prospect has a confidence score from 0-100% per team. Higher confidence means:

| Confidence | OVR Range | Strengths/Weaknesses | Potential Tier |
|-----------|-----------|---------------------|---------------|
| 0% | 54-point spread | 1 strength, 0 weaknesses | Inaccurate |
| 50% | ~27-point spread | 2-3 strengths, 1-2 weaknesses | Close |
| 100% | 2-point spread | 4 strengths, 3 weaknesses | Accurate |

**Diminishing returns** prevent over-investing: `effectiveGain = rawGain * (1 - current * 0.3)`. Early scouting is cheap; squeezing out the last 10% is expensive.

## Draft Board

Before the draft, you rank prospects on your personal draft board:
- Browse by position with filter chips
- Sort by confidence, projected OVR range, or position
- View team needs alongside prospect ratings
- Confidence % and OVR range midpoint replace traditional scout grades

## Draft Room

The draft itself is a multi-round event:
- Pick-by-pick resolution with the current pick highlighted
- **Make your pick** when it's your turn
- **Sim one pick** to advance past the next CPU selection
- **Advance to my pick** to skip ahead automatically
- **Sim entire draft** to auto-complete
- Drafted players immediately join your roster

## After the Draft

All prospects convert to full Player objects with their true ratings revealed. The gap between what you scouted and reality is where the drama lives — a high-confidence pick should be close to what you expected, but a low-confidence gamble could be a steal or a bust.
