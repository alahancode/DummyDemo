# OSINT Agent Console Frontend SPEC

Generated: 2026-06-29

## 1. Scope

Build a single-file HTML high-fidelity frontend demo for OSINT Agent Console.

The deliverable is a presentation-grade investigation workbench, not a production frontend. It should use mock data to simulate OSINT investigation flow and should be ready for future replacement of mock fixtures with FastAPI / OSINT backend responses.

## 2. Delivery Constraints

- Single `.html` file.
- Inline CSS.
- Inline JavaScript.
- No build tool.
- No backend service.
- No database.
- No external API calls.
- Browser-openable by double clicking the file.

Optional external resources should be avoided unless necessary. If icons or fonts are used from CDN, the page should still degrade gracefully.

## 3. Page Structure

The UI should feel like an analyst workbench, not a marketing page.

Recommended structure:

1. Top command bar
   - Product label: `OSINT Agent Console`
   - IOC input
   - `Run Investigation` button
   - `Reset` button
   - Demo boundary badge: `Mock data / No external API calls`

2. Left panel: execution timeline
   - Investigation status
   - Progressive execution log
   - Orchestrator / Executor / Reasoning step labels may appear as process labels, not as separate autonomous agents.

3. Center panel: source and report workspace
   - OSINT source cards
   - Investigation report
   - Risk and confidence summary
   - Evidence chain
   - Recommended actions

4. Right panel: Agent Lab / Source Inspector / Chat
   - Locked state before investigation
   - Source detail after investigation
   - Raw result
   - Normalized signals
   - Reasoning notes
   - Suggested action
   - Follow-up chat simulation

## 4. Core Interactions

### 4.1 Initial State

- IOC input is enabled.
- Default IOC can be prefilled as `185.220.101.47`.
- Source cards are visible but idle, or shown as pending sources.
- Execution log shows an empty or ready state.
- Report shows a placeholder state.
- Agent Lab shows a locked message explaining that an investigation must run first.
- Chat is disabled or shows a prompt that it becomes useful after evidence exists.

### 4.2 Run Investigation

When the user clicks `Run Investigation`:

- Validate that the IOC input is not empty.
- Lock the input and run button during simulation.
- Start appending execution log entries progressively.
- Move source cards through visible state changes:
  - `idle`
  - `querying`
  - `done`
  - `flagged`
  - `error` if needed for demonstration
- Reveal partial evidence as sources complete.
- Build toward final report readiness.
- Unlock Agent Lab and Chat after enough evidence is available or after the investigation completes.

### 4.3 Source Inspection

When the user clicks a source card:

- The right panel displays that source's detail.
- Detail should include:
  - Source name
  - Query status
  - Mock raw result
  - Normalized signals
  - Reasoning notes
  - Suggested action
  - Boundary note if useful: `Mock source result for demo`

### 4.4 Report Generation

After the simulation completes:

- Show risk level.
- Show confidence.
- Show threat summary.
- Show evidence chain.
- Show recommended actions.
- Show limitations / caveats.

The report must feel evidence-backed. It should reference source findings and not read like generic LLM filler.

### 4.5 Chat Simulation

The chat area should support predefined answers for common questions:

- Should we block this IOC?
- Could this be a false positive?
- Why is confidence not 100%?
- What are the next steps?
- Which evidence matters most?

Rules:

- Chat responses must be based on existing mock evidence.
- Chat must be labeled as simulated or demo-only.
- Chat must not claim live LLM inference unless a real LLM is integrated later.
- Unknown questions can receive a safe fallback response explaining that the demo chat is limited.

### 4.6 Reset

When the user clicks `Reset`:

- Clear execution log.
- Reset source cards to initial state.
- Clear selected source detail.
- Restore report placeholder state.
- Re-enable input and run button.
- Restore Agent Lab locked state.
- Restore chat initial state.

## 5. Data Strategy

Use one centralized mock fixture inside the JavaScript section.

Recommended high-level structure:

```text
demoInvestigation = {
  ioc,
  iocType,
  sources,
  executionSteps,
  report,
  chatResponses,
  limitations
}
```

Each source should contain:

```text
source = {
  id,
  name,
  status,
  severity,
  headline,
  rawResult,
  normalizedSignals,
  reasoningNotes,
  suggestedAction
}
```

Report should contain:

```text
report = {
  riskLevel,
  confidence,
  summary,
  evidenceChain,
  recommendedActions,
  limitations
}
```

Data contract status:

- Current status: `mock-only`.
- Future integration: replace fixture with an adapter that maps FastAPI / OSINT backend investigation result into the same frontend view model.
- UI labels and docs must not treat mock fields as confirmed backend contract.

## 6. Visual Requirements

The visual direction should be:

- Dark.
- Console-like.
- Data dense.
- Security analysis oriented.
- Professional and restrained.
- Technical, but still readable for non-security reviewers.

Avoid:

- SaaS landing-page layout.
- Large marketing hero.
- Decorative gradient blobs.
- Overly colorful cyberpunk styling.
- Fake enterprise dashboard clutter.
- Text-heavy instruction panels.

Recommended visual elements:

- Compact top command bar.
- Monospace logs.
- Small status badges.
- Risk color coding.
- Dense but readable cards.
- Source state indicators.
- Thin borders and subtle contrast.
- Max 8px border radius for cards and panels.

## 7. State Design

The implementation should support these visible states:

- `empty`: no investigation has run.
- `ready`: IOC is available and run can start.
- `validating`: input is being checked.
- `running`: investigation simulation is active.
- `source_idle`: source has not started.
- `source_querying`: source is being queried.
- `source_done`: source completed without major flag.
- `source_flagged`: source returned concerning signal.
- `source_error`: source failed or timed out in demo.
- `report_pending`: report not ready.
- `report_ready`: report is available.
- `lab_locked`: Source Inspector unavailable before investigation.
- `lab_ready`: Source Inspector available.
- `chat_disabled`: chat unavailable before evidence exists.
- `chat_ready`: chat can answer based on mock evidence.
- `reset_complete`: page returned to initial state.

## 8. Acceptance Criteria

Functional acceptance:

- Opening the HTML file directly works.
- No console errors during normal use.
- `Run Investigation` starts a visible dynamic flow.
- Source cards change state over time.
- Execution log appends multiple entries progressively.
- Final report includes risk, confidence, summary, evidence chain, and actions.
- Agent Lab is locked before running and usable after running.
- Selecting a source changes the Source Inspector content.
- Chat can answer at least 4 predefined follow-up question types.
- Reset returns the entire page to initial state.

Boundary acceptance:

- UI clearly states that source results are mock data.
- UI does not claim real external API calls.
- Chat does not claim real LLM inference.
- The demo does not imply production-grade detection or response automation.

Visual acceptance:

- First impression is a professional security analysis console.
- Text does not overlap at desktop presentation size.
- Buttons and labels fit within containers.
- Page is usable without scrolling excessively on common laptop screens.
- Visual hierarchy supports a 3-minute walkthrough.

