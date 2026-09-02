# Cost Curve & Pricing Strategy

## What product-coach does, and how often

The coach sits in a product manager's daily work. It helps with prioritisation calls, OKR drafts, reading a dashboard, prepping a stakeholder conversation, and answering "have we tried this before" against the team's own history. On top of that daily help it does one thing formally: when an experiment brief is drafted, it raises an objection carrying a prediction, and weeks later it records whether that prediction was right.

That split matters for everything below. The daily help is frequent, cheap and unscored. The objection is rare, expensive and scored. The coach only claims a hit rate on what it formally predicted, not on everything it ever said.

**Usage, per seat per month.** Four assists on a working day is 88 interactions, plus 1.67 experiment reviews, plus ambient watching of open experiments. Counted in AI requests rather than user actions, that is **528 requests per seat per month**.

**One measured input.** The product is running and records the model, cost and outcome of every call in a `calls` table. Pulled 2026-09-01: 15 objections, $0.96 total, **$0.0642 average**, range $0.0449 to $0.1042, all on claude-opus-5. That measured figure is used for the objection line below. Everything else is modelled from published token prices and stated volumes.

## Where every number on this page comes from

Nothing here should have to be taken on trust, so the inputs are separated by how far they can be relied on.

**Measured, from the running product.** product-coach logs the model, the dollar cost and the outcome of every call in a `calls` table.

| | |
|---|---|
| Objections recorded | 15 |
| Total spend | $0.96 |
| **Average cost per objection** | **$0.0642** |
| Range | $0.0449 to $0.1042 |
| Model | claude-opus-5 on all 15 |
| Pulled | 2026-09-01, covering calls made 2026-08-29 |

Fifteen calls over one day is a small sample, and all of them replayed completed experiments rather than reviewing live drafts, which use a slightly different prompt. It is the only measured input on this page.

**Published, from vendor price pages.** USD per million tokens.

| Model | Input | Output | Used for |
|---|---|---|---|
| claude-opus-5 | $5 | $25 | The objection |
| claude-sonnet-5 | $2 | $10 | The harder fifth of daily help |
| claude-haiku-4-5 | $1 | $5 | Daily help, triage, verification, ambient checks |
| Embeddings | $0.02 | n/a | All retrieval and re-indexing |
| Vercel Pro | $20/month | | Hosting |
| Neon Launch | $19/month | | Postgres, holding the ledger and the corpus |

**Assumed, and these are the ones that can be wrong.** Each is a claim about behaviour that nobody has checked.

| Assumption | Value | Why this value | If it is wrong |
|---|---|---|---|
| Team size | 5 seats | One or two PMs plus a lead and analysts | Per-seat costs move inversely, team totals do not change |
| Experiments per team per year | 50 | Weekly cadence, carried over from the moat work | Metered revenue moves with it directly |
| Review passes per experiment | 2 | The draft, then the revision after the objection | Small. Reviews are 4% of requests |
| Daily assists per person per working day | 4 | A habit-forming but not constant tool. **The most load-bearing number here** | AI COGS moves almost one for one. At 8 it doubles |
| Working days per month | 22 | Standard | None |
| Tokens per daily assist | 12,000 in, 700 out | Retrieved context plus a short answer | Directly proportional to cost |
| Ambient checks per team per day | 8 | Roughly hourly during working hours | 6.6% of requests, small effect |
| Corpus items re-indexed per team per month | 600 | Tickets, docs and results that changed | Almost free, embeddings only |
| Onboarding per team | 2 hours at $150 loaded | One call to connect systems and read the first backtest | **65% of COGS.** At 4 hours margin drops 17 points |
| Teams, for amortising fixed cost | 10 | The first cohort | Infrastructure per seat falls as this grows |
| Cost of a wasted 2-week experiment | $25,000 | 2 weeks x 3 people at $220,000 loaded | The whole pricing argument scales with it |
| Cost to acquire a customer | $3,200 | 4 backtests at 2 hours each, plus $2,000 outbound | Payback scales directly. **Least evidenced number here** |

**Derived.** Everything else is arithmetic over those three groups, shown where each number first appears.

**Usage, worked through.** 50 experiments a year at 2 passes each is 100 reviews per team per year, 8.3 a month, and across 5 seats **1.67 reviews per seat per month**. Four assists a day across 22 working days is **88 interactions per seat per month**. Counted as AI requests rather than user actions, because one interaction fans out into several calls, the total is **528 requests per seat per month**, composed in the tier table below.

## Packaging decision

| | |
|---|---|
| **Leader** | The objection carrying the team's own evidence, plus the coach's hit rate on that kind of call |
| **Filler** | Daily task help. Frequent, cheap, and not what anyone signs a contract for |
| **Killer** | Continuous metric monitoring that proposes experiments on its own |
| **Killer usage** | Well under 70% |
| **Bundle or add-on** | **Add-on** |

The Filler is what earns the habit. Nobody adopts a tool they open twice a month, so the daily help is what puts the coach in the workflow and the objection is what makes it worth paying for.

**Why the Killer is an add-on, and it is not mainly about cost.** Priced as it would actually be built, 20 cheap checks a day plus one frontier proposal, it is $3.58 per team per month, or $0.72 a seat. Bundling it costs about two points of margin.

The reason to sell it separately is the 70% rule and what sits behind it. Teams will not hand an agent the job of proposing what to test before it has a track record, so adoption starts well below 70%. And its cost runs on calendar time rather than on use, which makes it the one feature whose bill is uncorrelated with the metered revenue funding everything else. Every other cost line moves with experiments reviewed. This one does not.

## Cost Model

Per seat per month, at an assumed 10 teams and 50 seats.

| Cost Category | Per-User/Month | How it is arrived at |
|--------------|----------------|-------|
| Inference (primary model) | $0.161 | (1.67 objections + 0.83 amortised backtest) x the measured $0.0642 |
| Inference (cascading/triage) | $1.778 | 88 daily assists, 35 ambient checks, 6.7 triage and verification calls, each priced by token count on haiku or sonnet |
| Infrastructure | $0.780 | ($20 Vercel + $19 Neon) / 50 seats |
| Data/storage | $0.002 | 396 embedding calls at roughly 1,000 tokens each, at $0.02 per million |
| Human-in-the-loop | $5.000 | 2 hours x $150 = $300 per team, / 12 months / 5 seats |
| **Total AI COGS** | **$7.719** | Template label. The first two rows and part of the fourth are AI. The rest is infrastructure and labour |

**Blended cost per request: $1.939 of AI cost over 528 requests, so $0.00367.** Gross margin is **74.3%** at $30 a seat and **94.3%** at the pricing proposed below, rising to 98.2% by year three.

Two things this table says that are worth stating plainly.

Frontier inference is 0.47% of requests and 8.3% of cost. That is what a working cascade looks like from the outside.

Human onboarding is still the largest single line at 65% of COGS, which is unusual for an AI product and is the first number to attack.

### Why the largest cost line is given away

Daily help is 84% of AI cost and is priced at zero. That is a strategy decision, not an oversight, and it is the same decision as the moat.

**It buys the workflow moat.** The moat work scored this product low on workflow depth because the coach appeared only at experiment time, which a team under deadline pressure can skip. Eighty-eight interactions a month is a habit. Under two is a tool nobody opens. The daily surface is what puts the coach in the path of the work, and it costs $1.64 a seat a month, paid out of gross margin on purpose.

**It feeds the data moat.** Every daily interaction adds context about what this team is working on and worried about, which is what makes the rare scored objection specific rather than generic. The cheap surface is the input to the expensive one.

So charging for daily help would raise revenue slightly and damage both moats at once. It would put a price on the thing that creates the habit, and starve the corpus that makes the paid output worth paying for.

**The load-bearing assumptions.** Four assists per working day is the one everything else rests on. Two hours of onboarding per team is the second. Both are guesses about behaviour rather than measurements, and both should be checked against the first real customer before this model is trusted.

## Cascading Strategy

**Triage model:** claude-haiku-4-5, for daily help, retrieval, triage, verification and ambient checks
**Frontier model:** claude-opus-5, for the objection
**Mid tier:** claude-sonnet-5, for the harder daily requests, roughly one in five
**Routing rule:** route on whether the answer will be scored. Anything the coach will later be held to goes to the frontier model. Everything else, including all retrieval and all daily assistance, goes to the cheapest model that can do the job.
**Expected cascade ratio:** **96% cheap / 4% mid and frontier**

### Feature to model tier, with the reason for each

| Feature | Complexity | Model tier | Why this tier, and not the one next to it | $/req | Vol % | Weighted |
|---|---|---|---|---|---|---|
| Daily task help, most of it | Simple | Small, haiku | Retrieval and summary over material retrieval has already selected. There is nothing to work out that is not on the page. A frontier model costs 5x and returns the same answer more slowly | $0.01550 | 13.3% | $1.0912 |
| Daily task help, the harder fifth | Medium | Mid, sonnet | Has to hold several sources at once and notice when they disagree, which is where a small model loses the thread. Not frontier, because being wrong costs a re-read and nothing is recorded | $0.03100 | 3.3% | $0.5456 |
| Retrieval for daily help | Simple | Embeddings | Vector similarity. No language is generated, so any model call here would be pure waste | $0.00003 | 50.0% | $0.0079 |
| Corpus re-indexing | Simple | Embeddings | The same operation on a schedule, where latency does not matter and nobody is waiting | $0.00002 | 22.7% | $0.0019 |
| Ambient watch on open experiments | Simple | Small, haiku | One binary question against a small diff: has anything changed that matters. It runs thousands of times, so per-call cost dominates, and 5x the price for a yes or no is not a trade | $0.00275 | 6.6% | $0.0962 |
| Retrieval inside a review | Simple | Embeddings | Fetching candidate past experiments. Judgment happens in the next step, not this one | $0.00003 | 2.2% | $0.0004 |
| Triage and number verification | Simple | Small, haiku | Triage is a bounded yes or no. Verification compares a stated figure to a retrieved row, which is arithmetic rather than reasoning | $0.00525 | 1.3% | $0.0351 |
| The objection | Complex | Frontier, opus | The only genuinely capability-bound step. It has to weigh several past experiments that used different mechanisms, decide whether the new hypothesis shares the mechanism or only the surface, and commit to a number. A live miss on ex-044 came from exactly that distinction, which is evidence the reasoning is hard rather than merely important | $0.06418 | 0.3% | $0.1072 |
| Backtest, amortised over year one | Complex | Frontier, opus | Identical task to the row above, so identical model. A cheaper one would produce a hit rate the customer then fails to reproduce | $0.06418 | 0.2% | $0.0535 |
| **Blended** | | | | **$0.00367** | **100%** | **$1.9390** |

**The rule this table follows: a task moves up a tier only when both tests pass.** Does a smaller model actually fail at it, and does being wrong cost something that matters?

Either test alone gives the wrong answer. Difficulty alone would push the harder daily-help requests to frontier, where being wrong costs a re-read. Consequence alone would push everything the coach is measured on to the biggest model available, including the arithmetic of checking a figure against a row, which any model gets right.

Only two of the nine lines pass both tests, and both are the objection. It is the one step where a smaller model measurably fails, because working out whether a new hypothesis shares a mechanism with a past experiment or only resembles it is the distinction the live miss on ex-044 turned on. It is also the only output anyone is ever shown a hit rate for.

Everything else fails at least one test and takes the cheapest model that clears the bar.

### What cascading is worth

Each model call priced on its own token profile, not the objection's.

| | AI COGS per seat | Total COGS | Margin at $30/seat |
|---|---|---|---|
| Cascaded, as modelled | $1.94 | $7.72 | **74.3%** |
| Every model call on the frontier model | $7.79 | $13.57 | **54.8%** |

Cascading cuts AI COGS by 75% and adds **19.5 points of gross margin**. At ten teams, not shipping it costs about $3,500 a year.

Worth building, and not existential. The temptation when modelling this is to price every request at the objection's size and produce a frightening number. Most requests are nothing like that shape: a daily assist on the frontier model costs $0.0775, not $0.12, and the 396 embedding calls would never go to a model at all.

**It is designed and it does not run yet.** `lib/ai/router.ts` maps three tasks to three models. `lib/coach/review.ts` only ever calls `task: 'objection'`, and every review in the ledger went to opus. A routing table can look like a cascade in code review while doing nothing, which matters more once the daily-help surface ships and multiplies request volume by 300.

**Retrieval is the volume, not the cost.** Embeddings are 75% of all requests and 0.1% of spend. They are easy to under-count and almost free, so the risk they carry is latency and rate limits rather than money.

## Pricing Model

**Current pricing:** none, the product is pre-revenue.

**Proposed AI pricing:** $500 per team per month, plus $298 per resolved call. In year one that is $6,000 base and about $2,150 metered, so roughly **$8,150 per team**, rising as the record deepens.

**Model:** hybrid.

**Strategy posture: maximize.** Not skim, because there is no track record to skim on. Not penetrate, because a low price on a product that claims to improve decisions argues against the claim.

### What the customer actually values

The obvious answer is a wasted experiment prevented, and it is wrong twice over.

**A failed experiment is not waste.** It is the mechanism. A team running 50 tests a year expects most to fail, because that is how the winners get found. A product that sells itself as stopping tests that would fail is selling less learning.

**Loss avoidance also sells badly.** There is no budget line for waste prevented, and nobody is promoted for experiments they did not run.

What the coach actually detects is not failure, it is **repetition**. Every objection cites the team's own past experiments. It does not say this will fail, it says you established this eighteen months ago. A test that fails for a new reason is valuable. A test that fails for a reason already in the corpus is the only real waste.

So the value is **recovered discovery throughput**: experiment slots taken back from re-treading known ground and spent on new ground instead. A team has roughly 50 slots a year, and recovering four of them is about 8% more novel experiments from the same headcount and the same calendar. That is a throughput number a product leader can put in a plan.

There is a second stream, and it is the social half of the job. Killing an experiment is politically expensive. A record showing the team tested this assumption three times, with results, is what makes the kill survivable in a review.

### Unit of work: one resolved call

A resolved call is an objection that the team acted on and that the outcome later showed was right. It is this product's equivalent of Intercom's resolved conversation, or a coding agent's resolved ticket: the customer is billed when they got the thing they came for.

Three units were considered and the difference is what revenue tracks.

| Unit | Per year | Price | Cost per unit | Revenue tracks |
|---|---|---|---|---|
| Experiment reviewed | 50 | $50 | $0.081 | Activity. Bills for "nothing to flag" 40% of the time |
| Objection raised | 30 | $83 | $0.135 | Warnings issued, including wrong ones |
| **Resolved call** | **7.2** | **$298** | **$0.482** | **Value delivered** |

Billing per experiment reviewed would charge a team about $1,000 a year for silence. Billing per objection raised charges for warnings whether or not they were any good. Only the third unit is one the customer would defend, and it is the one that makes the invoice and the hit rate count the same events.

**What it is deliberately not.** Not a seat, because the scored work happens 1.67 times per seat per month and access pricing needs frequency to feel fair. And not the daily help, even though that is 84% of the cost, because metering it would make people think before asking and that is the habit the whole position rests on.

**Why a base fee as well.** Two reasons. A resolved call reads out weeks after the work, so pure outcome pricing would put a quarter of lag into revenue recognition. And the record has value on days when nobody drafts anything, which is exactly when experiment cadence falls.

### Revenue scales with value, cost scales with usage

This is the reason the unit matters. The two do not move together, and the gap between them is the moat expressed as money.

**Cost tracks experiments.** Every review costs the same to produce whether the coach is right or wrong, so AI COGS moves with volume and stays forecastable.

**Value tracks the corpus**, and it compounds on two independent multipliers, which are the two moats.

The **data moat** makes the coach right more often, because every resolved call adds a labelled example. The **workflow moat** makes the team override less often, because they have watched the coach be right and the habit has set.

| | Experiments | Objections | Hit rate | Acted on | Resolved calls |
|---|---|---|---|---|---|
| Year 1 | 50 | 30 | 60% | 40% | 7.2 |
| Year 2 | 70 | 42 | 70% | 55% | 16.2 |
| Year 3 | 85 | 51 | 75% | 65% | 24.9 |

Experiments grow 70% over three years. Resolved calls grow **245%**, because two multipliers move at once instead of one.

| | Revenue | COGS | Gross margin |
|---|---|---|---|
| Year 1 | $8,146 | $463 | 94.3% |
| Year 2 | $10,828 | $210 | 98.1% |
| Year 3 | $13,420 | $245 | 98.2% |

Gross expansion is **133% in year two and 124% in year three**. Margin widens with tenure rather than narrowing, because revenue is tied to a quantity that compounds and cost is tied to one that does not.

### Checking the price against the value

At $8,146 in year one for 7.2 resolved calls, the buyer pays about $1,130 per call that changed a decision correctly.

For that to be worth it, roughly one resolved call in eight has to recover a slot that would otherwise have gone to known ground. Given that every objection is triggered by a match against the team's own history, one in eight is a low bar, and it is checkable in the backtest before anyone signs.

The comparison that makes the case is not against a cheaper tool. It is against the alternative of finding out eighteen months later that the team had already run the test.

| Option | Year 1 revenue | Gross margin | What the buyer is betting on |
|---|---|---|---|
| $30/seat | $1,800 | 74.3% | Nothing. The price is too low to signal that decisions are at stake |
| $60/seat | $3,600 | 87.1% | Access to a tool, not to an outcome |
| **$500/mo + $298 per resolved call** | **$8,146** | **94.3%** | **One resolved call in eight recovers an experiment slot** |

## Stress Tests

| Scenario | Impact on Margin | Response |
|----------|-----------------|----------|
| Inference costs 3x | 74.3% to 61.3% | Survivable, not comfortable. Push more daily help down to haiku and shorten the context sent with each assist, which is where the tokens are |
| Heaviest segment doubles usage | 74.3% to 67.8% | Watch rather than act. Metered revenue does not move with daily help, so a heavy user costs more and pays the same. Cap daily assists if a segment runs away |
| Model provider raises prices 50% | 74.3% to 71.0% | None required. The vendor swap gate from the kill switch audit applies if it becomes structural |

All three are measured at $30 a seat, which is the harsh case. At the proposed pricing none of them takes margin below 91%.

Three scenarios hurt more than any of those.

**Onboarding takes four hours instead of two.** Margin falls from 74.3% to 57.6%, because labour is 65% of COGS. Making the backtest self-serve is worth more than every token optimisation combined.

**The cascade never ships.** Margin falls to 54.8%. At 19.5 points it is the largest controllable item on this page.

**Monitoring gets bundled.** Margin falls to 71.9%, only two points. So the case for selling it separately rests on adoption and on its cost being uncorrelated with revenue, not on the size of the bill.

### Holding quality while cutting cost

If cost has to come down without any answer getting worse, three levers come first, and all of them attack daily help, which is 84% of AI spend, rather than the objection, which is 5.5%.

**Prompt caching, about 52% of the daily-help bill.** Roughly 9,000 of the 12,000 tokens sent with an assist are identical every time: the system prompt, the corpus summary, the person's profile. Cached input bills at a tenth of the normal rate, so a haiku assist falls from $0.0155 to $0.0074. The gateway already implements this, with cacheable blocks ordered stable to volatile.

**Trimming the context, 65% cumulative.** Sending 12,000 tokens where 6,000 would do is a retrieval problem rather than a cost problem, and fixing it tends to improve answers by removing noise.

**Semantic caching on repeats, 74% cumulative.** "Have we tested this before" gets asked repeatedly, often by different people on the same team in the same week. Same question, same corpus, same answer.

Together these take AI COGS from $1.94 to about $0.73 a seat, lifting margin at $30 from 74.3% to 78.3%, with no answer getting worse.

**What not to cut.** The objection is $0.107 a seat, 5.5% of AI COGS. Downgrading it to sonnet saves 0.8% of total COGS and puts the only scored output in the product at risk. Cut on the frequent path, never on the accountable one.

## Board One-Pager

**Before, traditional SaaS**
Revenue: $30 per seat times 5 seats = $1,800 per team per year
COGS: $463 per team in year one, of which $347 is fixed and $116 variable
Gross margin: **74.3%**

**After, AI-powered**
Revenue: $500 per month base plus $298 per resolved call = $8,146 per team in year one, $13,420 by year three
COGS: $463 in year one, $245 by year three
Gross margin: **94.3%**, rising to **98.2%**

**Net margin shift**
Δ margin: **+20.0 points in year one, +23.9 by year three** · Δ gross dollars: **+$6,346 per team per year**, or +$63,460 at ten teams

### The narrative

**Why margin moves, and why it moves the unusual way.** The standard AI board story is margin down and gross profit up, and the job is explaining why the trade is fine. This one goes up on both, and the reason is structural rather than good housekeeping. The expensive part of the product is the daily help, which stays free because it buys the habit. The priced part is the rare scored call. Charging for the work rather than for access adds $6,346 per team and no cost at all.

**Why it keeps moving.** Cost tracks experiments reviewed, which grows 70% over three years. Revenue tracks resolved calls, which grows 245%, because two things compound at once: the coach is right more often as the corpus fills, and the team overrides less often as it watches the coach be right. Those two are the data moat and the workflow moat, and this is where they show up on the P&L.

| | Experiments | Resolved calls | Revenue | Gross expansion |
|---|---|---|---|---|
| Year 1 | 50 | 7.2 | $8,146 | |
| Year 2 | 70 | 16.2 | $10,828 | **133%** |
| Year 3 | 85 | 24.9 | $13,420 | **124%** |

**That is gross expansion, not net revenue retention**, and the difference is what a board is actually shown. Net of churn, at a 133% gross expansion:

| Logo retention | NRR |
|---|---|
| 100% | 133% |
| 90% | 120% |
| 80% | 106% |
| 70% | 93% |

NRR clears 100% unless roughly a quarter of teams churn. With no customers there is no churn data, so the honest claim is that the pricing model makes strong NRR reachable and retention decides whether it is reached. The moat argument and the retention argument are the same argument, which is convenient and also means they fail together.

**The hedge.** If metered usage collapsed to zero the base fee alone is $6,000 per team, 74% of year-one plan, still clearing 92% margin against a $463 cost to serve. If the premium proves unsellable, retreating to $60 a seat gives $3,600 at 87% margin, a worse business but not a broken one.

### The number this page was missing: payback

Gross margin is half of unit economics and it is the flattering half. A CFO asks what a customer costs to acquire and how long gross profit takes to repay it.

**Cost to serve is front-loaded.** Year one is $463 per team because onboarding sits in it. From year two it is around $210, so margin rises without anything improving.

| Price | Year 1 ACV | Year 1 gross profit | CAC payback | 3-year LTV:CAC |
|---|---|---|---|---|
| **$500/mo + $298 per resolved call** | **$8,146** | **$7,683** | **5.0 months** | **9.8x** |
| $60/seat | $3,600 | $3,137 | 12.2 months | 3.1x |
| $30/seat | $1,800 | $1,337 | 28.7 months | 1.4x |

**This is the real argument against seat pricing, and it is not margin.** At $30 a seat the product still runs 74% gross margin, which looks fine, takes 29 months to repay the cost of winning the customer, and returns 1.4x lifetime value against acquisition cost. That business cannot fund its own growth. The same cost structure on resolved calls pays back in five months at 9.8x, and the multiple improves each year because revenue compounds while the cost to serve does not.

The sales motion is human and evidence-led, because a backtest has to be run and explained. Only a high ACV carries that.

### What this asks the board to decide

**Approve the pricing model change.** Seat to hybrid on resolved calls is +$6,346 per team in year one at no additional cost, and it moves CAC payback from 29 months to five. What has to be true is that the backtest convinces a buyer, and that is testable before any of this ships.

**Fund the cascade before the daily-help surface launches.** It is 19.5 points of gross margin and about $3,500 a year at ten teams. Cheap to build now, awkward to retrofit once request volume is 300 times higher.

**Fund self-serve onboarding.** Two hours of a person per team is the largest line in year-one COGS, and more importantly it is a growth ceiling. A hundred teams is 200 hours, five person-weeks per cohort. Each hour removed returns $150 per team per year and, at scale, the ability to add customers without adding people.

### What would say this is wrong

Three numbers, in the order they would surface.

**The acted-on rate not rising.** The whole expansion case assumes teams override less as the coach earns trust, moving from 40% acted on to 65%. If that rate is flat after two quarters, the workflow moat is not forming and revenue grows only with experiment volume, which takes gross expansion from 133% back to about 112%.

**The hit rate not rising.** The data moat assumes 60% to 75% as the corpus fills. If it is flat, the coach is not learning from its own record and the central claim of the product is in question, not just the pricing.

**CAC nearer $8,000 than $3,200**, which is plausible for a human, evidence-led sale. Payback stretches past a year even at the proposed price. Replace that assumption with a measurement after the first five deals rather than carrying it into a plan.
