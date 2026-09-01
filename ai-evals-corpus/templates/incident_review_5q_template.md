# AI incident review · five questions

**Incident:** [ID and one-line title]
**Date of incident:** [date] · **Date of review:** [date]
**Severity:** P0 / P1 / P2 · **Author:** [name] · **Attendees:** [names]

> Blameless. The output of this review is a change to a system, never a
> change to a person's standing. If a name appears below, it appears as a
> role, and the finding is about what the role could see, not about
> judgement.
>
> Work the questions in order. Question 5 is where people want to start
> and it is the one that goes wrong if you start there.

---

## 1. What happened

Plain narrative. What the system did, what the user experienced, over
what period. No causes yet, no blame, no fix.

[Two or three paragraphs.]

**Impact, in numbers:**

| | |
|---|---|
| Conversations affected | [N] |
| Users affected | [N] |
| Money, if any | [amount] |
| Time from ship to detection | [duration] |
| Time from detection to mitigation | [duration] |

Those last two rows are the ones that predict your next incident.

---

## 2. How was it detected

Be honest about this one. Most AI incidents are detected by a human
noticing a pattern, not by a system firing.

- **Detected by:** [alert / dashboard / support escalation / customer / social media / internal Slack]
- **Detected on:** [date, and how long after it started]
- **Should have been detected by:** [the control that existed and did not fire]
- **Why it did not fire:** [one paragraph]

**The question worth sitting in:** if this had been ten times smaller,
would anything have caught it? If the answer is no, your detection floor
is set by whatever a human happens to notice, and that is the finding.

---

## 3. What was the failure mode

Name it at every layer it is true, then pick the one you are going to act
on. Most AI incidents are honestly describable at four layers, and teams
argue past each other because they are each standing on a different one.

| Layer | Was it true here? | Notes |
|---|---|---|
| **Model** | [yes/no] | The model behaved differently than expected |
| **Prompt** | [yes/no] | The instruction produced a behaviour nobody intended |
| **Eval** | [yes/no] | A grader or rubric measured the wrong thing, or nothing |
| **Process** | [yes/no] | A ritual, gate or review that exists did not run |

**The layer we are acting on:** [pick one and say why]

Picking a layer is a real decision, not a formality. Act on the prompt
and you fix one line. Act on the eval and you fix a class. Act on the
process and you fix the next three incidents you have not had yet.

**Which failure category from your Week 1 taxonomy is this?**
[Name it. If it is not in the taxonomy, that is itself a finding, and
your taxonomy needs a new row.]

---

## 4. What would have caught it

For each control, say whether it existed, whether it fired, and why not.

| Control | Existed? | Fired? | Why not |
|---|---|---|---|
| Offline eval on the regression set | | | |
| CI gate before merge | | | |
| Runtime guardrail | | | |
| Production sampling + judge | | | |
| Segment-level alerting | | | |
| Weekly review ritual | | | |
| Human escalation path | | | |

**The cheapest control that would have caught it:** [name it, and cost it
in eng-days]

That row is the one that goes in the launch review the next time somebody
asks why the evals function needs headcount. A named incident with a
costed control that would have prevented it is the strongest funding
argument available to you, and it is worth more than any slide about best
practice.

---

## 5. What are we changing

Not "we will be more careful." A change is something with an owner, a
date, and a way to tell whether it happened.

| Change | Layer | Owner | By when | How we know it landed |
|---|---|---|---|---|
| | | | | |
| | | | | |
| | | | | |

**What we are explicitly NOT changing, and why:**
[Say this out loud. A review that only adds controls will eventually
produce a system nobody can ship through, and the discipline of naming
what you are leaving alone is what keeps that from happening.]

**Re-run date:** [when you check the changes actually worked]

---

## The one paragraph that goes to leadership

[Three or four sentences. What happened, what it cost, what changes,
when it is verified. Written so somebody who was not in the room can
read it once and know whether to worry.]
