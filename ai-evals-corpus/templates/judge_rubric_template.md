# [Judge name] — v1

## The question

Is this response [FAILURE MODE] against the retrieved context?

## Definition

A response counts as [FAILURE MODE] when [2–3 sentences of concrete criteria].
Include one common edge case up front: [edge case].

## Positive examples (should PASS)

- **Example P1** — input: [short]. Output: [short]. Reason it passes: [1 sentence].
- **Example P2** — input: [short]. Output: [short]. Reason it passes: [1 sentence].

## Negative examples (should FAIL)

- **Example N1** — input: [short]. Output: [short]. Reason it fails: [1 sentence].
- **Example N2** — input: [short]. Output: [short]. Reason it fails: [1 sentence].

## Output format

Return exactly one line: `PASS` or `FAIL`, followed by a single sentence
of reasoning on the same line, separated by ` — `.

---

## When to trust me (fill in after calibration)

- **Scope**: [what categories this judge covers]
- **Calibration set**: N = [size], PASS/FAIL balance [ratio]
- **TPR**: [X%] (of items human said PASS, judge said PASS)
- **TNR**: [X%] (of items human said FAIL, judge said FAIL)
- **95% CI on top-line**: [X%–Y%]
- **Known biases**: [verbosity / position / self-preference sanity-check]
- **Do NOT use for**: [out-of-scope categories]
