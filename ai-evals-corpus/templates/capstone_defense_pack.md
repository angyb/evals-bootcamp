# Capstone defense pack

Your one-pager is `quality_strategy_template.md`. Its five sections are
your five slides, in order. This pack is everything around the slides:
what to say, what you will be asked, and how to rehearse it.

---

## The five slides

One per section. One slide each, and resist the urge to add a sixth.

| # | Slide | The sentence it has to earn |
|---|---|---|
| 1 | **Gates** | "Nothing ships past this bar, and here is the bar." |
| 2 | **Guardrails** | "Here is what intervenes at runtime, and what it costs in false positives." |
| 3 | **Drift** | "Here is how we find out the metric moved before a customer tells us." |
| 4 | **Incidents** | "Here is what happens the day it goes wrong." |
| 5 | **Ownership** | "Here is who can block a launch, and how the function is paid for." |

Every claim on every slide points at a Week 1, 2 or 3 artefact. Your
taxonomy, your calibrated judge, your red-team memo. A strategy with no
artefacts behind it is a slide about strategy.

---

## The elevator sentence

Write it before you write the slides. If you cannot say it in one
breath, the slides will not fix that.

> "We [gate on X] before merge, [guardrail Y] at runtime, and sample
> [N] traces a day so we find out about [failure Z] in hours instead of
> weeks. [Role] can block a launch."

Say it out loud. Time nothing, just notice whether you ran out of air.

---

## Three things that make a defense strong

Straight from what separates the good ones.

**A day in the life.** Not the architecture, the calendar. "Every week
the PM opens the dashboard, checks three numbers, and pulls twenty
traces." Concrete rituals survive questioning in a way that diagrams do
not.

**A specific incident you have actually thought about.** Take Air Canada,
Chevrolet, DPD or Samsung, and walk through what your stack does with it.
"Air Canada's agent invented a bereavement policy. Our groundedness gate
would have caught the invented figure at merge. Our segment alert would
have caught it in production within a day if it slipped." That is a
better answer than any general claim about rigour.

**One thing you are honestly uncertain about.** Name it yourself, before
anyone asks. "I do not have a good answer for indirect injection beyond
removing the outbound tool, and I think that is the weakest part of this."
Reviewers trust the person who found their own soft spot. It also steers
the hard questions toward the thing you have thought about most.

---

## The questions you will get

Instructors go first. Peers follow. Prepare an answer for each of these,
because most of them turn up in some form.

| # | Question | What it is really testing |
|---|---|---|
| 1 | "What is the first thing you would cut if you had half the budget?" | Whether you know your own priority order |
| 2 | "Your judge is 90% TPR at n=10 per arm. Would you bet the launch on that?" | Whether you understood the confidence interval |
| 3 | "This gate blocks my merge and I think it is wrong. What happens?" | Whether the override protocol is real |
| 4 | "Who decides when the metric drop is bad enough to roll back?" | Whether ownership is named or vague |
| 5 | "You sample 200 traces a day. Why 200?" | Whether the number came from anywhere |
| 6 | "What does this catch that a human reading transcripts would not?" | Whether the system earns its cost |
| 7 | "Your top failure mode is X. Show me the traces." | Whether the taxonomy is real |
| 8 | "What happens when the model version changes underneath you?" | Whether recalibration is scheduled |
| 9 | "Nothing has broken in two months. Is this still worth funding?" | The prevention paradox. Have an answer |
| 10 | "What would make you tell a VP not to ship?" | Whether you would actually use the authority |

### Answering one you cannot answer

You will get one. The move is not to bluff.

> "I do not have that. Here is how I would find out, and here is what I
> would do differently depending on the answer."

That answer scores better than a confident guess, in this room and in
every launch review afterwards. What loses points is inventing a number.

---

## Mock defense scorecard

Give this to your study partner. Fill it in for each other before the
defense session. Marking your own is not the same exercise.

**Presenter:** [name] · **Reviewer:** [name] · **Date:** [date]

| | Yes | Partly | No |
|---|---|---|---|
| Elevator sentence landed in one breath | | | |
| Every slide pointed at a real artefact | | | |
| Gates had a named threshold, not "high quality" | | | |
| Guardrails had a false-positive cost attached | | | |
| Drift had a number, a threshold and an owner | | | |
| Incident slide described a ritual, not a hope | | | |
| Ownership named who can block a launch | | | |
| Included a day-in-the-life example | | | |
| Named one honest uncertainty | | | |
| Answered the hard question without inventing a number | | | |

**The strongest thing in it:** [one sentence]

**The thing a reviewer will push on first:** [one sentence]

**One change before the real defense:** [one sentence]

---

## What happens to the recording

The defense is recorded, and the recording is the point as much as the
presentation is. You end the course with a version of yourself defending
a real artefact under questioning, which is closer to a frontier-lab
interview loop than anything you can rehearse alone. Keep it. Watch it
once before your next interview.
