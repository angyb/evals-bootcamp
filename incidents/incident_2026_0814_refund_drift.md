# Incident INC-2026-0814 · refund guidance widened without a code change

> **Fictional incident, written for the Week 4 live session.** CloudApp is
> synthetic. Every name, figure and timestamp below is invented. Use it to
> run the five-question review together, then run the same template on a
> real incident from your own product.
>
> Read this before the session. Do not draft the review yet.

---

## What people saw first

A support lead posted in `#cloudapp-support`:

> "Third customer this week saying we promised them a refund on an annual
> plan past day 30. I keep having to walk it back. Did policy change?"

Policy had not changed. KB section 2 still reads: annual plans are
pro-rated in the first 30 days only, no refund after day 30.

## Timeline

| When | What happened |
|---|---|
| Day 0 | A prompt change ships. One line added to the support agent's system prompt: "Be warm and solution-oriented. Look for a way to help before declining." Intent was tone. It passed review in under an hour. |
| Day 0 | CI ran. All code graders green. The groundedness judge ran on the 30-item regression set and returned 93% pass, above the 90% gate. Merged. |
| Day 1 to 5 | Top-line judge pass rate on sampled production traffic sits between 91% and 93%. No alert fires. The threshold is a 5% week-over-week drop on top-line. |
| Day 6 | Support lead posts in Slack. Not an alert, a human noticing a pattern. |
| Day 6 | Someone segments the dashboard by intent for the first time in three weeks. Billing-intent pass rate is 71%, down from 94%. Annual-plan billing traces are at 58%. |
| Day 7 | Prompt line reverted. Billing pass rate returns to 93% within a day. |
| Day 7 to 9 | Manual review of 6 days of billing traces. 41 conversations where the agent offered or implied a refund that KB section 2 does not support. 12 customers had already been told yes. |

## The evidence

Sampled trace from day 3, `trace_prod_88412`:

```
User:   I bought the annual plan back in March and I'm not using it.
        Can I get a refund?

Agent:  I completely understand, and I want to find a way to help here.
        While our standard annual refund window is 30 days, let me see
        what I can do for you. I can put in a request for a pro-rated
        refund on the unused months. You should hear back within 3 to 5
        business days.
```

Retrieved context available to the agent at the time:

```
KB §2: Annual plans: pro-rated refund available in the first 30 days
       only. After day 30, no refund on annual plans.
```

The groundedness judge scored this **PASS**.

## Why the judge passed it

The judge's rubric asked: *does the response quote a refund window that
appears verbatim in a retrieved chunk?*

The agent quoted "30 days" correctly. It then offered something the chunk
does not support, in a separate sentence, using hedged language. The
rubric had no clause for offers, only for quoted figures. The judge did
what it was asked. The rubric was asked the wrong question.

## Impact

- 41 conversations with unsupported refund guidance.
- 12 customers told yes before anyone noticed.
- Finance honoured all 12. Roughly $2,300.
- One customer quoted the agent transcript back in a chargeback dispute.
- Six days between ship and detection. Detection was a human in Slack,
  not a system.

## What was already in place

- A calibrated groundedness judge, TPR 90%, TNR 85% at n=10 per arm.
- A 30-item regression set, gated in CI at 90%.
- A production sampling job, 200 traces per day.
- A daily dashboard with top-line pass rate.
- A weekly review that had not run for two weeks. Both owners were on leave.

Everything on that list is a real control. The incident happened anyway,
which is the point of reviewing it.

---

## For the session

Do not skip to the fix. Work the five questions in order. The most useful
disagreement in the room is usually about question 3, because "the failure
mode" can be honestly named at four different layers here, and which layer
you pick decides what you change.
