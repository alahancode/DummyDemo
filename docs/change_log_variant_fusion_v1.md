# OSINT Agent Console Variant Fusion v1

## Purpose

This change absorbs selected UX strengths from `osint-agent-variant.html` into `osint_agent_console_demo.html` while preserving the current demo boundary: single-file HTML, no build step, no backend, no real OSINT API calls, and no real LLM execution.

The goal is to make the demo read less like a generic chat/report page and more like a task-oriented security investigation console.

## Absorbed Changes

1. Added two primary tabs:
   - `Investigate`
   - `Agent Lab`

2. Upgraded the old right-side source inspector into an independent `Agent Lab` page.
   - The investigation page focuses on IOC input, execution log, source cards, and final report.
   - The Agent Lab page focuses on per-source raw data, normalized signals, reasoning chain, suggested actions, and source-bound chat.

3. Expanded source workers from 4 to 6:
   - WHOIS
   - DNS
   - VirusTotal-style reputation
   - Shodan-style service exposure
   - AlienVault OTX-style pulse correlation
   - Threat Feeds

4. Added `chatMap` to each source worker.
   - The per-source chat answers from fixed, evidence-bound mock responses.
   - It does not claim to call a real LLM or query a real external source.

5. Upgraded report visualization:
   - `risk-pill`
   - `confidence-bar`
   - `evidence-source-badge`
   - `action-severity`

## Boundary Decisions

Kept:

- Single-file HTML with inline CSS and inline JavaScript.
- Mock-only investigation data.
- Explicit demo-only language in source detail and assistant replies.
- No external JavaScript, CSS, fonts, APIs, or network calls.

Avoided from the variant:

- External CDN dependencies.
- `LLM online` style labels.
- Real API/submission language.
- Overconfident labels such as confirmed malicious or APT attribution.
- Claims that the static page performs autonomous production-grade investigation.

## Validation Evidence

The following local checks passed after implementation:

```text
inline-script-syntax: pass
variant-fusion-static: pass
variant-fusion-dom-flow: pass
```

The DOM flow validation covered:

- Initial locked Agent Lab state.
- Six source cards rendered.
- Investigation completion.
- Report visual elements rendered.
- Agent Lab tab switching.
- Source detail rendering with raw result, reasoning chain, and suggested actions.
- Per-source chatMap responses for VirusTotal and Shodan.
- Reset returning Agent Lab to locked state.

