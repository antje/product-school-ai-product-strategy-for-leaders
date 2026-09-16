# Compounding System Design

## Feedback Loops

| Loop | Input | Output | Compounds? | Status |
|------|-------|--------|-----------|--------|
| Recursive Learning | Accept or override on each objection, plus the experiment result weeks later | Which objection types hold up, and how confidently to raise each one | N | broken |
| Cross-Domain Transfer | Read-outs from staged rollouts and flagged releases, graded B, alongside controlled tests graded A | Whether objection types that hold on controlled tests also hold on rollouts, and how much a grade B outcome should move confidence | N | designed |
| Network Intelligence | Objections, overrides and outcomes, held per customer | Which call types prove right across all accounts | N | missing |

**Broken loop identified by partner:** Recursive Learning. The product captures the accept or override on every objection, and resolves each prediction when the experiment reads out. It then uses none of it. The record is shown to the user and never returned to the reasoning, so the objection a team gets in month three is the one they would have got on day one, however the intervening calls turned out.

**Fix plan:** Return the resolved record to the review. The coach should read its own record, sliced by objection type, at the moment it forms an objection, and calibrate confidence against it, so a call type it has misjudged for this team before is raised tentatively and says so. Show the user the record that confidence was calibrated against, so the number carries its provenance. Owned by the Founder, gated on the golden rows not regressing.

### What N actually means at this stage

The tool asks present tense: does this loop compound today. product-coach is a prototype with no paying customers, so the answer is N three times, and it would be N three times for any pre-launch product in this category. The letter records the stage, not the design. The three N's have three different causes, and only one is a defect.

| Loop | What is actually absent | Gated on |
|------|------------------------|----------|
| Recursive Learning | The return path from the record to the reasoning | Nothing. This is a design decision we can make now |
| Cross-Domain Transfer | Attribution grading on read-outs, and the first grade B outcomes | The first design partner releasing behind flags |
| Network Intelligence | Customers, under data-use terms that permit pooling | The first design partners, whose agreements grant pooled use of objection-type outcomes and nothing else |

Cross-Domain Transfer was first declined as a scope decision, on the grounds that only controlled tests can be checked against a control. That kept scoring honest and left the product on the surface the experimentation platforms own, with a market of teams that run formal experiments weekly. The revised answer grades every read-out by the quality of its counterfactual: A for a controlled test, B for a staged rollout or flagged release, C for a plain launch. The coach objects on any decision that will produce a read-out, confidence and record weight follow the grade, and only A and B count toward the published hit rate. The loop is designed and not yet fed, because the record today holds only grade A outcomes.

Network Intelligence cannot exist before customers do. Marking it as a failure would be marking pre-launch as a failure.

Recursive Learning is the one to answer. The freeze test below decides how urgently, and the design commitments after it say what to do.

### The freeze test

Freeze the product for three months, about one frontier cycle, and give every competitor the same model. Model quality is then not the variable. The question is what is left.

| Product | What it competes on | What that asset does during the freeze |
|---------|--------------------|-----------------------------------------|
| ChatPRD | Templates, integrations, team workspaces | Static. Copyable in a quarter |
| Lennybot | Breadth of published practitioner content | Static. Already public |
| Statsig, Eppo, Amplitude | Optimization inside a decision already taken | Static. They never record whether the bet was worth making |
| product-coach | A verified record of predictions and outcomes | Grows. Cannot be backfilled |

Around 25 reviews per team accumulate over three months, each carrying a prediction that resolves when the experiment reads out. A competitor starting the same day has zero rows and no way to obtain them, because the record requires having been present when the decision was made, present when it was overridden, and watching when the metric came back. It cannot be bought, scraped or generated from a model. Every other asset in the table can be.

The last row describes the product we intend, not the one running today. The rest of this section is what has to become true for it to hold.

## What This Changes About the Product

Six design commitments follow from the diagnostic. They are decisions, not backlog items: each one forecloses or preserves an option that is expensive to recover later.

**1. The record is the product. The advice is how we earn the right to keep it.**

The natural way to build this is an advisor that logs its outputs. The diagnostic says to invert that. The advice is the part any competitor with the same model can produce next quarter. The record of what was predicted, what the team did instead, and what happened is the only asset that survives a freeze.

So the record becomes the primary surface, not a statistics page behind a link, and every product decision is judged on whether it makes the record denser or thinner. The first prototype put the coach's hit rate in the smallest type on the page and the refinement moved it under the objection. This commitment extends that from a layout fix to the organizing principle.

**2. Three moments have to be instrumented, and each has to be something the user wants.**

A learning loop needs the decision, the override and the read-out. Most tools in this category own only the first.

The product already records all three, which is why the broken loop above is a return path rather than a capture problem. Recording them is not the same as designing them. An override captured from a dismiss button is a row that says a user clicked something, and a read-out that waits for the user to come back is a row that never arrives. So the other two moments break as product problems before they are engineering problems, and the quality of everything the loop can learn is set here.

Captured as a reason the user is willing to state, the override becomes the most valuable row in the record, because a team overriding a correct objection is the single most informative event the product can observe. The design answer is to make it an assertion the user gets credit for: they go on the record too, and the scoreboard shows both sides.

The read-out will not happen if it requires the user to return. Nobody comes back four weeks later to close the loop on an objection they overrode. It has to arrive: the result finds the person who made the call, and closing the loop is one action inside that message.

A loop whose inputs users do not produce cannot be wired, however good the backend is.

**3. Separate craft knowledge from customer context in the data model now, before there is any data.**

Network Intelligence ships after the first paying accounts. The decision that enables it has to be made before the first one signs.

Two things get recorded and they are not the same kind of thing. What this team tested and what happened is customer context, private, and it never leaves the account. Which objection types prove right is craft knowledge, a property of product management rather than of anyone's business, and it can be pooled without exposing anything.

Stored as one blob per customer, the second can never be separated from the first, and pooling becomes a data protection problem instead of a product feature. That forecloses the loop permanently and quietly. Split at the schema, it stays open at no cost today.

**4. Cold start is solved by the pooled layer, not by the account.**

The M1 diagnostic scored Data Advantage 4 out of 5, and named the condition for a 5: the shareable slice alone makes a first-day customer measurably better served than a strong general model would. That condition is now a design commitment.

It also decides what the pooled layer is for. It is not a general improvement fund. Its job is the first thirty days of a new account, which is the window where this product is otherwise indistinguishable from a chat prompt and most at risk of churning before any record exists.

**5. Stop investing in anything that goes static under a freeze.**

The freeze table is also a kill list. Templates, integration breadth and content libraries all go flat the moment the model stops improving, and all of them are copyable by a competitor with more engineers. Four context sources, maintained to work and never featured as a differentiator. Every roadmap slot spent on integration count is a slot not spent on the record.

This is the commitment most likely to be broken under sales pressure, because integration count is what prospects ask about and record density is not.

**6. Throttle the loop on purpose: the record calibrates how loudly a call is made, never whether to make it.**

This is the guardrail the compounding loop needs, and it costs real compounding to install. A coach allowed to suppress objection types it had been wrong about would lift its hit rate by going quiet on exactly the cases a team most needs challenged, and the scoreboard would climb while the product got worse. Declining costs the team a warning and costs the coach nothing on the scoreboard, which makes silence the one failure this record cannot catch.

So the record should set confidence and phrasing, and a call type the coach has misjudged before should be raised tentatively and say so. It should never decide what goes unsaid. The loop compounds more slowly this way. That is what the guardrail costs, and it is worth paying.

### What this means for build order

1. The override and read-out experiences, because they are the inputs and nothing accumulates without them. The return path is gated on nothing technically, but wiring it to a record of dismissals would compound noise, so the inputs come first on purpose.
2. The return path from the record into the reasoning, which closes Recursive Learning.
3. The craft and context split, which costs nothing now and is unrecoverable later.
4. The pooled cold-start layer, at the first paying accounts.

Cross-Domain Transfer opens with attribution grading at the first design partner releasing behind flags, and the grade keeps it from diluting the record.

## Context Connectivity

**How knowledge flows:** One direction only. Objections and outcomes flow from the review into the record, and from the record to the user's track record page. Nothing flows back.

**Where it silos:** Two places, and they are Recursive Learning and Network Intelligence. Between the record and the reasoning, so outcomes never reach the next objection. And between accounts, where each team's history is fenced. Fencing is correct for a team's own experiments and wrong for which objection types prove right, and the design commitment above is to split those two at the schema so the second can be pooled without touching the first.

There is no third silo of the usual organizational kind, because there is no organization. One person builds, ships and reviews, which removes the classic handoff failures and replaces them with a single point of failure. The governance policy below accounts for that rather than pretending it away.

## Governance Policy

The posture in one line: the coach argues, it never acts. Every output is advisory and lands in front of the person who asked, and the product holds no write path into any customer system. That removes the Air Canada exposure of the classic kind. It is a permanent design constraint, not a stage we intend to grow out of.

The exposure that does exist is quieter: this product grades its own homework, and the grade is what we sell. Most of what follows guards that.

**Scope:** all customer-facing behaviour of the product-coach review product, covering the preflight refusal checks, the objection and endorsement path, the prediction ledger, and the track record surface.

**Excludes:** the fifteen local coaching skills that run inside a user's own agent. They never reach our infrastructure, store nothing, and make no model call we control or pay for. The shared name covers two different things and only one of them is governed here.

### Autonomy boundaries

| Decision | Level | Detail |
|---|---|---|
| Raise an objection or endorsement with a dated, falsifiable prediction | Auto | Advisory. The user decides, and the prediction is recorded either way |
| Read the repository, tracker, analytics and feedback channels | Auto | Read-only. No write scope is requested on any customer system |
| Run the preflight refusal checks | Auto | Deterministic arithmetic, no model call, no variance between runs |
| Score a prediction right or wrong when the read-out is unambiguous | Auto | Rule-based comparison against the threshold the objection committed to |
| **Score a prediction when the read-out is ambiguous** | **Human approval** | Defined below. Never resolved automatically. Grade C read-outs are never scored at all |
| **Ship a prompt or model change that alters how objections are formed** | **Human approval** | Gated on the golden set, thresholds below |
| Write to a customer's experiment, brief, ticket or backlog | Never | No approval path exists. A request for one opens a design review |
| Show a person's coaching profile to anyone but that person | Never | See the regulatory section |
| Propose experiments from metrics, once the monitoring add-on ships | Human approval | Draft only. Nothing reaches a backlog unreviewed |

The two human-approval rows carry the weight.

**Ambiguous read-outs.** Experiments come back inconclusive often: underpowered, flat, or with guardrails moving against the primary metric. Auto-scoring those is how a self-graded scoreboard drifts flattering, and the scoreboard is the product. Ambiguous means the 95% confidence interval on measured lift contains the threshold the objection named, or the experiment's minimum detectable effect exceeds the observed effect. Both tests need the read-out to carry a confidence interval alongside the point estimate, which the data model does not hold today. Until that field exists, every inconclusive result routes to manual resolution rather than being scored, so the rule degrades safely instead of silently failing to run.

**Prompt and model changes.** One prompt edit changes every objection every customer sees, which makes this the highest-leverage decision in the product. A change cannot ship if the golden-set pass rate is below 90%, if any adversarial row regresses against the previous version, or if the hallucinated-citation rate exceeds 1%. The run is stamped with the prompt version and attached to the release. Approver: Eval owner.

**What these cost.** Both buy safety with speed. The prompt gate means no wording change reaches customers without a golden run, which is roughly a day of latency on a change that would otherwise take an hour. Manual resolution of ambiguous read-outs puts a person in a loop that was designed to be automatic, and that load grows linearly with customers until the confidence-interval field ships. Both are worth paying. Neither is free, and leadership should approve them knowing that.

### Escalation triggers

Each one is measurable, and each names the state the system moves to.

1. A cited experiment id is absent from the corpus, or its read date falls on or after the brief's. Void the call, enter decline-only, page the Founder.
2. Golden-set pass rate falls more than 10 points on the four-week rolling window, or the hallucinated-citation rate exceeds 2%. Pin the last verified model id, page the Founder.
3. p95 review latency exceeds 30 seconds over any one-hour window. Page the Eval owner. No mode change, since a slow correct answer is still correct.
4. An experiment reads out ambiguous, meaning the 95% confidence interval on measured lift contains the threshold the objection named, or the minimum detectable effect exceeds the observed effect. Do not score. Queue for manual resolution.
5. Any request to write to a customer system. Refuse and log. This opens a design review rather than a permission request.
6. A request for a named individual's coaching profile from anyone other than that individual. Hold and refer to the regulatory section.

**Decline-only, defined.** A runtime state in which the coach still reviews and still refuses unreviewable briefs, and returns a decline on every call rather than an objection. It exists because the failure mode worth guarding against is a confident wrong citation, not silence. Entered automatically by triggers 1 and 2, and only by the Founder manually. Left only after the golden rows pass on the pinned version, which makes exit a measured event rather than a judgment call. This is the runtime hook the kill switch in the moat work assumed and did not name.

### Audit cadence

Continuous checks catch drift, periodic ones catch the systemic problems no automated rule is watching for. Owners are roles, not people. One person holds all of them today, and naming them separately is what makes the first hire obvious.

| Cadence | What we review | Owner |
|---|---|---|
| Realtime | Per-call invariants: every citation resolves to a real experiment, no replay cites anything dated after the brief, preflight refusals stay deterministic | Automated gate. No human in the path. Accountable: Founder |
| Daily | Golden set re-run, hallucinated-citation rate, p95 latency, each against its contract threshold | Eval owner |
| Weekly | Drift against a frozen model id, and override rate split by user experience level | Eval owner |
| Monthly | Every wrong call and every override read end to end, looking for a pattern the rubric missed | Product owner |
| Quarterly | Policy reviewed against shipped features, plus the regulatory tier below | Policy owner, with outside counsel from the first paying customer |

Four roles, one person. That is a single point of failure, not a design. The mitigation is the first row: the realtime invariants and the daily golden run are automated and block a bad release without anyone present, so the checks that protect customers do not depend on attendance. The weekly and monthly reviews are the ones that lapse during absence. Lapsing is acceptable at zero customers and not at one, which makes the first paying account the hiring trigger. The first hire is the eval owner, not a second builder, because that is the role whose absence is invisible until the scoreboard is already wrong.

### Regulatory exposure

**Regimes:** EU AI Act, GDPR. SOC 2 is not held and becomes required at the first enterprise customer, along with DPAs and sub-processor disclosure.

**Risk tier: limited, conditionally.** A decision-support tool for product teams sits in no Annex III category. The applicable obligation is transparency, which the product meets by construction, since the entire interface is an AI stating an opinion and every objection is labelled advisory.

**Controls.** Design-partner and customer agreements grant pooled use of one thing, which objection types proved right, and nothing else; a team's experiments, briefs and overrides never leave the account. No customer data trains any model. Prompts carry briefs and experiment metadata only, with no PII fields collected by design. The ledger holds a salted hash of the caller's IP for rate limiting and session-scoped call records. Model and prompt versions are stamped on every ledger row, so any score is attributable to a specific system version rather than to the product in general. Retention: IP hashes 30 days, since their only purpose is rate limiting; call records 24 months, because the track record is the product and a shorter window would delete the asset; aggregate craft statistics irreversibly anonymised and retained indefinitely. Deletion on request removes call records and any personal profile within 30 days and cannot reach the anonymised aggregates, which is stated plainly at signup rather than buried.

**Personal data.** Saying no PII is collected is too neat. An override is attributable to the person who made it, which makes it personal data under GDPR whether or not a name field exists. Data minimisation is therefore about what we do with it: the leadership record aggregates by decision and never by named individual.

**The condition on the tier.** Limited risk holds only while a person's coaching profile stays private to that person. Annex III covers AI used to evaluate people's performance in a work context, and a profile of what a named product manager is repeatedly wrong about, visible to the leader who signs the renewal, is exactly that. Building it as first designed moves the product to high risk, bringing conformity assessment, logging, human oversight and registration.

The decision is to keep the profile private to the individual. Leadership should see what that costs, not read it as a compliance conclusion. It removes per-person performance visibility from the product, which was one of the reasons a leader would buy. What survives is the record of decision quality for the team, aggregated and not attributed, and that is still a leadership-grade artifact. The renewal argument holds, and it is narrower than the original diagnostic assumed. The strategy's own pressure test points the same way: a leader installing an auditable record of how often their team overrode good advice is installing something that can be used against them, and making it per-person makes that worse.

## Agent Topology

Four components today, three of which call a model, plus one designed and not yet built. The last column separates rules the system enforces from conventions it merely follows, because a reader cannot otherwise tell which lines would survive a bug.

| Component | Can do | Cannot do | Enforced by |
|---|---|---|---|
| Preflight | Reject an unreviewable brief on arithmetic, and show its working | Call a model, or vary between runs | Code. No model in the path |
| Triage | Decide whether the history holds anything worth raising | Produce a customer-visible objection | Code. Its output is not user-facing |
| Objection | Reason over the history and commit to a dated prediction | Cite an experiment that does not exist, or one dated after the brief | Code. Unresolvable citations are dropped and counted; a replay citing the future raises and voids the result |
| Judge | Score a resolved prediction against measured lift | Run in production, or resolve an ambiguous read-out | Code for the first. Policy plus the manual queue for the second, owned by the Eval owner |
| Monitor, not built | Watch metrics and draft candidate experiments | Send, schedule or start anything | Design. To be enforced in code when built |

No component calls another component's tools. Retrieval is a whitelisted read against four named sources. Memory is session-scoped for the caller and per-customer for the ledger, with nothing shared across customers by default. There is no chain in the multi-agent sense, so there is no handoff to own, and that simplicity is worth keeping on purpose rather than losing by accident.

## Shadow AI Audit

A user-side audit: what people build around the product, not what they did before it existed.

The product is pre-launch, so none of this comes from a support inbox or a Zapier directory yet. Each row is derived instead from a decision this strategy has already made, which makes the workarounds forecastable and turns the audit into a test of those decisions.

The signal source column names where each one will surface first, so this doubles as an instrumentation plan. A team watching only support tickets would catch two of these six.

| Workaround | Signal source | Signal type | Freq | $/mo | Decision |
|------------|---------------|-------------|------|------|----------|
| Paste the coach's objection into ChatGPT to rewrite the brief | Sales calls | Capability gap | H | 20 | partner |
| Re-ask the objection in another model to check whether the coach is right | User interviews | Trust gap | H | 0 | build |
| Keep a private spreadsheet of which objections they overrode and why | Support tickets | Trust gap | M | 0 | build |
| Screenshot the track record into a slide for a quarterly review | Social media | Workflow gap | M | 0 | build |
| Zapier or Make recipe piping the analytics read-out into Slack to close the loop by hand | Zapier/Make recipe directories | Workflow gap | M | 15 | build |
| Pre-check the brief in ChatGPT before submitting, to avoid paying for a review that gets refused | Public forums/Reddit | Pricing gap | L | 0 | ignore |

Spend is charged to a row once. Rows one, two and six all run on a single ChatGPT Plus subscription at $20, so the seat is priced where it first appears and the other two carry zero. Row five is a Zapier or Make starter seat at $15. Pricing every row at list would total $75 and describe a person paying for the same tool three times, so the column as written sums to the real figure.

**Total tools found:** 6

**Tools after triage:** 4 build, 1 partner, 1 ignore, 0 undecided

**Estimated hidden spend:** $35 per product manager per month, the sum of the spend column. For a five-seat team that is $175 a month, or **$2,100 a year** spent on work this product created the need for.

**Dominant signal:** trust gap. Trust and workflow each account for two rows, but trust carries the higher-frequency one. Frequency is what separates a dominant signal from a merely present one.

### Action plan

**Build.** Four workarounds come native, sequenced as two pairs.

First, the two that are missing loop inputs. Override reasons: replace the dismiss button with a short assertion the user goes on record with, and show both sides on the scoreboard. Users keeping private spreadsheets are hand-building this, and every row in their file is a row missing from our ledger. Read-out delivery: the experiment result finds the person who made the call, with closing the loop as one action inside that message, because nobody returns four weeks later on their own.

These two go first because the return path that closes Recursive Learning is only as good as what reaches it. Wiring the loop to a record of unexplained dismissals would compound noise.

Then the two that depend on a record existing and being trusted. Evidence and track record promoted in the objection panel, so a user checking the coach against another model can see the cited experiments and the hit rate on this call type without leaving. Export of the decision-quality record as a shareable view, aggregated by decision and never by named individual, per the governance decision on the person layer.

Sequence: override reasons, then read-out delivery, then record prominence, then export.

**Partner.** ChatPRD, with a generic open-in-your-drafting-tool fallback for teams on something else.

Document generation is the stated hard no. It is the incumbent's ground and the economics where copies arrive fastest, so this is a workaround the strategy chooses to cause rather than one it failed to prevent.

Auth is per-user OAuth from product-coach to the drafting tool, with no service account and no org-wide token, so one user's drafting workspace is never readable on another's behalf. Data flows one direction only: we push the sharpened hypothesis and the objection text out, and never read documents back. That keeps a new and sensitive data class outside our boundary entirely, the control the governance audit found missing almost everywhere else. The entry point is a draft-this action attached to the sharpened hypothesis inside the review, not a settings-page integration. Drafting is where a review gets triggered, so meeting the user there is how the coach arrives before intent instead of after it.

**Ignore and monitor.** Pre-checking a brief in ChatGPT to avoid paying for a review that gets refused.

There is nothing to absorb. Preflight runs on deterministic arithmetic, makes no model call, and is already free, so the user is spending to avoid a charge that does not exist. The fix is telling them: state that the pre-check is free at the point of submission, and show what it checked.

The signal to re-evaluate is when this stops being a communication problem and becomes a pricing one, which happens if the workaround appears with the $60-per-experiment meter named in it. Revisit the metered component if pre-checking shows up in five or more public mentions, or if reviews per team fall below the 8.3 a month the margin model assumes. Either would mean the meter is suppressing the usage the workflow moat depends on.

### What the audit changes

Four of the six rows are the same complaint from different angles: the loop does not close inside the product, so users close it themselves. Re-asking another model, keeping a private override spreadsheet, screenshotting the record, and wiring a Slack alert for the read-out are all people doing by hand what design commitments 1 and 2 say the product should do. The demand side independently confirms what the diagnostic found.

The override spreadsheet deserves separate attention. A user maintaining their own record of overrides is keeping a shadow copy of the asset the whole strategy rests on. It says they want the record and do not trust ours to be complete or theirs to keep. Every row in that spreadsheet is a row missing from the ledger, which means this workaround does not merely indicate a gap, it actively drains the moat while it runs.

### Roadmap brief

Six workarounds, four build, one partner, one ignore, nothing undecided. Adjacent spend $35 per product manager per month. Dominant signal: trust.

Trust dominating changes what this audit is. Users double-checking the output against another model are not asking for a feature, they are telling us they do not yet believe the answer, which is a credibility problem wearing a feature request as a disguise. Building the four rows without fixing the credibility underneath would produce a better-instrumented product that people still verify elsewhere.

So the next move loops back to the reliability work rather than forward into new surface: the confidence tiers, the reliability contract, and making the evaluation legible to the user, not only to us. The one build row that matters most on this reading is record prominence, because it is the only one that directly answers "why should I believe this call," and the other three are worth less until it lands.

Sequence the build column on frequency against strategic relevance, not on frequency alone. Confirm the partner row with ChatPRD's partnership team before treating it as a plan. Re-run the whole audit each quarter, because workarounds move faster than roadmaps.

**What would make this audit real.** Each entry in the signal source column is a place to go looking. Search the support inbox for ChatGPT, Claude, Zapier and competitor names. Read the Zapier and Make directories for recipes naming the product. Ask in interviews what someone did in the ten minutes after the objection appeared, because the two highest-frequency rows here are invisible in telemetry and surface only by watching someone work. Five mentions is a pattern. All of it requires customers, which is the same gate as the judgment backtest, and the same reason this section forecasts rather than reports.
