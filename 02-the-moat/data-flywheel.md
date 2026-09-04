# Data Flywheel Map

> Score each loop 1-5. Your weakest loop is where competitors attack first.
> The four loops below are the M2 starting point - adapt if your product has 2 or 6 loops instead of 4.

## Flywheel Loops

| Loop | Score | What the product captures today | How it compounds | What the user notices next time |
|---|---|---|---|---|
| **Correction** | **4/5** | The accept-or-override choice, then the experiment result that says who was right | Every override comes back labelled, so the system learns which objection types hold up | Objections start citing the user's own past disagreements and how they turned out |
| **Preference** | **2/5** | Override events, who overrode and on what kind of objection | Nothing acts on it yet, and when it does it has to run backwards | Nothing. Every user gets the same coach |
| **Domain Context** | **1/5** | Nothing that crosses areas, the beachhead is one decision type | It does not, siloed on purpose | Nothing. Moving from activation to retention, the coach starts cold |
| **Network** | **2/5** | Every objection, override and outcome, held per customer | Which objection types prove right is not confidential, so it can be pooled | Nothing at launch. Once there are enough customers, a benchmark before they have any history |

### Correction Loop - 4/5

**What you capture today:** The coach raises an objection. The user accepts the sharpened hypothesis or keeps the original. That choice is a correction, and it is captured by construction, because it is a button in the main flow rather than a feedback widget nobody clicks.

**How it compounds:** Three weeks later the experiment reads out and settles who was right. Most products store the disagreement and never learn the answer, so what they hold is a pile of opinions. Here it comes back labelled, without anyone doing extra work. The label is clean only when someone overrides, because an accepted objection means the original hypothesis never runs and nobody learns what it would have done.

What improves is shared rather than per customer. The labelled results teach the product which kinds of objection hold up, and that lesson applies to every account. Each team's own history is read at the moment of the objection instead of being trained into a private model, so a new customer benefits from everything learned so far without anything being built specifically for them.

This is why 4 is the ceiling to aim for rather than a limitation. Reaching 5 would mean training a separate model per customer, and that cost grows with every account while the benefit stays inside one of them.

**What the user notices next time:** The next time they write a hypothesis assuming personalization drives activation, the coach does not say the team tested this before. It says they overrode this kind of objection three times, and two of those came in under target. Their own past disagreements become the evidence. After a few months the objections stop reading like generic advice and start reading like someone who was in the room the last time this went wrong.

### Preference Loop - 2/5

**What you capture today:** Override events, with who overrode and on what kind of objection. Nothing more.

**How it compounds:** It does not yet, because nothing acts on it. Two things keep this loop low on purpose.

A preference loop in a product whose job is to disagree is dangerous. Learning what someone prefers means learning to stop raising the objections they dislike, and the objections people dislike most are the ones about their favourite ideas. Satisfaction would climb while the product became worthless.

The second reason is cost. Deep personalization is per-person customization, which is the expensive end of the trade, and it produces something that helps one user and nobody else. The same effort spent on shared learning improves every account at once.

**What the user notices next time:** Nothing. Every user gets the same coach. The designed version would give someone who keeps overriding sample-size objections, and keeps getting burned by underpowered tests, more of those checks rather than fewer. The profile would record what a person is repeatedly wrong about rather than what they enjoy hearing. None of that is built.

### Domain Context Loop - 1/5

**What you capture today:** Nothing that crosses areas. The coach works on one kind of decision, experiments that get A/B tested, because that is the only ground where you can check afterwards whether the advice was right.

**How it compounds:** It does not. The narrow start is a trade. Covering one kind of decision means the evidence stacks up in a single place, which is what makes a claim about the coach's accuracy believable. Covering ten would leave a handful of examples in each and nothing defensible anywhere.

**What the user notices next time:** Nothing, and this is the visible cost of the narrow start. A product manager who has spent six months on activation moves to retention and the coach starts cold on the new area. It knows the team's experiment history but has no accumulated sense of the new problem space.

### Network Loop - 2/5

**What you capture today:** Every objection, override and outcome, held per customer.

**How it compounds:** Across customers rather than within one. Which kinds of objection get overridden and later prove wrong is not commercially sensitive, so it can be learned from every account without touching anyone's private information. Users never connect to each other, so this is pooled statistics rather than a network effect.

**What the user notices next time:** Nothing at launch, because pooling needs a customer base first. Once enough teams are running, a new customer's first objection can carry a benchmark drawn from every other customer, telling them how often teams like theirs override this kind of call and how often those overrides go badly. No single team could produce that for itself.

**Total Flywheel Score: 9/20**

**Weakest Loop:** Domain Context, at 1.

**Fix for weakest loop:** Build the cross-customer benchmark, which raises the Network loop. Leave Domain Context at 1 for now.

That answer runs against the exercise, which says to invest in the weakest loop, so both halves need explaining.

### Why not fix Domain Context

The coach works on one kind of decision: experiments that get A/B tested. An A/B test has a control group, so weeks later you can tell whether the coach's advice was right. On most other product decisions you cannot tell, because too many things change at once and nothing isolates the effect.

Domain Context scores 1 because what the coach learns from activation experiments does not carry over when the same person starts working on retention. The obvious fix is to cover more kinds of decisions, and it would cost more than it returns.

The other kinds of decisions are exactly the ones where nobody can check the advice afterwards. Roadmap calls, pricing changes, positioning. Expanding into them means giving up the ability to keep score, and keeping score is the only thing separating this from every other AI advice tool.

There is also an evidence problem. The coach's credibility comes from having reviewed many decisions of one kind and being able to say how often it was right about them. Cover ten kinds and there are a handful of examples in each, which supports no claim anywhere. Stay on one kind and the evidence stacks up in a single place.

So Domain Context stays at 1 on purpose, and gets addressed once there is a real record on experiments to extend from.

### Why the Network loop instead

The version not worth building is a genuine network effect, where each new user makes the product better for other users the way LinkedIn does. A review tool used by a product team of ten or twenty will never have that.

What is available is simpler. The company running the product can look across all its customers and find patterns no single customer can see: which kinds of objection people tend to override, and how often those overrides turn out badly.

Three things make it the right investment.

It works on day one. A new customer has no history of their own, so a benchmark drawn from everyone else is the only evidence available at that moment.

It touches nobody's confidential information, because the pattern describes a category of objection rather than any company's product plans.

And it works at small scale. A statistic about objection types settles down after roughly a hundred teams, where a network effect needs millions. That difference is why one is reachable within a year and the other is not.

It is also the only investment here that gets paid for once. Every other loop improves a single account, so the cost repeats with each new customer.

### How fast the loop turns

A flywheel is a claim about rate, so here is the arithmetic. Every input is an assumption, named so it can be argued with or measured.

**The assumptions.** A team running weekly experiments completes about 50 a year. The coach flags roughly a third of them, so about 17. Users override roughly 60% of what gets flagged, so about 10 produce a clean answer about who was right.

**One team alone is too slow.** Ten labelled calls a year is not a flywheel. On that path the product needs years before it can say anything about its own accuracy, which is the thing it sells.

**The backtest is what makes the rate workable.** A team's 50 completed experiments already have results attached, so the coach can be run over them and produce about 17 labelled calls immediately, before that team makes a single new decision. One customer signing up delivers what they would otherwise generate in eighteen months of live use.

The two kinds of label are not the same. A backtest label says whether the coach's judgment was right. A live label says that, and also what a human chose to do about it. The first arrives in bulk and is cheap. The second is what teaches the product which objections actually change behaviour.

**How many labels before a claim can be made.** Stating a hit rate near 70% within plus or minus 15 points takes about 36 labelled calls. Within 10 points takes about 81.

| Claim | Labels needed | Customer backtests |
|---|---|---|
| Overall hit rate, ±15 points | 36 | 3 |
| Overall hit rate, ±10 points | 81 | 5 |
| Hit rate per objection type, ±15 points, 8 types | 287 | 17 |
| Hit rate per objection type, ±10 points, 8 types | 645 | 39 |

An overall accuracy claim is available after roughly three customers, which is reachable in the first months. The per-objection-type claim, which is the version that appears in the product and tells a user how much to trust the objection in front of them, needs around seventeen customers.

That is the threshold for the flywheel doing visible work, and it is a sales target rather than an engineering one. It also confirms the priority independently: nothing in this arithmetic improves by making one customer's experience better.

**Refined after Module 4 (2026-09-03).** The rates above assume the coach only produces a scorable call when it objects. Adding a fourth outcome, an endorsement carrying its own prediction on named positive precedent, roughly doubles the share of reviews that produce a labelled row.

| | Object only | With endorsements |
|---|---|---|
| Scorable share of reviews | 31% | 63% |
| Labels per 50-experiment backtest | 16 | 32 |
| Backtests for an overall hit rate at ±15 points | 2.3 | 1.1 |
| Backtests for a per-call-type hit rate at ±15 points | 18.5 | 9.1 |

The seventeen-customer threshold above was the binding constraint on this whole strategy, and it halves. The figures in this section stay as written, because they are the record of what the design supported in Module 2. This is the correction.

### For comparison, a competitor's flywheel

Scored from public information about ChatPRD, so these are estimates rather than measurements.

| Loop | ChatPRD | product-coach | Difference |
|---|---|---|---|
| Correction | 2 | 4 | They capture edits to a generated document. Nothing tells them whether the document led to a good decision |
| Preference | 3 | 2 | They personalize templates and document style, and they do it better than this product plans to |
| Domain Context | 2 | 1 | They read Drive and Linear, so they hold more company context |
| Network | 1 | 2 | Neither has one. Nothing pools across their customers |
| **Total** | **8/20** | **9/20** | Nearly identical scores, different shape |

The totals being almost the same is the useful finding. This category does not have a flywheel. Everyone captures signal and nobody closes the loop, because closing it means finding out whether the advice was any good.

Two of the four loops are genuinely theirs. They personalize more than this product plans to, and they hold more of a company's context.

The whole difference sits in one loop. Their corrections tell them a user changed the wording. These tell the product the user was wrong. That is the only cell in the table where a signal comes back with an answer attached.

---

## Encroachment Threat Assessment

The percentages below need a basis, otherwise they are decoration. A customer paying for this product is paying for three things:

| What they are paying for | Share | Why |
|---|---|---|
| Objections specific to their situation | 25% | Table stakes. Generic advice is already free |
| The judgment in the objection itself | 40% | The service being bought |
| Proof the judgment is worth trusting | 35% | Without it this is one more opinion competing against free |

That split is an assumption, not a measurement, and it is the first thing to put in front of real buyers. Every percentage below is derived from it, so if the split is wrong the numbers move together.

### 1. Platform Encroachment

**Attacker:** Anthropic

**Vector:** The coding agent already reads the repository and keeps memory across sessions. Extending that memory to cover a team's product decisions turns context-aware advice into a free feature inside a tool the team already has open.

**Time-to-threat:** The first part has shipped. Project instruction files and cross-session memory exist today. The rest is one to two quarters, because frontier models release every three to four months and platform features move at that pace.

**% of value at risk:** About 25%. They take the first row of the table, and only that row. A model provider will not watch one team's experiment run for three weeks and then publish whether its own advice was wrong, because the only possible result is looking worse. The judgment and the proof both survive. It removes one reason to buy without touching the main one.

### 2. Vertical Competitor

**Attacker:** ChatPRD

**Vector:** Add a review step to the documents they already generate, using the customer data they already read from Google Drive and Linear. The objection mechanism is not hard to build and their team is capable of it.

**Time-to-threat:** One to two quarters.

**% of value at risk:** About 65%. They can take the first two rows, context and judgment, because both are copyable by anyone with the seats and the engineering. They cannot take the third without building an outcome record and choosing to publish an accuracy number.

The likelihood splits in two. Copying the mechanism is likely, because it is a quarter of work and they already have thousands of paying teams. Copying the scorekeeping is unlikely, because they sell document generation at $15 a seat and a published hit rate can only reduce that number.

### 3. Adjacent Expansion

**Attacker:** Statsig, Eppo, or Amplitude Experiment

**Vector:** Hypothesis review inside the experiment creation flow. They already hold the hypothesis, the result and the read-out date for every experiment their customers run, so the feature appears where the work happens with no integration for the customer and no procurement conversation.

**Time-to-threat:** One to two quarters.

**% of value at risk:** About 90%, and this is the worst of the three. They are the only attacker who could build all three rows, including the proof, because the outcome data is already sitting in their database.

The speed comparison is the uncomfortable part. Reaching a per-objection-type accuracy claim takes roughly seventeen customer backtests, which for this product means seventeen sales. They already hold hundreds of customers' experiment histories and could run the same backtest across all of them in a weekend.

What holds the number below 100% is that they see the experiment and not the decision. They have no objection, no override, and nothing from the repository, the tracker or the customer feedback channels. They know what was tested. They do not know what the team believed or what else it was weighing.

The likelihood is lower than the capability, for two reasons. Their buyer is data and engineering rather than product leadership, so this would be a new sales motion. And publishing an accuracy number invites the same scrutiny of everything else they sell.

**The conclusion this assessment changes.** Module 1 named ChatPRD as the primary attacker on two of three axes. That was wrong. Choosing A/B tested decisions as the beachhead, which was the right call for attribution, placed the product inside a surface the experimentation platforms already own. They are the more dangerous attacker, and the assessment should have found that before the beachhead was chosen rather than after.

## 90-Day Encroachment Plan

*Your partner played the Big Tech attacker. What was their plan to kill you?*

**Attacker:** Microsoft, Developer Division. Chosen over Google or OpenAI because they own GitHub, Azure DevOps and the enterprise licence, so they can attack distribution and breadth in the same move.

**Attack vector (target the weakest loop):** Domain Context, scored 1, plus Network, scored 2. The coach covers one kind of decision and has no cross-customer learning. Microsoft attacks both by going wide and by starting from a corpus this product would need years of sales to match.

**Weeks 1-4 - what they ship:** Decision Review inside GitHub Copilot Enterprise. It reads the repository, Issues, Pull Requests and Azure Monitor metrics, and comments on an experiment plan the way Copilot comments on code. Not a new product and not a new purchase. It appears in a tool most target customers already have open, on a seat they already pay for. product-coach needs a procurement conversation. Microsoft needs a feature flag.

**Weeks 5-8 - how they poach users:** They sell breadth where this product chose depth. Their version reviews the PRD in Teams, the roadmap item in Azure Boards, the launch plan and the pricing change. A VP of Product with eleven kinds of decision to make this quarter has never asked for a tool that covers fewer of them. And when a product manager moves from activation to retention, the coach here starts cold while theirs has been reading everything.

**Weeks 9-12 - why users don't come back:** They never arrive. The ask is a purchase order for a point solution covering one decision type, against a checkbox that covers eleven and came free with a licence renewed last March. The track record argument requires a prospect to try the product first, and nothing in the buying process gets them that far. Then it folds into E5 and the buyer stops being a product leader with a budget.

**Your defense:**

Two parts of that attack land and should be conceded.

The distribution asymmetry is real and permanent. A bundled free feature beats a paid point solution for any team that wants context-aware advice and nothing more. That is the 25% of value already written off in the platform assessment, and no amount of product work recovers it.

The breadth argument also lands with a buyer, because eleven decision types demo better than one.

The third part does not survive contact.

Microsoft's corpus is code, not product outcomes. GitHub holds repositories, issues and pull requests. Azure Monitor holds infrastructure telemetry. Neither holds the result of an A/B test on activation rate. So the benchmark they threatened to publish would be about code review, not about whether a product bet paid off, and those are different claims. The scale advantage evaporates once you ask which table the outcome data sits in.

Breadth also carries a cost they did not mention. Covering eleven decision types means covering ten where nobody can check afterwards whether the advice was right. A product that reviews everything cannot keep score on anything, because most product decisions have no control group. They would ship a broader product that is structurally unable to do the one thing this product sells.

And a free bundled feature has no incentive to publish its own accuracy. E5 features are not measured in public. The same disincentive that stops ChatPRD stops Microsoft, and it is stronger for them, because a number attached to a bundled feature invites questions about every other bundled feature.

So the defense is not to fight on breadth or on price, both of which are lost. It is to take the segment that has been burned by confident advice and wants a number attached to it, sell the backtest as the first conversation rather than the product, and stay on ground where results are measurable so the number keeps being true. That is a smaller market than Microsoft's, and it is one they have no reason to enter.
