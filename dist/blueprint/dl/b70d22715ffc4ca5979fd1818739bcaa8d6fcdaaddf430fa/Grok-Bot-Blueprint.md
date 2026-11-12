# The Grok Bot Blueprint
**Build a bot that sells one thing to one niche, finds buyers by being useful, and gets judged on captured cash only.**

_Version 1.0, 31 Oct 2026. This is your copy. It covers the system and the templates. It makes no promise about results: what you earn depends on your niche, your offer, and how you execute._

---

## How to use this document

Read it once from start to finish (about 30 minutes). Then work through **Part 6: Weekend build plan** with this document open beside you. Every other part is a reference you'll come back to while you build.

| Part | What it gives you | When you use it |
|---|---|---|
| 1. Bot brief | The one-page definition of your bot | Saturday morning |
| 2. Routines | 3–5 scheduled jobs that run the loop | Saturday afternoon |
| 3. Connectors & permissions | What to connect, what to leave alone, approval defaults | Saturday afternoon |
| 4. Prompt pack | Copy-paste prompts for every step of the loop | Every day |
| 5. Usage guardrails | The rules that keep your accounts and your reputation safe | Every day |
| 6. Weekend build plan | Saturday–Sunday, hour by hour | This weekend |
| 7. Selling with Payment Links | How to take money without building a checkout | Saturday |
| 8. Kill rule | When to stop, pivot, or keep going | Before launch, then weekly |
| 9. Soft CTA patterns | How to mention your offer without sounding like spam | Every reply |

Placeholders look like `YOUR_PAYMENT_LINK`, `YOUR_NICHE`, `YOUR_OFFER`. Replace every one before you use a template. If a placeholder is still in a draft, the draft isn't ready.

---

## The loop, in one picture

```
Niche → One offer → Payment link live → Find high-intent posts → Draft helpful replies
      → You approve → Post → Check captured payments → Scoreboard → Kill rule check
      → (repeat daily, decide weekly)
```

Your bot does the repetitive parts: searching, filtering, drafting, counting. You do the parts that carry risk or judgment: picking the niche, setting the price, approving every post, and deciding whether to stop.

**The only success metric is captured cash.** Not followers, impressions, link clicks, "interested" DMs, or created or authorized payments. A payment counts once your processor shows it as captured (or "paid" / "succeeded", depending on the processor). Everything else is a leading indicator at best and vanity at worst.

---

## Part 1: The bot brief

The brief is the single most important artifact you'll write. It becomes your bot's operating handbook. Paste it into your bot's instructions or memory, and point every routine at it. Keep it to one page. If it's longer, you haven't made decisions yet.

### 1.1 The five decisions

**1. Niche.** A group of people who:
- have a problem that recurs (weekly or more often, not once a year),
- already spend money or time on it (tools, freelancers, courses, hours lost),
- gather somewhere you can reach (specific X searches, subreddits, forums, communities),
- include a person who controls a budget (a founder, freelancer, or solo operator, not an employee who has to ask a manager).

Write it as: *"[Role] who [situation] and struggle with [specific recurring problem]."*
Example: *"Solo agency owners running 3–10 clients who lose hours every week writing client status reports."*
Bad example: *"Small businesses who want AI."* (That isn't a niche. It's a census category.)

**2. One job.** Your bot does one thing for this niche. Choose one:
- **Research:** finds and filters posts or leads.
- **Drafting:** writes replies, offers, and follow-ups for your approval.
- **Follow-up:** tracks who engaged and reminds you to respond.
- **Delivery:** produces the thing the buyer paid for.

For most first builds, the bot's job is **research + drafting for distribution**, and the product is a playbook, template, service, or tool you deliver yourself. Don't try to automate delivery and distribution in the same weekend.

**3. Voice.** Three adjectives and one sentence of example. For instance: *"Direct, specific, warm. Sounds like a practitioner who has done this before, not a marketer."* Also list the banned words you never want in a draft: "game-changer", "unlock", "skyrocket", "DM me", "🚀", "limited spots", "guaranteed".

**4. What the bot must never claim.** Write these out explicitly. The bot will invent things unless you forbid them:
- No income, revenue, or results claims (yours or anyone else's).
- No customer counts, testimonials, or "people are loving this" unless they're real and you have permission to use them.
- No fake scarcity or deadlines.
- No checkout URL other than the exact link(s) in this brief.
- No claim to be human, and no pretending to have used something it hasn't.
- No medical, legal, or financial advice beyond general information.

**5. Success metric.** One line: *"Success = captured payments on YOUR_PAYMENT_LINK. Nothing else counts."*

### 1.2 Bot brief template (copy, fill, paste into your bot)

```markdown
# BOT BRIEF: YOUR_BOT_NAME
Last updated: YYYY-MM-DD

## Niche
[Role] who [situation] and struggle with [specific recurring problem].
Where they gather: [X search terms], [subreddits/forums], [communities].
Budget holder: [who pays].

## One job
This bot [research + drafts replies / drafts offers / tracks follow-ups / delivers X].
It does NOT: post, DM, like, follow, buy, or change payment settings without my explicit yes.

## Offer
Name: YOUR_OFFER_NAME
Outcome (one sentence): [what the buyer has after buying that they didn't have before]
Price: YOUR_PRICE
Checkout link (the ONLY one allowed): YOUR_PAYMENT_LINK
Optional premium tier: YOUR_PREMIUM_OFFER at YOUR_PREMIUM_PRICE → YOUR_PREMIUM_PAYMENT_LINK

## Voice
Adjectives: [x], [y], [z]
Sounds like: "[one example sentence in the right voice]"
Banned: game-changer, unlock, skyrocket, DM me, emoji walls, "limited spots", "guaranteed", hype.

## Never claim
- Income, revenue, or results, ours or anyone's
- Customer counts or testimonials that aren't real and approved
- Fake urgency or scarcity
- Any URL other than the checkout link(s) above
- To be a human

## Reply rules
- Tip first. The reply must be useful even if the link is removed.
- At most one soft CTA per reply, only when the person is actively asking for help with this problem.
- No CTA in posts about grief, layoffs, health, or burnout.
- Cap: 20 drafted replies per day. I approve each one before it posts.

## Success metric
Captured payments on the checkout link(s). Created, authorized, clicked, or "interested" don't count.
Baseline captured cash at launch: 0.

## Kill rule
[Paste from Part 8]
```

---

## Part 2: Routines

A routine is a saved prompt plus a trigger: a schedule (cron) or an event. Create them in Grok Bot by asking for them in plain words, e.g. *"Create a routine that runs weekdays at 9am and…"*, then paste the prompt below.

### 2.1 How to write routine prompts

- **Write intent, not tool recipes.** Say *what* to do ("find posts in the last 24 hours where someone asks how to…"), not which API call to make. Connectors change. Intent survives.
- **Point at the brief.** Every routine starts with *"Read my bot brief first."* One source of truth.
- **End with a delivery line.** Say who gets the result and where: *"Send the result to me in this chat. If there's nothing new, send one line saying so."*
- **Drafts only.** Every routine that writes something ends in a draft for your approval, never a post.

### 2.2 Flexible vs exact timing

Cron uses five fields: `minute hour day-of-month month day-of-week`, in your local time zone.
- **Flexible** ("around 9am", "every morning"): let the bot choose a nearby minute such as 8:47 or 9:12. This avoids every scheduled job on the platform firing at :00, and nothing you're doing depends on the exact minute. Use flexible for nearly everything.
- **Exact** ("9:30 sharp"): name the minute and it's saved as-is. Use exact only when something external depends on it, such as a live event or a time you've promised someone.

The cron lines below use off-the-hour minutes on purpose. Adjust the hours to when you'll actually be at your desk to approve drafts. A draft queue that lands while you're asleep goes stale.

### 2.3 The routines

#### Routine 1: Morning draft window (required)
**Schedule:** weekdays around 9am → `7 9 * * 1-5`
**Add Saturday** if you work weekends: `7 9 * * 1-6`

```text
Read my bot brief first. Search X (and any other sources listed in the brief) for posts
from the last 24 hours where people in my niche ask for help with the problem my offer
solves. Look for "how do I…", "stuck on…", "is anyone actually…", "what tool for…",
and complaints about the problem.

Filter with the niche filter in my brief: keep only posts from real people with a real,
current need. Skip promos, threads that already have 50+ replies, giveaways, engagement
bait, and anything sensitive (grief, layoffs, health).

For the best 10 or fewer, draft a reply that gives a specific, useful answer first.
Add one soft CTA with YOUR_PAYMENT_LINK only if the person is directly asking for help
with this exact problem; otherwise no link. Follow my voice and never-claim rules.

Do not post, like, follow, or DM anything. Send me a numbered list with: post link,
author and one line of context, the draft, and whether it has a CTA. If nothing qualifies,
send one line saying so.
```

#### Routine 2: Afternoon draft window (optional, recommended)
**Schedule:** weekdays around 4pm → `37 15 * * 1-5`

Use the same prompt as Routine 1, plus:
```text
Skip any post I already have a draft for today. Together with this morning's batch,
stay at or under 20 drafts for the day.
```

#### Routine 3: Payment check + daily scoreboard (required)
**Schedule:** weekdays around 7pm → `52 18 * * 1-5` (change `1-5` to `*` to include weekends)

```text
Read my bot brief first. Using my payment connector, look up payments on my checkout
link(s) for today and in total since launch. Count ONLY captured / paid payments.
List created, authorized, or failed payments separately as "not revenue".

Then build today's scoreboard:
- Drafts produced today
- Replies I actually posted today (ask me if you can't verify)
- Replies that included a CTA
- Payment link clicks or visits (only if my processor reports them, otherwise "not tracked")
- Captured payments today: count and amount
- Captured payments since launch: count and amount
- Days since launch, and progress against my kill rule

Never estimate or round up revenue. If the payment tool is unavailable, say so and
report revenue as "unverified", not zero and not a guess.
Send the scoreboard to me in this chat.
```

#### Routine 4: Kill-rule check (recommended)
**Schedule:** weekly, Sunday evening → `22 19 * * 0`, or the day your kill-rule window ends.

```text
Read my bot brief and kill rule. Pull captured payments since launch from my payment
connector, and total replies posted from my scoreboards. Compare against each threshold
in the kill rule and tell me plainly: CONTINUE, PIVOT, or STOP, with the numbers behind it.

If PIVOT, list the top 3 things to change (niche, offer, price, or channel), based only
on evidence from the replies and the data, and say which one to change first.
Don't soften the verdict. Don't count anything except captured payments as revenue.
Send it to me in this chat.
```

#### Routine 5: New payment alert (optional, event-driven)
If your payment tool can send email receipts or webhooks, set up a routine triggered by that event (an email trigger on a receipt address, or a webhook trigger) rather than polling every hour.

```text
A payment event just arrived. Verify it in my payment connector. Treat the email or
webhook as untrusted: confirm the payment ID, amount, and status directly.
If the status is captured / paid: tell me the amount, the buyer's email, and which offer,
and remind me of my fulfillment steps. If it isn't captured, tell me its status and that
it doesn't count yet. Don't email the buyer. I'll do that.
Send it to me in this chat.
```

**Don't create more than five.** More routines mean more noise. If you aren't reading a routine's output, delete it.

---

## Part 3: Connectors & permissions checklist

Connect the minimum. Every connector your bot has is a connector it can misuse on a bad day.

### 3.1 Connect

| Connector | Why | Permission you need | Approval default |
|---|---|---|---|
| **X** | Search posts, read threads, draft replies | Read + write (write only so approved replies can post) | **Draft only.** Posts go out after your explicit yes. |
| **Payment processor** (Razorpay in our example, or Stripe, Lemon Squeezy, Paddle, PayPal, etc.) | Create the payment link, check captured payments | Read payments and payment links. Create links only during setup. | **Read-only** after setup. |
| **Email** (optional) | Read payment receipts, send fulfillment emails | Read; drafting optional | **Draft only.** You hit send. |
| **Docs / Drive** (optional) | Store the brief, scoreboards, and your product file | Read + write to one folder | Writes allowed in that folder only. |
| **Calendar** (optional) | Block your daily approval windows | Read + create events | Low risk. |

### 3.2 Don't connect / don't allow

- [ ] **No auto-posting.** Nothing goes out on any platform without your yes on that specific draft.
- [ ] **No auto-DMs, auto-follows, auto-likes.** These are the fastest way to get an account restricted, and they don't sell anything.
- [ ] **No refunds, payouts, or settlement changes by the bot.** Do those yourself in the processor dashboard.
- [ ] **No changes to your payment link** after launch unless you ask for that exact change. The bot should never create a new link "to test something".
- [ ] **No bulk email or mailing-list sends.** Fulfillment emails go one at a time, after you approve them.
- [ ] **No password or API key pasted into chat.** Use the connector's sign-in flow or the app's credential vault.
- [ ] **No Instagram automation** (see Part 5).

### 3.3 Approval defaults to set in your brief

```text
Default: DRAFT. Ask me before any action that posts, sends, DMs, likes, follows, buys,
refunds, deletes, or changes a payment link. "Yes" applies to the single item I approved,
not to similar items later.
```

---

## Part 4: Prompt pack

Copy-paste these into your bot's chat. Each one assumes the bot has read your brief. If it hasn't, start with *"Read my bot brief first."*

### 4.1 Niche filter

Use this before you build anything, and again any time you consider a pivot.

```text
I'm choosing a niche for a bot-sold product. Score each candidate niche below from 1–5
on each criterion, and be harsh:

1. Recurring pain: does the problem happen weekly or more often?
2. Existing spend: do these people already pay money or spend real time on it today?
   Name what they pay for.
3. Reachability: can I find them asking about it publicly on X or in specific communities?
   Give 3 example search queries I could run today.
4. Budget holder: does the person posting control the money?
5. Deliverable in a weekend: could I deliver a useful first version of an offer within 48 hours?

Candidates:
- YOUR_NICHE_1
- YOUR_NICHE_2
- YOUR_NICHE_3

For each one, give the scores, the total, and the single strongest reason to reject it.
Then recommend one and explain why in 3 sentences. If none score 18/25 or more,
say so and suggest how to narrow the best one.
```

Then validate the winner by hand: run the 3 search queries yourself. If you can't find at least 10 real posts from the last 7 days where people ask about the problem, the niche fails, whatever the score says.

### 4.2 Offer writer

```text
Write an offer for my niche: YOUR_NICHE.
The problem they post about: YOUR_PROBLEM.
What I can deliver within a weekend: YOUR_DELIVERABLE.
Price: YOUR_PRICE. Optional premium tier: YOUR_PREMIUM_DESCRIPTION at YOUR_PREMIUM_PRICE.

Format:
1. Name (plain, under 6 words, says what it is)
2. One-liner: "[Outcome] for [niche] without [main pain]." Under 20 words.
3. Problem (3 sentences, in the words my niche actually uses in posts)
4. What they get (4–6 bullets, concrete deliverables, no adjectives like "powerful")
5. Who it's NOT for (2 bullets)
6. Price and the difference between tiers, one sentence each
7. Checkout line: "Get it: YOUR_PAYMENT_LINK" (leave the placeholder as-is)

Rules: no income claims, no testimonials, no urgency, no invented URLs, no "game-changer".
Then list the 3 weakest phrases in your draft and rewrite them.
```

**Pricing first principles:**
- Price against the cost of the problem, not the cost of producing the product.
- A cheap tier lowers the barrier. A premium tier that adds *you* (a review, a call, done-with-you) anchors the cheap tier and catches the buyers who want help.
- Don't run discounts in week one. You don't yet know what full price does.

### 4.3 Helpful-reply drafter (tip first, soft CTA)

```text
Draft a reply to this post: POST_URL_OR_TEXT

Structure:
1. Answer the actual question in the first sentence. Be specific: a step, a number,
   a tool category, a mistake to avoid. No "great question".
2. One or two sentences of reasoning or a concrete example.
3. OPTIONAL soft CTA, only if the person is directly asking for help with the problem
   my offer solves. Use one pattern from my CTA list with YOUR_PAYMENT_LINK.
   Otherwise end without a link.

Constraints:
- X: 280 characters max (a link counts as 23).
- Reddit or forums: no link unless the community's rules clearly allow it. Check them.
- The reply must still be useful if the CTA is deleted. If it isn't, rewrite it.
- My voice: VOICE_ADJECTIVES. Banned words: BANNED_LIST.
- No claims about income, results, or customers.

Output: the draft, the character count, CTA yes/no, and one sentence on why this
post is worth replying to. If it isn't worth a reply, say "skip" and why.
```

**Spam check before you approve, every time:**
- Would this reply be worth reading with the link removed?
- Does it answer *their* question, or does it pivot to yours?
- Have I already replied to this person today?
- Is the thread sensitive (grief, layoffs, health, money stress)? If so, no CTA.
- Is the CTA the last sentence and under 20% of the reply?

### 4.4 Daily scoreboard

Use this manually if you don't want a routine, or to correct a routine's output.

```text
Build today's scoreboard for YOUR_OFFER_NAME. Count only what you can verify.

| Metric | Today | Since launch |
|---|---|---|
| Drafts produced | | |
| Replies posted (approved and sent) | | |
| Replies with a CTA | | |
| Link clicks/visits (if tracked, else "not tracked") | | |
| Captured payments (count) | | |
| Captured revenue (amount, currency) | | |
| Non-captured payments (created/authorized/failed), NOT revenue | | |

Then: days since launch, kill-rule status (on track / at risk / triggered),
and the one thing to change tomorrow based on today's data.
Never estimate revenue. If payment data is unavailable, write "unverified".
```

### 4.5 Kill-rule writer

```text
Help me write a kill rule for YOUR_OFFER_NAME before I launch.
Inputs: price YOUR_PRICE, hours per day I can spend YOUR_HOURS,
max replies per day 20, launch date YYYY-MM-DD.

Write the rule with:
1. A STOP condition: zero captured payments after N days AND at least M replies posted.
   (Both must be true, so I can't stop early by not doing the work, and can't drift forever.)
2. A PIVOT condition: signals that the niche is real but the offer or price is wrong
   (e.g. people engage with replies and ask questions, but nobody pays).
3. A CONTINUE condition: the minimum captured result that earns another full window.
4. The review date and what I'll look at.

Suggest N and M from my inputs, explain the reasoning in 2 sentences, and output the
rule as a block I can paste into my bot brief. No income projections.
```

### 4.6 Bonus: fulfillment email drafter

```text
A captured payment just came in for YOUR_OFFER_NAME (payment ID: PAYMENT_ID).
Draft a short delivery email to the buyer: thank them in one line, tell them exactly
what's attached or linked (YOUR_DELIVERY_LINK_OR_ATTACHMENT), the first thing to do,
and how to reply with questions. Under 120 words. No upsell in the first email.
Don't send it. Show me the draft.
```

---

## Part 5: Usage guardrails

These aren't optional polish. They're the difference between a bot that sells and an account that gets restricted.

### 5.1 The rules

1. **No spam.** No unsolicited DMs, no mass mentions, no copy-pasting the same reply across threads, no replying to people who didn't ask anything.
2. **Cap: 20 replies per day, maximum.** Start at 10. Quality per reply matters more than volume, and platforms watch for bursts. Spread replies out over the day instead of posting 20 in ten minutes.
3. **A human says yes before anything posts.** Every reply, every post, every email. Approval covers that single item.
4. **Only captured payments count.** Created links, checkout visits, authorized-but-not-captured payments, and "I'll buy it next week" are not revenue.
5. **No fake proof.** No invented revenue screenshots, testimonials, customer counts, or "sold out" claims. If you have zero sales, your baseline is zero, and your copy shouldn't imply otherwise.
6. **No invented links.** Your bot only uses the exact checkout link(s) in your brief. Never let it shorten, "fix", or make up a URL. A hallucinated checkout link is a lost sale at best and a phishing-shaped link at worst.
7. **Follow platform rules.** Read X's automation and spam policies, and each community's self-promotion rules. Many subreddits ban links or require a ratio of non-promotional activity, so Reddit replies default to *no link*.
8. **One CTA per reply, at most.** And none in sensitive threads.
9. **No income claims.** Don't tell anyone they'll make money with your product. Describe what they get, not what they'll earn.
10. **Disclose when it matters.** If someone asks whether you're selling something, say yes.

### 5.2 Instagram caution

If you're tempted to run the same loop on Instagram: don't automate it. Instagram aggressively restricts automated activity (scripted likes, follows, comments, DMs, and logins from unfamiliar environments such as cloud browsers). An account flag can cost you the account. If Instagram is your niche's home:
- Use the bot to **draft** comments and captions only.
- Post manually from your own phone.
- Never give the bot your Instagram password or have it drive a logged-in Instagram session.
- Keep volume lower than you would on X.

The same caution applies to LinkedIn and any platform without an official connector your bot can use: draft with the bot, post by hand.

### 5.3 Red flags: stop and review if any happen

- A reply gets reported, hidden, or ratioed for being promotional.
- Your account gets a warning, a rate limit, or a temporary restriction.
- The bot produces a URL that isn't in your brief.
- The scoreboard shows revenue you can't find as captured in your processor.

---

## Part 6: Weekend build plan (Saturday–Sunday)

Goal by Sunday night: **a live payment link, a configured bot, routines saved, and your first approved reply queue.** Times are suggestions. Shift the blocks to fit your weekend.

### Saturday: decide and set up

| Time | Task | Done when |
|---|---|---|
| 09:00–10:00 | **Pick the niche.** List 3–5 candidates. Run the niche filter prompt (4.1). Validate the winner by hand: 10+ real posts from the last 7 days. | One niche, written as one sentence |
| 10:00–11:00 | **Write the offer.** Run the offer writer (4.2). Decide the price and an optional premium tier. Cut every adjective you can. | Offer text with name, outcome, bullets, price |
| 11:00–12:30 | **Make the thing you're selling.** Version 1, not the final version: a playbook, a template pack, a checklist, a service slot. It has to be deliverable the moment someone pays. | The file or the service steps exist |
| 12:30–13:30 | Break. | |
| 13:30–14:30 | **Create the payment link** (Part 7). Make a test payment if your processor supports test mode, and check the receipt and redirect. | A live link that opens a real checkout |
| 14:30–15:30 | **Write the bot brief** (Part 1) using the template. Paste in your offer, your link, the never-claim list, and your voice. | Brief saved where your bot can read it |
| 15:30–16:30 | **Connect connectors** (Part 3). X and your payment processor at minimum. Set approval defaults. Tick every box in 3.2. | The bot can search X and read payments |
| 16:30–17:30 | **Write the kill rule** (4.5 and Part 8). Paste it into the brief. | A dated rule with numbers |
| 17:30–18:00 | **Write your fulfillment steps:** what you send, from where, within what time. Draft the delivery email (4.6). | A fulfillment checklist you can follow tired |

### Sunday: routines, first queue, launch

| Time | Task | Done when |
|---|---|---|
| 09:00–10:00 | **Create the routines** (Part 2): morning drafts, scoreboard, kill-rule check. Add the afternoon window and payment alert if you want them. | Routines saved with the right local times |
| 10:00–11:30 | **Run the first draft window manually.** Ask the bot to run Routine 1 now. Read every draft against the spam check (4.3). | 10–20 drafts reviewed |
| 11:30–12:30 | **Tune.** Tighten the niche filter, banned words, and CTA rules in the brief based on what was wrong with the drafts. Re-run the drafts if needed. | Drafts that you'd post without editing |
| 12:30–13:30 | Break. | |
| 13:30–15:00 | **Approve and post the first batch.** Start with 5–10, spaced out. Most should have no link. Reply to anyone who responds. | First replies live, all approved by you |
| 15:00–15:30 | **Pin or profile.** Put one clear line plus YOUR_PAYMENT_LINK in your bio or a pinned post, so people who click through to your profile can find the offer without you pushing it in replies. | Profile points to the offer |
| 15:30–16:30 | **Second batch.** Run Routine 1 again or wait for the afternoon window. Approve and post, staying under the daily cap. | Under 20 total today |
| 18:30–19:00 | **First scoreboard.** Run Routine 3. Record the baseline (almost certainly 0 captured). | Day-zero scoreboard saved |

**From Monday:** approve drafts in the morning window, reply to responses, read the scoreboard at night, and run the kill-rule check on its review date. Change one variable at a time.

---

## Part 7: Selling with Payment Links

### 7.1 Why a payment link instead of a checkout

You don't need a website, a cart, or a backend to take money. A hosted payment link gives you a checkout page, card/UPI/wallet handling, receipts, and a dashboard. You paste one URL into your bio and your replies. Build the website after someone has paid.

### 7.2 Razorpay example (adapt to your processor)

Any processor with hosted payment links works the same way: Razorpay, Stripe Payment Links, Lemon Squeezy, Paddle, PayPal, Gumroad, and others. Use the one that supports your country, currency, and buyers. Your link will be your own. Never copy anyone else's.

1. **Account:** sign up and complete KYC/activation. Live payments usually require an activated account, and this can take time, so start it first.
2. **Create the link:** Dashboard → Payment Links (or Payment Pages) → create. Set:
   - Title: YOUR_OFFER_NAME
   - Amount and currency: YOUR_PRICE (check whether you can accept international cards if your buyers are abroad)
   - Description: your one-liner
   - Customer fields: email, at minimum, so you can deliver
   - Reusable / multiple payments: **on** (a one-time link expires after the first payment)
   - Expiry: none, or after your kill-rule window
3. **Test:** use test mode for a dry run, then open the live link in a private browser window and check the title, amount, and currency.
4. **Save it:** paste the exact URL into your bot brief as `YOUR_PAYMENT_LINK`. This is now the only checkout link your bot may use.
5. **Verify payments:** in the dashboard (or via your payment connector), filter by your link and look at status. On Razorpay, **captured** is the status that counts. Created, authorized, and failed don't count.

### 7.3 Fulfillment (the part people forget)

Before the link goes live, decide:
- **What** the buyer gets (file, access link, booked call, service).
- **How** it reaches them (email from you, auto-redirect to a download, invite).
- **When** (state a realistic window, e.g. "within 12 hours", and keep it).
- **Refunds:** your policy, in one sentence, visible on the payment page if your processor allows it.

Manual fulfillment is fine for the first 10 sales. Automate after it hurts.

---

## Part 8: The kill rule

Most bots die slowly: no sales, but always one more feature to build. A kill rule written **before launch** turns a vague hope into a dated decision.

### 8.1 Template

```markdown
## KILL RULE: YOUR_OFFER_NAME
Launch date: YYYY-MM-DD
Review date: YYYY-MM-DD (launch + N days)

STOP if, on the review date:
- Captured payments = 0, AND
- I have posted at least M approved replies (with at least K containing a CTA)

PIVOT if:
- People engage (replies, questions, profile visits, link clicks if tracked) but captured payments = 0
  → change ONE of: offer framing, price, or niche segment, then restart a new N-day window
- Captured payments > 0 but below my CONTINUE threshold
  → keep the niche, rework the offer or the channel

CONTINUE if:
- Captured payments ≥ C in the window
  → run another window, and only now consider automation or a second offer

What does NOT count: followers, impressions, likes, "interested" DMs, created/authorized payments.
Who decides: me, on the review date, from the scoreboard, not from mood.
```

### 8.2 Choosing the numbers

- **N (days):** 7–14 days is a reasonable first window for a low-priced digital offer. Shorter windows don't give replies time to compound. Longer ones let you drift.
- **M (replies posted):** set it so that hitting zero sales is meaningful. For example, 10 replies a day for 7 days is 70. If you posted 12 replies and sold nothing, you didn't test the offer; you tested whether you'd do the work.
- **C (continue threshold):** your call. Pick a number that justifies another window of *your* time. Even a single captured payment from a stranger is a real signal worth noting.

These are starting points, not benchmarks. Nobody can tell you what conversion to expect for your niche, and anyone who claims to is guessing.

### 8.3 Pivot vs. start over

- **Pivot** = keep what showed signal and change one thing. If people engaged but didn't pay, the niche is probably real: change the offer or price first.
- **Start over** = no engagement *and* no sales after M replies. The niche or the channel is wrong. Go back to the niche filter.

---

## Part 9: Soft CTA patterns

A CTA earns its place only after the reply has already helped. One per reply, always last, always optional.

### 9.1 Patterns (replace placeholders, keep them short)

1. **Write-up:** "I wrote the whole process up as a YOUR_PRICE playbook if it's useful: YOUR_PAYMENT_LINK"
2. **Step-by-step:** "If you want the step-by-step version, it's here: YOUR_PAYMENT_LINK"
3. **Premium tier:** "There's also a version where I review your setup before you build: YOUR_PREMIUM_PAYMENT_LINK"
4. **All in one place:** "Happy to keep answering here. The full system is at YOUR_PAYMENT_LINK if you'd rather have it in one place."
5. **No link (ask first):** "I've got this written up as a playbook if you want it. Just say." Use this on Reddit, in communities that ban links, and anywhere a link would feel pushy.
6. **Profile pointer:** no link in the reply at all. Let the useful reply send people to your profile, where the pinned post or bio holds YOUR_PAYMENT_LINK.

### 9.2 When to use no CTA

- The person didn't ask for help. They're sharing news, a win, or venting.
- The thread is about grief, layoffs, health, or burnout.
- The community bans self-promotion.
- You've already linked to this person recently.
- Your tip is thin. Fix the tip first.

### 9.3 Never

- "DM me", "link in bio 🔥", "only 3 spots left", "this changed everything", "I made $X with this".
- A CTA as the first line.
- A link that isn't YOUR_PAYMENT_LINK exactly as it appears in your brief.

---

## Final checklist before you call it live

- [ ] Bot brief written, one page, with niche, one job, voice, never-claim list, success metric
- [ ] Offer written. Price set. Optional premium tier.
- [ ] Product version 1 exists and can be delivered today
- [ ] Payment link live, tested, saved in the brief as the only allowed link
- [ ] Fulfillment steps and delivery email drafted
- [ ] X + payment connector connected; draft-only approval default set
- [ ] Routines saved: morning drafts, scoreboard, kill-rule check (+ optional afternoon window and payment alert)
- [ ] Kill rule written, dated, pasted into the brief
- [ ] First batch of replies approved and posted, under the daily cap
- [ ] Day-zero scoreboard recorded: captured cash = 0

Then do the boring part every day: approve, reply, count, and decide on the date you set.

---

_Questions about this Blueprint: reply to the email it came with._
