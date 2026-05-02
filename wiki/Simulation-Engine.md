# Simulation Engine

Football Sim resolves every snap through explicit phase pipelines. Player ratings are not cosmetic here. If a rating exists, it is wired into outcomes.

---

## Pass Engine (6 Phases)

1. **Protection** - Offensive line blocking vs defensive line pass rush.
2. **Separation** - Route running vs coverage creates the target window.
3. **Decision** - QB processing and pressure handling choose the read.
4. **Throw** - Accuracy and arm strength shape the ball.
5. **Catch** - Hands, ball skills, and contested catch logic decide the result.
6. **YAC** - Yards after the catch use receiver YAC vs tackle and pursuit quality.

The public-facing takeaway is simple: pass plays now have a separate YAC phase, so a completion is not the end of the story.

## Run Engine (5 Phases)

1. **Blocking** - OL run blocking vs defensive front resistance.
2. **Vision** - RB vision chooses the lane.
3. **Engagement** - First contact at the line or in the hole.
4. **Contact** - Power or elusiveness matters depending on the run, not both at once.
5. **Breakaway** - Speed matters only once the runner has daylight.

## Key Rules

- Ratings are position-specific.
- Safety range is hidden and derived from speed plus awareness.
- Run contact uses power or elusiveness, never a blended average.
- Speed only becomes decisive in open-field breakaway situations.
- Talent compression keeps the league competitive instead of letting one roster run away with every season.

## Calibration

The engine is tuned against NFL-caliber ranges and then treated as locked. That includes validation against long stress-test runs so changes do not quietly drift the game away from football-shaped results.

## Playbook Fit

Playbook fit feeds both call frequency and execution strength.

- A better fit makes a play type more likely to be called.
- A better fit also gives the play a real success bonus.
- A bad fit can suppress both selection and execution.

See also: [[Playbook Fit]]
