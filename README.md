# Maat — Anti AI Slop Skill for Claude Code

Audit AI slop in business artifacts: strategic reports, M&A memos, board decks, RAG pipelines, and prompt libraries. A Claude Code skill that detects untraceable claims, fake authority, lost uncertainty, missing counter-analysis, and prompt bias in AI-generated or AI-assisted documents.

> The problem is not that AI hallucinates. The problem is that organizations hallucinate that they are informed.

## Why "Maat"?

In Egyptian cosmology, Maat is the goddess of truth, balance, and cosmic order — the principle that weighs the heart of the dead against a feather. Lighter than the feather, you pass. Heavier, you don't.

The premise of this skill: AI slop is what happens when organizations stop weighing claims against evidence and start trusting fluent prose. Maat audits the gap between *what looks verified* and *what actually is*.

## What it audits

Any artifact where AI was used to produce, summarize, or inform business output:

- Strategic reports, M&A memos, investment theses, board decks
- Market analyses, due diligence, competitive intelligence
- Internal RAG pipelines and curated knowledge bases
- Prompt libraries used for recurring decisions
- Meeting summaries that fed a decision

## The 10 Maat principles

1. **AI is not the source.** Never cite ChatGPT/Claude/Gemini as ground truth.
2. **Every strategic claim needs traceability.** Where, who, when, definition, contradicting evidence, dependent decision.
3. **Separate draft / analysis / approved truth.** Three documental states, never mixed.
4. **Expert review = truth, not style.** Premises, data, omissions — not commas.
5. **Govern prompts, not just outputs.** A prompt is a research question.
6. **RAG only on curated knowledge.** Versioned, dated, owned, deprecated marked.
7. **Uncertainty must survive the summary.** Known vs believed vs unknown.
8. **Strategic decisions require counter-analysis.** "Why this could be wrong" is mandatory.
9. **Separate generative AI from decision AI.** Different risk, different controls.
10. **Periodic audit of production outputs.** Real error rate, sampled, not perceived.

## Install

```bash
mkdir -p ~/.claude/skills
ln -s "$PWD" ~/.claude/skills/maat
```

Then in Claude Code: `/maat <file-path-or-text-or-url>`

## Output

The skill produces:

- **Executive verdict** (SLOP CRÍTICO / MODERADO / RIESGO BAJO / LIMPIO)
- **Per-principle audit** (PASS/WARN/FAIL with literal evidence)
- **Top 5 dangerous claims** table
- **Counter-analysis** (auto-generated when missing)
- **Maat score 0–10** in a machine-readable `MAAT_REPORT` block at the end

### Score

Each principle scores PASS = 1.0 · WARN = 0.5 · FAIL = 0.0 · N/A excluded. Principles 2 (traceability), 7 (uncertainty), and 8 (counter-analysis) carry double weight. The score is rounded to one decimal and mapped to a verdict:

| Score | Verdict |
|---|---|
| 0.0 – 2.9 | SLOP_CRITICO |
| 3.0 – 5.9 | SLOP_MODERADO |
| 6.0 – 7.9 | RIESGO_BAJO |
| 8.0 – 10.0 | LIMPIO |

Recommended blocking threshold: **7.0** for decision-grade documents, **5.0** for early drafts. Hard fails on principle 1 or on principle 8 (when the artifact is decision-grade) force `blocking: true` regardless of score.

## Author

[@jlcases](https://github.com/jlcases) — based on the 10 principles for serious AI use in organizations.
