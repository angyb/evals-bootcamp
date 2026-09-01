# When to trust me

**Judge name:** [name]
**Rubric version:** [v1 / v2 / v3]
**Written by:** [you]
**Last calibrated:** [date]

> Every judge ships with one of these. One page. If someone downstream
> is going to act on this judge's output, they get to read this first.
>
> Fill sections 1, 2 and 4 during the live session. Sections 3 and 5
> need your homework numbers.
>
> Related templates: `judge_rubric_template.md` holds the rubric itself
> and a short trust summary. This doc is the standalone one-pager you
> hand to someone else. If they disagree, this file wins.

---

## 1. What this judge decides

[One sentence. What question does it answer, on what kind of input?]

*Example: Judges whether every policy figure in a support response
appears in a retrieved context chunk.*

**What a PASS means:** [one sentence]
**What a FAIL means:** [one sentence]

---

## 2. Rubric

Verbatim. Not a summary. If the rubric changed, this section changes
and every number in section 3 is void until you re-run.

```
[Paste the rubric exactly as it appears in the judge prompt.
Question, definition, edge case, out-of-scope.]
```

**Prompt file:** `judge_prompt_template.txt`, version [vN]
**Model + settings:** [model name, temperature, any other setting that moves the output]

---

## 3. Calibration

### The set

| | |
|---|---|
| Gold set size | [N] items |
| Human PASS items | [N] |
| Human FAIL items | [N] |
| Where the items came from | [traces.jsonl rows / your own production traces / other] |
| Sampled how | [random / stratified / all of a segment. Say if you cherry-picked. Cherry-picking is not a crime, hiding it is.] |
| Labeled by | [who, and why they are the domain expert for this category] |
| Labeled blind | [yes / no. If no, the numbers below are optimistic and you should say so out loud.] |

### The numbers

| Metric | Count | Rate | 95% CI | Ship bar | Pass? |
|---|---|---|---|---|---|
| **TPR** (human PASS, judge agreed) | [k] / [n] | [X%] | [lo% to hi%] | ≥ 85% | [yes/no] |
| **TNR** (human FAIL, judge agreed) | [k] / [n] | [X%] | [lo% to hi%] | ≥ 85%, or ≥ 95% for legal, safety, medical | [yes/no] |

**Report the interval, not the point estimate.** A judge that scored
9/10 did not score 90 percent. It scored somewhere between 60 and 98
percent, and you do not get to pick which.

### Read your interval off the table

Important: TPR is computed only on your human-PASS items, and TNR only
on your human-FAIL items. A 20-item gold set split 10/10 gives you
**n = 10 for each rate**, not 20. Use the n=10 table unless you labeled
more.

**n = 10** (a 20-item gold set split 10 PASS / 10 FAIL)

| Agreed | Rate | 95% CI |
|---|---|---|
| 5/10 | 50% | 24% to 76% |
| 6/10 | 60% | 31% to 83% |
| 7/10 | 70% | 40% to 89% |
| 8/10 | 80% | 49% to 94% |
| 9/10 | 90% | 60% to 98% |
| 10/10 | 100% | 72% to 100% |

**n = 20** (you labeled 40 items, or you are reporting a combined rate)

| Agreed | Rate | 95% CI |
|---|---|---|
| 10/20 | 50% | 30% to 70% |
| 12/20 | 60% | 39% to 78% |
| 14/20 | 70% | 48% to 85% |
| 15/20 | 75% | 53% to 89% |
| 16/20 | 80% | 58% to 92% |
| 17/20 | 85% | 64% to 95% |
| 18/20 | 90% | 70% to 97% |
| 19/20 | 95% | 76% to 99% |
| 20/20 | 100% | 84% to 100% |

Wilson score intervals. If you want another n, the formula is in any
stats reference under "Wilson score interval"; do not use the naive
normal approximation at these sample sizes, it lies near 0 and 100.

**What this means in one sentence:**
[Write it. "At n=10 per arm I cannot distinguish an 85% judge from a
70% judge, so the ship-bar call is provisional until I label 30 more."
That kind of sentence.]

---

## 4. Known limits

**Categories this judge does NOT cover:**
- [category], owned by [other judge / nobody yet]
- [category]

**Do not use this judge for:**
- [input type or segment where you know it degrades]

**Biases checked:**

| Bias | Checked? | What I found |
|---|---|---|
| Verbosity (longer answers score better) | [yes/no] | [finding] |
| Position (order of examples moves the label) | [yes/no] | [finding] |
| Self-preference (favours output from its own model family) | [yes/no] | [finding] |

**Disagreements I could not resolve:**
- [item id]: [one sentence on why the rubric still cannot settle it]

An unresolved disagreement listed here is a stronger artefact than a
clean sheet. It tells the reader where the judge is soft.

---

## 5. Rerun cadence

Recalibrate when any of these happen. Until you do, the numbers in
section 3 are historical, not current.

- [ ] The rubric changes, at all, including wording
- [ ] The judge model version changes
- [ ] A new failure category is added upstream
- [ ] The input distribution shifts (new customer segment, new channel, new locale)
- [ ] [N] weeks pass with no rerun. Pick a number: [ ]

**Last rerun:** [date] · **Next scheduled:** [date] · **Owner:** [name]

---

## Sign-off

I have read the limits in section 4 and I am acting on this judge's
output anyway, with those limits in mind.

| Name | Role | Date |
|---|---|---|
| | | |
