Finding a profitable trading strategy is not the hard part. The hard part is sticking to it.

Every trader eventually discovers that following a strategy through real gains and real drawdowns is psychologically different from backtesting it. A system that returned 40% last year means nothing if the trader panicked and exited at the worst drawdown, or sized down at exactly the wrong moment. The strategy was fine; the mismatch between the strategy's personality and the trader's personality was not.

The idea is to use ML to match a trading algorithm to a trader's emotional and psychological profile — the same way dating apps match people based on compatibility, not just attractiveness.

**The mismatch problem:**

- A trader who checks their portfolio once a week and can't stomach more than 2% peak-to-trough drawdown will abandon a mean-reversion strategy that regularly dips 8% before recovering, even if it ends the year up 25%.
- A trader who wants 60%+ annual upside and is psychologically prepared for 40% drawdowns will find a "safe" 5%-per-year dividend strategy unbearably boring and will start overriding it.
- Neither trader is wrong. The strategy-trader fit is wrong.

**What the system does:**

1. **Profile the trader** — not just stated risk tolerance (which people consistently misreport), but revealed preferences: How do they react when the position is down 5%? Do they increase size or reduce? How many trades per week feels right? What would cause them to abandon the strategy entirely? Questionnaires + simulated paper trading scenarios.

2. **Characterize strategies along psychological dimensions** — not just Sharpe ratio and CAGR, but: maximum consecutive losing days, average drawdown duration, required decision frequency, emotional variance (calm steady grind vs. volatile spike-and-recover), dependence on rare large wins vs. frequent small gains.

3. **Match** — find the strategy whose psychological fingerprint best fits the trader's profile. A trader who needs frequent feedback needs a strategy with many small wins. A trader who can sit through long flat periods can run trend-following.

**Example trader profiles:**

- **Conservative/passive**: trades once a week, cannot handle more than 2% peak-to-trough drawdown, satisfied with 5% annual return. Match: low-volatility dividend capture, covered calls, or short-duration bond strategies.
- **Aggressive/growth**: accepts 40% drawdown if the realistic upside is 60%+ annually. Match: momentum, concentrated equity, or long-dated options on high-growth names.
- **Thrill-averse but engaged**: checks positions daily, needs to feel in control, can't handle ambiguity. Match: systematic rules-based strategies with clear entry/exit triggers, no discretion required.
- **High-patience, low-frequency**: sets a position and forgets it for weeks. Match: long-term trend-following, pairs trading, or deep value with 6-12 month holding periods.

**Why ML:**

The space of strategies is large and the space of psychological profiles is continuous. Rules-based matching ("conservative traders get bond strategies") is too coarse. ML can learn from:
- Which strategies traders actually abandoned vs. held through (real broker data, anonymized)
- Self-reported emotional state during simulated drawdowns
- Behavioral signals: log-in frequency, order frequency, override rate (how often they deviate from the system's signal)

A recommendation model trained on this produces a ranked list of strategies for each trader, with estimated adherence probability — because a strategy with a 30% expected return and 90% chance the trader will stick to it is better than one with 50% expected return and 40% chance they'll bail at the worst time.

**The dating-site analogy:**

Dating apps don't just match on stated preferences ("I want someone tall and funny"). They learn from revealed behavior: who you swipe on, who you message, who you go on a second date with. Similarly, this system doesn't just ask "how much risk can you tolerate?" — it observes behavior in simulated and live conditions and infers actual tolerance.

Long-term, the system could evolve the match as the trader matures — a trader who survives their first 30% drawdown without panicking now qualifies for a different strategy tier.

**What makes this hard:**

- Traders lie about their risk tolerance, and so do their stated post-hoc explanations for why they exited
- Strategy returns are non-stationary; a strategy that matched a trader well for three years may stop working in a regime change
- Regulatory constraints on providing personalized investment advice vary by jurisdiction
- Requires either broker data partnerships or a paper-trading simulation environment with enough emotional fidelity to generate useful signals
