# Plan 14: Text-Native Back Office for Trades

## What We Sell
A phone-based AI receptionist and ops assistant for small trade businesses. Roy texts or calls Echoform with job details after completing work. Echoform formats invoices, sends customer SMS updates, tracks jobs in a simple spreadsheet, and sends Roy a daily summary — all via text. No new software for the plumber to learn. No integrations to build.

## Who Pays
Solo or two-person trade businesses (plumbers, HVAC, electricians) who are drowning in admin but won't learn new software. They already use their phone for everything. They want someone (something) to handle the "after the job" workflow without them lifting a finger.

**Specifically:** Roy's Pro Drain AK, then 2-3 other plumbers in his network.

## Why They Pay
Every plumber finishes a job exhausted, dirty, and does not want to:
- Write up the invoice
- Text the customer the quote
- Follow up on late payments
- Send a "did you need anything else?" check-in

They'd rather pay $150/month to have that handled than spend their evenings doing paperwork. They want to do plumbing, not office work.

## The Insight That Unblocks This

The blocker in prior plans was "what scheduling software does Roy use?" — but that's the wrong question. **The right question: what does Roy already do on his phone?**

He probably:
- Texts customers directly from his phone
- Writes invoices (maybe in an app, maybe on paper)
- Gets paid via check or cash app

If we can intercept that workflow via TEXT — have Roy forward customer texts to Echoform, have Echoform draft responses, have Echoform maintain a job log — we can build a back office without touching any existing system.

**Text is the API.**

## Simplest Version

**The Echoform Text Hook:**
1. Roy configures a Google Voice number (or uses his existing) and forwards job-related texts to Echoform via email-to-gateway or similar
2. After each job, Roy texts Echoform: "Job done at 123 Main St, replaced water heater, $450, customer owes $200"
3. Echoform:
   - Logs the job in a shared Google Sheet
   - Texts the customer: "Hi, this is from Pro Drain AK — your job is complete. Here's your invoice: $200 due. Pay via [Venmo/PayPal link]. Thanks for your business!"
   - Adds the job to Roy's daily summary
   - Sends Roy a end-of-day summary: "3 jobs today, $1,200 total, $400 outstanding"
4. Customer replies to Echoform's text with payment confirmation or questions
5. Echoform handles FAQs, escalates payment issues to Roy

**Cost:** Twilio account for ~$1/month in phone numbers + usage. Google Sheet is free. No merchant account needed for now — customers pay Roy directly via his existing Venmo/cashapp.

**Revenue:** $150/month per business for daily ops coverage.

## Blocker
**Roy's participation in setup.** We need him to spend 30 minutes configuring a Google Voice number (or equivalent) and establishing the text-forwarding workflow. This is a one-time config that takes more than zero effort from him.

**Trust:** Roy needs to trust that Echoform won't mess up customer texts. Solution: start with a low-stakes workflow (job logging + daily summary) before live customer SMS.

## First Step
Ask Roy: "What do you currently do after a job to notify the customer and track the invoice? Do you text them directly? What does that message say?"

This tells us exactly what we're replacing and what the current workflow looks like. From there, we can design the Echoform layer on top.

## Revenue Model
- **Phase 1:** Free for Roy, proof of concept. We get: working workflow, real data, testimonial.
- **Phase 2:** Offer to 2-3 other plumbers Roy knows: $150/month for unlimited job logging + daily summaries + customer SMS draft generation.
- **Phase 3:** $300/month for full customer SMS lifecycle (appointment reminders → job confirmation → invoice → follow-up → review request).

**Target:** 3 plumbers × $150 = $450/month recurring. Not life-changing money, but real and recurring.

## Why This Works for Roy Specifically

Roy is in TurboTax season RIGHT NOW — he has no bandwidth for a big setup project. But the text workflow is so minimal that it could theoretically be tested THIS WEEKEND with zero disruption:
- He texts Echoform after each job instead of whatever he currently does
- Echoform handles the rest
- If it works, it reduces his evening admin load immediately
- If it doesn't, we've lost 30 minutes of his time

## Competitive Edge

No automation tool targets the solo plumber who won't learn new software. Jobber, Housecall Pro, and similar are full platforms with subscriptions, training, and onboarding. They require the plumber to change how they work.

**We're different:** We meet the plumber where they already are (texting) and handle the admin so they don't have to think about it.

## What We Need from Roy
1. A 10-minute conversation about his post-job workflow (what he does now, in detail)
2. Willingness to text Echoform after jobs for a 2-week test period
3. Permission to use his business as a case study (anonymized if needed)

## Sample Daily Summary (what Roy would receive)

```
📋 PRO DRAIN AK — End of Day Summary
Date: 2026-03-22

Jobs Completed: 3
  ✓ 123 Main St — Water heater replacement, $450
  ✓ 456 Oak Ave — Drain clog clear, $125
  ✓ 789 Elm Blvd — Inspection + quote, $0 (follow-up pending)

Revenue Today: $575
Outstanding: $200 (456 Oak Ave)

Customer Texts Sent: 3
Replies Received: 1 (789 Elm Blvd — requested quote by 3/26)

Tomorrow's Schedule: [Empty — no jobs scheduled]
```

## Next Question to Answer
What does Roy currently do after a job? Until we know that, we're designing blind. This plan goes to the bottom of the stack until Roy answers this one question.
