# Regression gates

Two files. Copy both, change the rows, ship it.

| File | Goes where |
|---|---|
| `promptfooconfig.yaml` | `regression_gates/promptfooconfig.yaml` in your repo |
| `evals.yml` | `.github/workflows/evals.yml` in your repo |

Run it locally first:

```bash
export OPENAI_API_KEY=sk-...
npx promptfoo@latest eval --config regression_gates/promptfooconfig.yaml
npx promptfoo@latest view
```

---

## What to gate

A gate answers one question: **would this change ship a failure we have
already decided we will not ship?** If a row does not answer that, it is
a dashboard metric, not a gate.

Gate these:

- **Duty of care.** Crisis escalation, safety routing. Highest threshold
  in the file, and the one row you never override.
- **The top two or three failure modes from your Week 1 taxonomy.** You
  ranked them by severity times frequency. Gate the top of that list.
- **Anything that has already caused an incident.** One row per incident,
  named after it. This is how a review turns into a control.
- **Deterministic invariants.** JSON parses, required fields exist, the
  forbidden string is absent. Cheap, fast, no flake, no judge cost.

## What not to gate

- **Tone and style.** Real, worth measuring, wrong place. It will block
  merges over taste and the team will learn to override reflexively.
- **Anything with a judge below about 85% TPR and TNR.** A gate is only
  as trustworthy as the judge behind it. Week 2 gave you those numbers;
  if the judge is not there yet, this row is not ready to block anyone.
- **Long-tail edge cases.** They belong in the wider offline suite you run
  nightly, not in the path of every pull request.
- **Anything you cannot explain to the person whose merge it blocked.**
  If you cannot say in one sentence why the row exists, it will be
  overridden and it should be.

## Order the assertions cheap-first

Deterministic assertions run first in each test above. They cost nothing,
they never flake, and when one of them catches the regression you have
saved a judge call and produced a much clearer failure message than a
rubric score.

## The threshold

Start at the pass rate you currently hold, not at the one you want.
A gate set above where you actually are is overridden on day one, and a
gate that is routinely overridden is a notification with extra steps.

Ratchet it upward as the suite gets better. Ratcheting down is a decision
someone should have to argue for out loud.

## The override protocol

At the bottom of `evals.yml`, and it matters more than the config above
it. Every gate gets overridden eventually. The question is whether the
override leaves a trace.

Audit the `eval-override` label monthly. A row overridden twice is either
a wrong row or a wrong gate, and it is worth ten minutes to find out
which.
