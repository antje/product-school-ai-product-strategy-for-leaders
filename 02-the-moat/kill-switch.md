# Kill Switch Audit

## Vendor Dependency Assessment

| Dimension | Current State | Risk Level | 48-Hour Action |
|-----------|--------------|------------|---------------|
| **Provider** | Anthropic, handling every call from retrieving past experiments to writing the objection. Inherited from the skills implementation, not chosen for the productized version | H | Provision a second provider account and move the evidence-formatting calls to it end to end, so a second path is proven, not assumed |
| **Abstraction** | Product code calls the provider SDK directly. The coaching logic is portable text, but nothing between it and the vendor | H | Replace every direct SDK call with one internal function, `coach.complete(task_class, context)`, with provider and model name read from config. One file, no behaviour change |
| **Routing** | None. Every request goes to the same frontier model regardless of what it is doing | H | Add `task_class` to `coach.complete()` and route `retrieve`, `match` and `format` to a small model on the second provider, keeping `object` on frontier. Ship behind a flag |
| **Eval** | The backtest already exists as a quality bar, because the product scores its own advice | L | Run the backtest against the candidate model and compare flagged versus unflagged separation, pooled across at least three customer histories |

Why the concentration matters more here than usual. Anthropic is both the supplier and a plausible attacker. Module 1 scored Platform Exposure at 2 out of 5 for this reason. A normal vendor can raise prices or fail. This one can also ship the feature free inside a tool the customer already has open, which means the pricing scenario and the competing-product scenario below are the same company.

*Refined after Module 6.* The encroachment assessment in the flywheel file puts Anthropic at about 25% of value at risk, behind ChatPRD at 65% and the experimentation platforms at about 50%, and the Module 6 revision moved the product upstream of the platforms. Anthropic remains the supplier this audit is about; it is no longer the attacker the strategy is built to survive. The two scenarios below stand as the supplier risk.

Why Eval is the outlier. For most teams this is the dimension that blocks a swap, because proving a replacement model is good enough needs a quality bar nobody built. Here it came free. The product already runs its own advice over completed experiments and measures how often it was right, and that is the harness a provider swap needs.

What the gate should be, and why that number. One customer's backtest produces about 17 labelled calls, which can only detect a difference of roughly 22 percentage points. Pooling three customer histories gives about 51 calls and resolves to 13 points. Five gives 10 points.

So the swap gate is: pool at least three customer backtests, and accept the candidate only if it lands within 15 points of the incumbent. Not because 15 is a comfortable margin, but because it is the smallest difference the available sample can actually see. Claiming a tighter gate would be claiming precision the data does not support.

*Refined after Module 4.* Adding Endorse doubled the scorable share of a backtest, so one customer now yields about 32 labelled calls and resolves to roughly 16 points, and three pooled resolve to about 9. The 15-point gate stays, now as a conservative bar that three histories clear with room, and the pooling rule stays because it matches the unit of decision the backtest itself uses.

## Portability Score

Partial.

Not Locked, because the expensive dimension is already handled. Eval is normally the blocker and it is the one thing here that is strong.

Not Ready, because three of four dimensions score High and a swap today would be a guess. Every call goes direct to one provider, with no interface in between and no way to send cheap work somewhere cheaper.

Partial to Ready is about two weeks of ordinary engineering. The dependency is a choice that has not been made yet, not a trap that has closed.

## If Anthropic doubles pricing tomorrow:

The 48-hour response is routing, not renegotiation.

Most of what the product does needs no frontier reasoning. Retrieving a team's past experiments, matching a new hypothesis against them, and formatting the evidence panel are all small-model work. Writing the objection is the part that needs the best model available.

Assume 30% of calls genuinely need frontier and the rest move to a small model on a second provider at roughly a tenth of the price. A doubling then leaves the bill at **0.67 of what it is today**, so the shock becomes a 33% reduction instead of a 100% increase.

That 30% figure was the pre-cascade assumption and the answer is sensitive to it:

| Share needing frontier | Bill after the doubling | Versus today |
|---|---|---|
| 20% | 0.48 | -52% |
| 30% | 0.67 | -33% |
| 40% | 0.86 | -14% |
| 50% | 1.05 | +5% |

The break-even sits just under half. If more than about 48% of calls genuinely need frontier reasoning, routing does not save the product from a doubling and the answer becomes renegotiation or a full swap.

Which means the first action is measurement, not engineering. Tag every call by task class and log a week of real volume, so the split is known before it is relied on.

*Refined after Module 3.* The cost model built the cascade this scenario assumes: frontier handles 0.47% of requests and 8.3% of AI cost, with 96% of requests on small models and embeddings. On that split a doubling of the frontier price raises AI COGS by about 8%, inside the 50% price-rise stress test the margin file ran, which moved gross margin from 74.3% to 71.0%. The table above stays as the sensitivity it was; the measurement action stays first, because the 4% is modelled and not yet logged.

## If Anthropic ships a competing product:

The coaching prompts are not defensible. They are text, and a platform that wants to write similar ones will.

Three things survive, and they survive for the same reason: none of them can be bundled into a model.

**The integration graph.** The issue tracker, the product analytics and the customer feedback channels are separate systems with separate authentication, and a coding assistant has no reason to connect to them. Repository context is already commoditised and should not be counted.

**The outcome record.** Verifying that a prediction held requires watching one team's specific metric read out over weeks. That is a mechanism running over time, not a capability that ships in a model release.

**The willingness to publish accuracy.** This is the one nobody will copy, and not for a technical reason. A number attached to a bundled free feature invites questions about every other bundled feature, so a platform has no incentive to state its own hit rate and every incentive not to.

The limit on that last point: it is a bet about how a competitor behaves, not something structural. It holds while nobody is brave, not forever.
