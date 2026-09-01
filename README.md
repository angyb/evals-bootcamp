# AI Evals Bootcamp — sample corpus

Everything you need to work through the bootcamp when you can't use your own
production traces (NDA, PII, product not live yet). Fully synthetic — safe
to paste anywhere, including into public LLM APIs.

All traces come from a deliberately-broken B2B SaaS support agent
`CloudAppSupport-v0.3`. The failure modes are calibrated to match what real
production support agents actually break at.

## Files

| File | What it's for | Rows |
|---|---|---|
| `traces.jsonl` | The main trace corpus — open-code these in Week 1 | 103 |
| `knowledge_base.md` | The 'docs' the agent was grounded on — use for groundedness checks | — |
| `ground_truth_labels.csv` | Labels for the first 20 traces — Week 2 calibration seed | 20 |
| `safety_cases.jsonl` | Red-team attack prompts + expected behaviour — Week 3 sweep | 18 |
| `poisoned_knowledge_base.md` | The KB with 7 planted attacks — Week 3 Round 2 | — |
| `redteam_attack_playbook.md` | The 8 attack classes, organised into the 3 live rounds | — |
| `pre_course_smoke.jsonl` | 5-row categorization smoke test — pre-course dashboard verification | 5 |
| `part3_categorization.jsonl` | Small categorization dataset from the workshop | 5 |
| `part3_hard_cases.jsonl` | Adversarial categorization examples | 3 |
| `part4_email_quality.jsonl` | Email-quality rubric dataset for LLM-as-judge exercises | 5 |
| `part6_agent_transcripts.jsonl` | Multi-turn agent transcripts for Week 3 red-team | 5 |
| `incidents/` | Fictional incidents for review practice — Week 4 | 1 file |
| `regression_gates/` | promptfoo config + GitHub Actions workflow — Week 4 | 3 files |
| `templates/` | Copy-paste templates for every portfolio artefact | 15 files |
| `generate_corpus.py` | Deterministic generator — regenerates every file above | script |

## Templates

| File | What it's for | Used in |
|---|---|---|
| `open_coding_template.csv` | One row per code, anchored to a trace | Week 1 |
| `prioritization_memo_template.md` | The one-page memo to an engineering lead | Week 1 |
| `judge_rubric_template.md` | The rubric itself, plus a short trust summary | Week 2 |
| `judge_prompt_template.txt` | The runnable judge prompt shell, in four pieces | Week 2 |
| `gold_set_labeling_sheet.csv` | 20-item human gold set, blind-label column order | Week 2 |
| `when_to_trust_me_template.md` | The standalone judge one-pager, with CI lookup | Week 2 |
| `calibration_template.csv` | Side-by-side human vs judge, once labeling is done | Week 2 |
| `rules_of_engagement.md` | Scope, safety limits, what counts as a finding | Week 3 |
| `redteam_findings_log.csv` | 30-row attack log, evidence-before-scoring order | Week 3 |
| `severity_scoring_rubric.md` | 1 to 5 anchors + the ship / hold / block matrix | Week 3 |
| `incident_review_5q_template.md` | The five-question blameless AI postmortem | Week 4 |
| `capstone_defense_pack.md` | Five-slide map, question bank, mock-defense scorecard | Week 4 |
| `quality_strategy_template.md` | The capstone strategy doc | Week 4 |
| `launch_memo_template.md` | Ship / no-ship recommendation | Week 4 |
| `pre_course_checkin_template.md` | Pipeline smoke-test writeup | Pre-course |

### Which Week 2 sheet do I use?

`gold_set_labeling_sheet.csv` first, then `calibration_template.csv`.

The gold sheet orders its columns human-first so you fill it
left-to-right and finish the human pass before the judge columns are
in front of you. That is the blind-label discipline. The calibration
template puts human and judge side by side, which is the right shape
for reviewing agreement after both passes exist, and the wrong shape
for labeling.

## Trace schema (`traces.jsonl`)

Each row is a single trace with the following fields:

```json
{
  "trace_id": "trace_037",
  "timestamp": "2026-08-08T14:23:00Z",
  "user_id_hash": "u_ab12cd34",
  "channel": "email | chat | api",
  "intent": "billing | how_to | bug_report | escalation | prompt_injection | ...",
  "input": "user message text",
  "retrieved_context": ["KB §2: ...", "..."],
  "tool_calls": [{"tool": "lookup_account", "args": {}, "result": "..."}],
  "output": "agent's final response to user"
}
```

Nothing in the trace tells you the intended failure mode — that's the whole
point of open coding. `ground_truth_labels.csv` reveals the intended
failure mode for the first 20 traces after you've open-coded them yourself.

## Failure-mode distribution (103 rows across 100 scenarios)

- 30 clean baseline
- 15 hallucinated policy / ungrounded confident claim
- 10 tone mismatch
- 10 format drift / schema violation
- 8 over-refusal
- 5 under-refusal
- 8 prompt-injection attempts (direct + indirect + tool poisoning)
- 5 groundedness / citation issue
- 4 system-prompt leak attempts
- 6 goal hijacking (3 multi-turn scenarios × 2 turns each)
- 2 PII exposure

## How to use

- **Pre-course**: run `pre_course_smoke.jsonl` through the OpenAI Evals dashboard
  to confirm your pipeline works end-to-end.
- **Week 1**: open-code all 100 traces in `traces.jsonl` using the
  `open_coding_template.csv`, produce your ranked taxonomy + memo.
- **Week 2**: use the first 20 traces as your calibration set for the LLM
  judge; `ground_truth_labels.csv` is your reference. Extend with your own
  labels for another 10.
- **Week 3**: read `templates/rules_of_engagement.md` before anything else.
  Work the rounds in `redteam_attack_playbook.md`, using
  `safety_cases.jsonl` as starter payloads and `poisoned_knowledge_base.md`
  for the indirect-injection round. Log every attempt in
  `templates/redteam_findings_log.csv`, score with
  `templates/severity_scoring_rubric.md`, then write
  `templates/launch_memo_template.md`.
- **Week 4**: run `templates/incident_review_5q_template.md` on
  `incidents/incident_2026_0814_refund_drift.md`, wire up
  `regression_gates/`, then write `templates/quality_strategy_template.md`
  as your capstone one-pager and rehearse with
  `templates/capstone_defense_pack.md`. Cite specific `trace_XXX` IDs
  throughout so every claim is defensible.

## Regenerate

```bash
python3 generate_corpus.py
```

Deterministic — every regen produces byte-identical files. Modify the script
to add / adjust failure modes for future cohorts.

## Licence

Do whatever you want with this. It's fake data.
