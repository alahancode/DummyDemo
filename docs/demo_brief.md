# OSINT Agent Console Demo Brief

Generated: 2026-06-29

## 1. Key Assumptions

- First-stage deliverable is a single HTML file with inline CSS and inline JavaScript.
- The demo can be opened directly in a browser without backend service, build tool, database, or external API key.
- All OSINT source results, execution logs, report content, and chat responses are mock data for presentation.
- The page must not imply that it is calling real external security APIs such as VirusTotal, AbuseIPDB, OTX, URLHaus, WHOIS, or DNS services.
- LLM-like behavior is limited to explanation, summarization, and follow-up answer simulation based on existing evidence.
- The demo should communicate a PoC / presentation-shell boundary, not claim production readiness.
- The main target screen is desktop presentation. Smaller screens should remain readable and non-broken, but mobile is not the core demo scenario.

## 2. Demo Goal

Build a high-fidelity OSINT Agent Console frontend demo that shows how AI can assist a security analyst in moving from one IOC input to a structured multi-source threat investigation report.

The demo should make the investigation flow visible: input an IOC, query multiple sources, organize evidence, explain risk, and produce recommended actions. The main purpose is not to prove production-grade OSINT accuracy, but to help interviewers, supervisors, reviewers, and non-security stakeholders understand the system value within 3 minutes.

## 3. Target Users and Audience

Primary user represented by the UI:

- Security analyst who needs to investigate suspicious IPs or domains.

Primary demo audience:

- Interviewers who want to see rapid requirement understanding, demo design, AI coding workflow, and PoC delivery ability.
- Supervisors or project reviewers who need to understand the OSINT Agent project's target workflow and current staged result.
- Solution customers or non-security stakeholders who care about business value, technical path, and future implementation potential.

Audience characteristics:

- May have technical background but may not know OSINT or threat investigation details.
- Will not read code line by line.
- Needs to quickly understand what the system does, why AI helps, and where the current capability boundary is.

## 4. User Problems

Security analysts face several workflow issues:

1. After receiving an IOC such as an IP or domain, they must manually query multiple OSINT sources.
2. Different intelligence sources return inconsistent formats, making evidence organization slow.
3. A single threat score or isolated alert is not enough for response decisions.
4. Analysts and reviewers need to understand why an IOC is suspicious, not only whether it has a high score.
5. Non-security reviewers cannot easily infer project value from backend code alone.
6. At PoC stage, the project needs to demonstrate the core flow quickly instead of overbuilding a production platform.

## 5. Core Demo Scenario

Example IOC:

```text
185.220.101.47
```

Demo flow:

1. User enters the IOC.
2. User clicks `Run Investigation`.
3. The system starts showing an Agent execution log.
4. Multiple OSINT source cards move through `querying`, `done`, `flagged`, or `error` states.
5. The page generates an investigation report containing risk level, confidence, threat summary, evidence chain, and recommended actions.
6. User opens Agent Lab / Source Inspector to inspect source-level raw result, normalized signal, reasoning notes, and suggested action.
7. User uses the chat area to ask follow-up questions about blocking, false positives, confidence, and next steps.
8. The audience sees a complete loop from IOC input to evidence-backed decision support.

## 6. Business Value

The demo should communicate four business values:

1. Workflow consolidation: one console shows the investigation path instead of scattered manual lookups.
2. Evidence organization: source outputs are normalized into a structured evidence chain.
3. Decision support: the system explains why an IOC is suspicious and what action should be considered.
4. Stakeholder alignment: a visual demo helps non-security audiences understand the project value faster than backend code alone.

The AI value should be framed as evidence organization, risk explanation, confidence reasoning, and recommended action support. It should not be framed as a magic detector that invents threat intelligence.

## 7. Demo Boundary

This demo is a high-fidelity presentation shell.

It can show:

- A realistic OSINT investigation workflow.
- Mock multi-source intelligence results.
- Simulated source querying states.
- Evidence-backed report structure.
- Source-level inspection.
- LLM-like explanation and follow-up chat behavior.
- Future integration direction with FastAPI / OSINT backend investigation results.

It must not claim:

- Real-time calls to external OSINT APIs.
- Production-grade detection accuracy.
- Authenticated user workflow, audit logging, or persistent storage.
- Real LLM inference if the chat is implemented as predefined mock responses.
- Autonomous source agents if the frontend only simulates source workers or source cards.

Recommended wording inside the UI:

```text
Demo-only mock investigation. Source results and AI responses are simulated to demonstrate workflow and interface design.
```

## 8. Success Criteria

The demo is successful if:

- A single HTML file opens directly in a browser.
- The first screen looks like a professional security analysis console.
- The audience understands the system value within 3 minutes.
- Clicking `Run Investigation` triggers a complete dynamic investigation flow.
- Source cards visibly change states.
- Execution log entries appear progressively.
- The final report contains risk, confidence, summary, evidence chain, and recommended actions.
- `Reset` restores the initial state.
- Agent Lab has a clear locked / empty state before an investigation runs.
- Agent Lab can show source details after an investigation.
- Chat creates an explainable AI feeling without pretending to be a real LLM.
- All mock and demo-only capability boundaries are visible and unambiguous.

