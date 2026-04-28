# Maat

Claude Code skill to audit AI slop in business artifacts — reports, M&A memos, board decks, RAG pipelines, prompt libraries.

> The problem is not that AI hallucinates. The problem is that organizations hallucinate that they are informed.

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

- **Executive verdict** (SLOP CRÍTICO / MODERADO / BAJO / LIMPIO)
- **Per-principle audit** (PASS/WARN/FAIL with literal evidence)
- **Top 5 dangerous claims** table
- **Counter-analysis** (auto-generated when missing)

## Author

[@jlcases](https://github.com/jlcases) — based on the 10 principles for serious AI use in organizations.
