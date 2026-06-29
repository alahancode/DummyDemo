# Explainability Drilldown Change Log

Generated: 2026-06-29

## Purpose

This change upgrades the OSINT Agent Console demo so each source worker can show a clearer evidence drilldown:

1. What the source returned.
2. Which raw fields matter.
3. How those fields influence risk interpretation.
4. What action the analyst should consider next.

The goal is to make the demo feel less like a generic chat interface and more like a security investigation workbench where each source contributes explainable evidence.

## What Changed

### 1. Source Detail Data Model

Each source now has a richer detail structure:

- `rawResultRows`: key-value rows for source-specific raw data.
- `reasoningChain`: short, presentation-safe reasoning steps.
- `suggestedActions`: multiple analyst-facing action recommendations.

The existing fields remain useful:

- `rawResult`: compact raw string for fallback/context.
- `normalizedSignals`: normalized source signals.
- `reasoningNotes`: compact explanation summary.
- `suggestedAction`: compact action summary.

### 2. Source Inspector UI

The right-side `Agent Lab / Source Inspector` panel now renders each selected source as:

- `查询结果 —— 来自源的原始数据`
- `Normalized Signals`
- `推理链 —— 可解释性`
- `建议行动`
- `Compact Reasoning Summary`
- Mock boundary note

This is intentionally similar to the reference image pattern: raw source result first, explanation second, recommended action last.

### 3. Visual Treatment

The source detail panel now includes:

- A compact raw result table.
- Risk-colored raw values.
- Numbered reasoning items.
- A lightly emphasized reasoning section.

This keeps the UI dense and security-console-like without turning it into a marketing page.

## Boundary Kept

This is still a static demo.

- The page does not call VirusTotal, AbuseIPDB, OTX, URLHaus, DNS, or any external OSINT API.
- The reasoning chain is a presentation-safe explanation summary, not hidden LLM chain-of-thought.
- The source cards are simulated source workers, not independent autonomous agents.
- The output is for demo storytelling and PoC alignment, not production detection accuracy.

## Why This Matters

Before this change, the demo already showed source details, but the explanation was relatively compact. After this change, each source can answer:

- What did this source return?
- Which fields are important?
- Why does this raise or lower risk?
- What should an analyst do next?

That makes the demo stronger for interviews, supervisor reviews, and solution-style presentations because the audience can see evidence and explanation tied to each source instead of only seeing a final report.

