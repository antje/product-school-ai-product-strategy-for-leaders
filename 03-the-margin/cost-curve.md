# Cost Curve & Pricing Strategy

## What product-coach does, and how often

The coach sits in a product manager's daily work. It helps with prioritisation calls, OKR drafts, reading a dashboard, prepping a stakeholder conversation, and answering "have we tried this before" against the team's own history. On top of that daily help it does one thing formally: when an experiment brief is drafted, it raises an objection carrying a prediction, and weeks later it records whether that prediction was right.

That split matters for everything below. The daily help is frequent, cheap and unscored. The objection is rare, expensive and scored. The coach only claims a hit rate on what it formally predicted, not on everything it ever said.

Usage, per seat per month. Four assists on a working day is 88 interactions, plus 1.67 experiment reviews, plus ambient watching of open experiments. Counted in AI requests rather than user actions, that is **528 requests per seat per month**.

One measured input. The product is running and records the model, cost and outcome of every call in a `calls` table. Pulled 2026-09-01: 15 objections, $0.96 total, **$0.0642 average**, range $0.0449 to $0.1042, all on claude-opus-5. That measured figure is used for the objection line below. Everything else is modelled from published token prices and stated volumes.

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

Usage, worked through. 50 experiments a year at 2 passes each is 100 reviews per team per year, 8.3 a month, and across 5 seats **1.67 reviews per seat per month**. Four assists a day across 22 working days is **88 interactions per seat per month**. Counted as AI requests rather than user actions, because one interaction fans out into several calls, the total is **528 requests per seat per month**, composed in the tier table below.

## Packaging decision

| | |
|---|---|
| **Leader** | The objection carrying the team's own evidence, plus the coach's hit rate on that kind of call |
| **Filler** | Daily task help. Frequent, cheap, and not what anyone signs a contract for |
| **Killer** | Continuous metric monitoring that proposes experiments on its own |
| **Killer usage** | Well under 70% |
| **Bundle or add-on** | **Add-on** |

The Filler is what earns the habit. Nobody adopts a tool they open twice a month, so the daily help is what puts the coach in the workflow and the objection is what makes it worth paying for.

Why the Killer is an add-on, and it is not mainly about cost. Priced as it would actually be built, 20 cheap checks a day plus one frontier proposal, it is $3.58 per team per month, or $0.72 a seat. Bundling it costs about two points of margin.

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
| **Total AI COGS** | **$7.719** | Template label. The first two rows and part of the fourth are AI. The rest is infrastructure and labor |

Blended cost per request: $1.939 of AI cost over 528 requests, so $0.00367. Gross margin is **74.3%** at $30 a seat and **94.9%** at the pricing proposed below, rising to 97.8% by year three.

Frontier inference is 0.47% of requests and 8.3% of cost. That is what a working cascade looks like from the outside.

Human onboarding is still the largest single line at 65% of COGS, which is unusual for an AI product and is the first number to attack.

### Why the largest cost line is given away

Daily help is 84% of AI cost and is priced at zero. That is a strategy decision, not an oversight, and it is the same decision as the moat.

It buys the workflow moat. The moat work scored this product low on workflow depth because the coach appeared only at experiment time, which a team under deadline pressure can skip. Eighty-eight interactions a month is a habit. Under two is a tool nobody opens. The daily surface is what puts the coach in the path of the work, and it costs $1.64 a seat a month, paid out of gross margin on purpose.

It feeds the data moat. Every daily interaction adds context about what this team is working on and worried about, which is what makes the rare scored objection specific rather than generic. The cheap surface is the input to the expensive one.

So charging for daily help would raise revenue slightly and damage both moats at once. It would put a price on the thing that creates the habit, and starve the corpus that makes the paid output worth paying for.

Two assumptions carry most of the weight. Four assists per working day, and two hours of onboarding per team. Both are guesses about behaviour rather than measurements, and both should be checked against the first real customer before this model is trusted.

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

The rule this table follows: a task moves up a tier only when both tests pass. Does a smaller model actually fail at it, and does being wrong cost something that matters?

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

It is designed and it does not run yet. `lib/ai/router.ts` maps three tasks to three models. `lib/coach/review.ts` only ever calls `task: 'objection'`, and every review in the ledger went to opus. A routing table can look like a cascade in code review while doing nothing, which matters more once the daily-help surface ships and multiplies request volume by 300.

Retrieval is the volume, not the cost. Embeddings are 75% of all requests and 0.1% of spend. They are easy to under-count and almost free, so the risk they carry is latency and rate limits rather than money.

## Pricing Model

**Current pricing:** none, the product is pre-revenue.

**Proposed AI pricing:** $500 per team per month, plus **$60 per experiment reviewed**. At 50 experiments a year that is $6,000 base and $3,000 metered, so **$9,000 per team per year**.

**Model:** hybrid, sold self-serve.

Strategy posture: maximize. Not skim, because there is no track record to skim on. Not penetrate, because a low price on a product that claims to improve decisions argues against the claim.

### What the customer actually values

The obvious answer is a wasted experiment prevented, and it is wrong twice over.

A failed experiment is not waste. It is the mechanism. A team running 50 tests a year expects most to fail, because that is how the winners get found. A product selling itself as stopping tests that would fail is selling less learning.

Loss avoidance also sells badly. There is no budget line for waste prevented, and nobody is promoted for experiments they did not run.

What the coach detects is not failure, it is **repetition**. Every objection cites the team's own past experiments. It does not say this will fail, it says you established this eighteen months ago. A test that fails for a new reason is valuable. A test that fails for a reason already in the corpus is the only real waste.

So the value is **recovered discovery throughput**: experiment slots taken back from re-treading known ground and spent on new ground. A team has roughly 50 slots a year, and recovering four is about 8% more novel experiments from the same headcount and calendar.

There is a second stream, and it is the social half of the job. Killing an experiment is politically expensive. A record showing the team tested this assumption three times, with results, is what makes the kill survivable in a review.

### Unit of work: one experiment reviewed

Billing happens when a team submits an experiment brief and the coach reviews it. Not per seat, not per objection, and not per correct call.

Three candidate units were tested against what a buyer's finance function would accept, and two failed.

| Unit | Observable to the buyer | Gameable | Behaviour as the product works | Forecastable |
|---|---|---|---|---|
| Resolved call, acted on and right | No, we score it ourselves | Yes, by not clicking accept | Shrinks | No, three stacked rates |
| Objection raised | Yes | No | Shrinks | Partly |
| **Experiment reviewed** | **Yes** | **No** | **Grows** | **Yes** |

Why the outcome-based unit fails, even though the module recommends outcome pricing. A resolved call is defined as an objection the team acted on that our own scoring later judged correct. That means **the vendor decides the invoice**, which no buyer's finance function accepts and no auditor is comfortable with. Intercom can bill per resolved conversation because resolution is determined by the customer's behaviour, not by Intercom's opinion of its own accuracy. We have no equivalent, so we should not pretend to.

It also creates a leak that costs nothing to exploit. If billing depends on clicking accept, the rational customer reads the objection, acts on it, and clicks keep original. Full value, no charge. And it gives us a financial incentive to nudge people toward accepting, which corrupts the only thing the product sells.

Why the unit must not shrink as the product works. Objections fall as a team stops repeating itself, which is the product succeeding. Any unit tied to warnings therefore bills less the better it gets, and the expansion case would quietly depend on the coach not working.

Experiments reviewed does the opposite. Recovered slots mean **more** experiments, so the product working raises the billable quantity. Revenue and customer value move the same direction for the same reason.

On billing for a clean review. A share of reviews return no objection, and charging for those is not a flaw. A code review that finds nothing is still a code review, and an audit that finds nothing still gets invoiced. What is being bought is a check on every decision.

Refined after Module 4 (2026-09-03). That argument was carrying more weight than it should. A fourth outcome was added to the coach: an endorsement, which cites positive precedent and carries its own prediction. That changes the picture materially. Roughly 63% of reviews now return a scored call rather than 31%, and only 37% return nothing at all. So most reviews produce a cited, falsifiable output, and the invoice needs less defending than it did. The unit and the price are unchanged, because the frontier model call happens on every review regardless of which way the call goes.

Why a base fee as well as metering. The record has value on days when nobody drafts anything, and experiment cadence falls exactly when a team is under pressure. The base holds the leadership view in place through a quiet quarter, and it carries the fixed cost of serving the account.

Not the daily help, even though it is 84% of cost. Metering it would make people think before asking, and that is the habit the whole position rests on.

### Revenue scales with value, cost scales with usage

Both move with experiments, but not at the same rate, and the gap is where the moats show up.

Cost tracks experiments reviewed and nothing else. Every review costs the same to produce whether or not it finds something, so COGS is forecastable from a single number.

Value tracks the corpus. As the record fills, the coach is right more often and the team overrides less. The same $60 review is worth more in year three than in month three, because the objection behind it is grounded in more of the team's own history. The **data moat** raises the hit rate. The **workflow moat** raises the rate at which advice is acted on. Neither shows up in the price, both show up in retention and in the customer's willingness to expand.

| | Experiments | Revenue | Growth | COGS | Gross margin |
|---|---|---|---|---|---|
| Year 1 | 50 | $9,000 | | $463 | 94.9% |
| Year 2 | 70 | $10,200 | 113% | $210 | 97.9% |
| Year 3 | 85 | $11,100 | 109% | $245 | 97.8% |

Expansion of 113% and 109% is more modest than a resolved-call model would project, and it is the number that survives scrutiny. It rests on one thing a customer controls and can verify: how many experiments they ran.

### Forecastability

The earlier design rested on three multiplied rates, none measured: flag rate, acted-on rate and hit rate. Across a plausible range the metered half spanned **$838 to $4,302, a 5.1x spread**. Presenting a point estimate from that would have been false precision.

Experiments reviewed rests on one assumption. Between 35 and 70 experiments a year, revenue runs **$8,100 to $10,200, a 1.3x spread**, and the buyer already knows which end they are at.

### Sales motion, which decides the price as much as the value does

An $8,000 to $9,000 contract sits in the awkward middle: too expensive for a casual card purchase, too cheap to justify a salesperson who must clear a security review to run the backtest. Left unresolved, that alone breaks the economics.

The answer is to make it self-serve, which is the same investment already argued for on cost grounds. The backtest connects to an analytics platform by OAuth and runs without a human, so a prospect sees their own history scored before talking to anyone. That is a product-led motion at a team price, which is how Linear, Vercel and Statsig sell in this range.

| Motion | CAC | Payback | 3-year LTV:CAC |
|---|---|---|---|
| **Self-serve, no rep** | **$1,200** | **1.7 months** | **24.5x** |
| Rep-assisted with security review | $3,200 | 4.5 months | 9.2x |

Both motions work, but only one is achievable without hiring, and the difference between them is the same self-serve onboarding work that is 65% of the cost of serving a customer.

### Checking the price against the value

At $9,000 a year for 50 reviews, a team pays $180 per experiment checked.

An experiment costs about $25,000 to run in loaded time for three people. So the review costs **0.7% of the experiment it is checking**. Framed that way the question is not whether $180 is a lot, but whether anyone would run a $25,000 test without a $180 check against their own history first.

| Option | Year 1 revenue | Gross margin | What the buyer is betting on |
|---|---|---|---|
| $30/seat | $1,800 | 74.3% | Nothing. The price is too low to signal that decisions are at stake |
| $60/seat | $3,600 | 87.1% | Access to a tool rather than a check on a decision |
| **$500/mo + $60 per experiment** | **$9,000** | **94.9%** | **That a check worth 0.7% of the experiment is worth running** |

## Stress Tests

| Scenario | Impact on Margin | Response |
|----------|-----------------|----------|
| Inference costs 3x | 74.3% to 61.3% | Survivable, not comfortable. Push more daily help down to haiku and shorten the context sent with each assist, which is where the tokens are |
| Heaviest segment doubles usage | 74.3% to 67.8% | Watch rather than act. Metered revenue does not move with daily help, so a heavy user costs more and pays the same. Cap daily assists if a segment runs away |
| Model provider raises prices 50% | 74.3% to 71.0% | None required. The vendor swap gate from the kill switch audit applies if it becomes structural |

All three are measured at $30 a seat, which is the harsh case. At the proposed pricing none of them takes margin below 91%.

Three scenarios hurt more than any of those.

Onboarding takes four hours instead of two. Margin falls from 74.3% to 57.6%, because labor is 65% of COGS. Making the backtest self-serve is worth more than every token optimization combined.

The cascade never ships. Margin falls to 54.8%. At 19.5 points it is the largest controllable item on this page.

Monitoring gets bundled. Margin falls to 71.9%, only two points. So the case for selling it separately rests on adoption and on its cost being uncorrelated with revenue, not on the size of the bill.

### Holding quality while cutting cost

If cost has to come down without any answer getting worse, three levers come first, and all of them attack daily help, which is 84% of AI spend, rather than the objection, which is 5.5%.

**Prompt caching, about 52% of the daily-help bill.** Roughly 9,000 of the 12,000 tokens sent with an assist are identical every time: the system prompt, the corpus summary, the person's profile. Cached input bills at a tenth of the normal rate, so a haiku assist falls from $0.0155 to $0.0074. The gateway already implements this, with cacheable blocks ordered stable to volatile.

**Trimming the context, 65% cumulative.** Sending 12,000 tokens where 6,000 would do is a retrieval problem rather than a cost problem, and fixing it tends to improve answers by removing noise.

**Semantic caching on repeats, 74% cumulative.** "Have we tested this before" gets asked repeatedly, often by different people on the same team in the same week. Same question, same corpus, same answer.

Together these take AI COGS from $1.94 to about $0.73 a seat, lifting margin at $30 from 74.3% to 78.3%, with no answer getting worse.

**What not to cut.** The objection is $0.107 a seat, 5.5% of AI COGS. Downgrading it to sonnet saves 0.8% of total COGS and puts the only scored output in the product at risk. Cut on the frequent path, never on the accountable one.

## Board One-Pager

Before, traditional SaaS
Revenue: $30 per seat times 5 seats = $1,800 per team per year
COGS: $463 per team in year one, of which $347 is fixed and $116 variable
Gross margin: **74.3%**

After, AI-powered
Revenue: $500 per month base plus $60 per experiment reviewed = $9,000 per team in year one, $11,100 by year three
COGS: $463 in year one, $245 by year three
Gross margin: **94.9%**, rising to **97.8%**

Net margin shift
Δ margin: **+20.6 points** · Δ gross dollars: **+$7,200 per team per year**, or +$72,000 at ten teams

### The narrative

Why margin moves, and why it moves the unusual way. The standard AI board story is margin down and gross profit up, and the job is explaining why the trade is fine. This one goes up on both, and the reason is structural rather than good housekeeping. The expensive part of the product is the daily help, which stays free because it buys the habit. The priced part is the review, which costs almost nothing to produce. Charging for the check rather than for access adds $7,200 per team and no cost at all.

Why it keeps moving. Cost falls after year one because onboarding is a one-time expense. Revenue grows because experiment volume grows, and it grows partly because the product works: recovered slots mean more experiments. That is the alignment worth pointing at. The product succeeding raises the billable quantity rather than reducing it, which is not true of any outcome-based unit we considered.

| | Experiments | Revenue | Growth |
|---|---|---|---|
| Year 1 | 50 | $9,000 | |
| Year 2 | 70 | $10,200 | **113%** |
| Year 3 | 85 | $11,100 | **109%** |

That is gross expansion, not net revenue retention. Net of churn:

| Logo retention | NRR |
|---|---|
| 100% | 113% |
| 90% | 102% |
| 80% | 90% |

NRR clears 100% if fewer than about one team in nine churns. With no customers there is no churn data, so the honest claim is that the structure makes NRR above 100% reachable and retention decides whether it is reached.

Where the moats show up. Not in the price, which is flat per review. In retention and in expansion. As the corpus fills the coach is right more often, and as the habit sets the team overrides less, so the same $60 review is worth more in year three than in month three. That is what makes a team run more experiments and keeps them from leaving. The data moat and the workflow moat are the retention argument, and they fail together if either stalls.

**The hedge.** If metered volume collapsed, the base alone is $6,000 per team, two thirds of plan, still clearing 92% margin against a $463 cost to serve. If the price proves unsellable, retreating to $60 a seat gives $3,600 at 87% margin, a worse business but not a broken one.

### The number this page was missing: payback

Gross margin is half of unit economics and it is the flattering half. A CFO asks what a customer costs to acquire and how long gross profit takes to repay it. This is also where the price and the sales motion have to agree, because a contract of this size cannot carry a salesperson.

| Motion | CAC | Year 1 gross profit | Payback | 3-year LTV:CAC |
|---|---|---|---|---|
| **Self-serve, backtest runs without a human** | **$1,200** | **$8,537** | **1.7 months** | **24.5x** |
| Rep-assisted, security review in the path | $3,200 | $8,537 | 4.5 months | 9.2x |
| $30/seat, rep-assisted | $3,200 | $1,337 | 28.7 months | 1.4x |

The real argument against seat pricing is not margin. At $30 a seat the product still runs 74% gross margin, which looks fine, takes 29 months to repay the cost of winning the customer, and returns 1.4x lifetime value against acquisition. That cannot fund its own growth.

And the real argument for self-serve is not cost. It is that it is the only motion this ACV supports. Nine thousand dollars is too much for a casual card purchase and too little for a rep who has to clear a security review before running the backtest. Making the backtest run on an OAuth connection without a human resolves both at once.

### What this asks the board to decide

**Approve the pricing model change.** Seat to hybrid on experiments reviewed is +$7,200 per team in year one at no additional cost. What has to be true is that a self-serve backtest convinces a buyer, and that is testable before any of this ships.

**Fund self-serve onboarding, and treat it as a revenue decision rather than a cost one.** Two hours of a person per team is the largest line in year-one COGS and a growth ceiling at 200 hours per hundred teams. More importantly it is what makes a $9,000 ACV sellable at all, by taking the rep and the security review out of the path.

**Fund the cascade before the daily-help surface launches.** It is 19.5 points of gross margin and about $3,500 a year at ten teams. Cheap now, awkward to retrofit once request volume is 300 times higher.

### What would say this is wrong

Three numbers, in the order they would surface.

**Experiment volume flat or falling.** The whole expansion case is that recovered slots produce more experiments. If volume does not move in year two, revenue does not either, and the value claim is unproven at the same time.

**Churn above one team in nine.** NRR drops below 100% and the expansion argument goes with it. Retention is where the moats are supposed to appear, so this failing means they are not forming.

**Self-serve conversion not working.** If prospects will not connect an analytics platform without a call, CAC goes to the rep-assisted number or higher, payback stretches past a year, and the ACV question reopens. Replace the $1,200 assumption with a measurement after the first twenty signups rather than carrying it into a plan.
