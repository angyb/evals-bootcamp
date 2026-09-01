# [Product] launch decision — [date]

**Decision requested:** SHIP / SHIP with monitoring / HOLD / BLOCK
**Recommender:** [PM name]
**Reviewers:** [Eng lead, Safety lead, Legal (if applicable)]

## Evidence

Ran red-team against [N] attack classes. [N] attack prompts × 3 runs each = [N] traces analysed.

| Class                       | Success rate | Sev × BR | Residual |
|-----------------------------|--------------|----------|----------|
| Direct injection            | X/Y          | S × BR   | R        |
| Indirect injection (RAG)    | X/Y          | S × BR   | R        |
| Goal hijacking              | X/Y          | S × BR   | R        |
| Tool poisoning              | X/Y          | S × BR   | R        |
| Data exfiltration           | X/Y          | S × BR   | R        |
| System prompt leak          | X/Y          | S × BR   | R        |

Full findings + attack prompts: [link to sheet]

Findings mapped to: OWASP LLM Top 10 (LLM01, LLM02, LLM06), MITRE ATLAS ([tactics]).

## Mitigations proposed (this sprint)

- **[Class] (P0)**: [specific mitigation pattern]. Est: [N] eng-days.
- **[Class] (P1)**: [specific mitigation]. Est: [N] eng-days.
- **[Class] (P2)**: [specific mitigation]. Est: [N] eng-days.

## Recommendation

**[SHIP / SHIP with monitoring / HOLD / BLOCK]** for [primary reason].

Timeline: mitigations land in [N] eng-days → re-run red-team → ship [N] days from decision.

## Alternatives considered

- **[Alternative 1]**: rejected. [Why — cite the residual risk delta.]
- **[Alternative 2]**: rejected. [Why.]
