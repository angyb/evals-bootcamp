# [Product] AI quality strategy — [date]

**Author**: [PM name]
**Weeks 1–3 artefacts**: [link to failure taxonomy] · [link to calibrated judge] · [link to red-team + launch memo]

## 1. Offline eval gates

- **Ship gate**: [Judge name] (TPR [X%] / TNR [Y%] on N=[Z] calibration set) at ≥ [threshold] pass rate on [regression set size]-item regression set.
- **Code graders**: [list — JSON schema, contains-not-'as an AI', word count]. All at 100% required.
- **CI**: gate on top [N] graders; override protocol = [Eng lead sign-off + reason logged].

## 2. Runtime guardrails

Layered request flow:
1. [Rate limiter → threshold]
2. [PII scrubber (in) → what fields]
3. [Input filter → what patterns]
4. Model call
5. [Tool-call whitelist → which tools allowed]
6. [Output validator → schema + moderation]
7. [PII scrubber (out) → what fields]

FP-rate SLO per guardrail: < [X]% of legitimate requests blocked.

## 3. Drift + monitoring

- **Sample size**: [N] traces/day stratified across [segments].
- **Alert threshold**: [N%] drop week-over-week OR 2σ from 30-day mean.
- **Dashboard metrics**: top-line pass rate, segment breakdowns, cost p50/p95, latency p50/p95, guardrail activity, judge non-determinism.
- **Weekly review**: [day, time, owner]. 15 minutes. 3 questions: any metric moved >3%? any new segment to investigate? any open incidents?

## 4. Incident review

- **Cadence**: P0 same-week, P1 within a month, P2 batched quarterly.
- **Template**: 5-question review (what happened / how detected / failure mode / would-have-caught / changing).
- **Owner**: [role].
- **Escalation**: P0 → [role] within [hours]; P1 → [role] within [days].

## 5. Ownership

**Pattern**: [PM-embedded / central evals team / safety org].
**Authority**: [who can block a launch].
**Funding case**: [1-sentence — headcount + funding source + ROI].

---

## Day in the life

Monday 9am: [PM opens dashboard, checks 3 metrics].
Tuesday: [judge sample review — 30 min].
Thursday weekly review: [PM + eng lead — 15 min].

## If Air Canada / Chevrolet / DPD shipped on our stack

[1 paragraph — how our monitoring / guardrails / gates would have caught it, and how fast.]
