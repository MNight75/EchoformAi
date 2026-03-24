# Text-to-Invoice: Roy as Proof-of-Concept (Plan 27)

## What We Sell
A text-based AI assistant that turns a plumber's job notes into professional invoices, customer SMS reminders, and weekly revenue summaries — no app, no portal, just texts.

## Who Pays
Small plumbers/HVAC/electricians who invoice manually (whiteboard, notepad, generic emails). $49/month after free trial.

## Why They Pay
- Currently: "I text the customer a price, they venmo me, I forget to track it"
- After: Forward the job text to Echoform → receive a clean invoice → forward to customer → done
- Time saved: 5 min/job × 15 jobs/week = 75 min/month

## Simplest Version (launch in 1 week with Roy)
1. Roy texts Echoform after each job: "bathroom sink, Smith, $185"
2. Echoform replies with a formatted invoice text
3. Roy copies/pastes to customer
4. Done.

That's it. No Stripe, no portal, no app.

## Blocker
Roy needs to actually text his first job. That's it. Everything else is built.

## First Step
Ask Roy one question: "After your next job, text me the basics — customer name, job type, price. I'll send you back a professional invoice you can copy-paste." That's the entire onboarding.

## Revenue Model
- Roy uses it free → proves it works → becomes testimonial
- Roy tells 3 plumber friends → 3 trials
- 1 of 3 pays ($49/month) → first revenue
- 5 paying clients → $245/month
- 10 → $490/month

## Competitive Edge
No one is selling "AI business assistant for tradespeople via text." QuickBooks is $30-60/month + setup hell. This is $49/month and works from any phone.

## Why This Works Now
Roy is in TurboTax season — he's thinking about revenue, expenses, and money right now. This is the perfect time to show him what an AI business assistant actually looks like for his real business.

## The Deeper Insight
Every plan we've developed hits "needs payment rails" as the blocker. Plan 25 is different: Roy texts a job → gets invoice back → sends to customer → customer pays Roy's existing Venmo. **Zero new payment infrastructure needed for proof-of-concept.** The moment Roy says "this works, my customer paid me from an invoice I sent in 10 seconds," we have our first case study.

## Next Phase (after Roy's first successful invoice)
- Add customer text-back capability (customer replies "yes" → log as paid)
- Weekly summary text to Roy (total jobs, total revenue)
- Then: automated reminder texts for overdue invoices
- Then: package as "Plumber's Kit" for Roy's network
