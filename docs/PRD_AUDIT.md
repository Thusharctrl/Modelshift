# PRD Audit

## Source and audit posture

This audit reflects the actual ten-page `ModelShift_PRD_v1.0.pdf`, dated 21 October 2026 and labeled “Draft for mentor review.” Its stated target is a one-month college minor-project prototype. Statements below identified as requirements are taken from that draft; recommendations are not approved requirements.

## Draft requirements

### Product behaviour

- Provide a local-first, CLI-first workflow: scan a selected repository, inventory supported references, check lifecycle status, compare a candidate output with a saved baseline, and produce HTML/JSON reports.
- Scan Python, JSON, YAML, TOML, and explicitly opted-in example environment files. Exclude real `.env` and secret-bearing files by default.
- Detect supported provider SDK patterns, literal model arguments, selected model-related constants, and selected configuration keys. Findings need location where available, inferred provider, value, and detection method; dynamic values must be uncertain, not guessed.
- Maintain lifecycle records with provider, model ID, status, relevant dates, official replacement only when stated, source URL, supporting excerpt, and verification time. Unknown must not become active; failed refreshes must preserve prior records and show stale/fetch-failed status.
- Use official provider lifecycle material or structured provider APIs as the primary evidence. Conflicts must be visible; broad fuzzy matches cannot produce definitive alerts.
- Support validated migration case manifests and deterministic exact, contains, regex, required-field, and JSON Schema checks. A missing reliable baseline or validator must yield not-comparable, not pass.
- Permit live candidate execution only through explicit user invocation; do not log credentials. Produce case-level results and configurable non-zero CLI/CI outcomes.
- Keep scanning static-only: never import, execute, or shell-run scanned project material or model-generated output. Keep analysis local by default and warn before sending selected inputs to a provider.
- Record run metadata and state clear limits: passing configured checks is not proof of behavioural equivalence, production safety, or complete dependency coverage.

### Acceptance and non-functional expectations

- Provide fixture-based tests for supported/unsupported/dynamic references, lifecycle matching and stale evidence, manifests, validators, exit codes, and error handling.
- Generate offline HTML/JSON from stored results, with lifecycle evidence and per-case outcomes.
- Aim to scan a 1,000-file fixture in 15 seconds on a typical student laptop, but measure rather than claim performance.
- Support macOS, Windows, and Linux for core offline functionality.

## Ambiguities and internal tensions

- “Known provider/model patterns” is not a testable scope until exact SDK call forms, configuration keys, model-ID syntax, and false-positive policy are listed.
- The PRD simultaneously calls official-source retrieval P0 and describes a local registry. It does not decide whether the MVP must fetch live sources, can use curated snapshots, or how official excerpts are licensed, stored, refreshed, and reviewed.
- Lifecycle states are named, but their canonical vocabulary, stale threshold, conflict resolution, aliases, and CI severity mapping are unspecified.
- “Confidence,” “review state,” “concise diff,” “configured regression thresholds,” request/cost limits, and report redaction rules lack definitions or acceptance tests.
- The manifest format, JSON Schema draft/version, raw-output retention policy, input-data classification, and report-access model are unspecified.
- “Live candidate run when configured” and an offline-first MVP are compatible, but a live adapter is a major scope variable. The required first provider and success criteria are not decided.
- The proposed technology stack and data entities are design suggestions in a draft PRD, not architecture decisions. Choosing them now would violate the requested pre-TRD boundary.
- The success claim requires lifecycle evidence, scanning, regression testing, reporting, and portability in a month of part-time work. This is feasible only with sharply bounded patterns, fixture-led offline behavior, and limited live integration.

## One-month implementation risks

| Risk | Why it threatens the schedule | Recommended control |
| --- | --- | --- |
| Provider documentation changes | Live retrieval/parsing is brittle and needs monitoring and fixtures. | Start with a manually curated, versioned official-evidence registry; treat refresh as a bounded experiment. |
| Detection breadth | SDK/config variants and dynamic references create false positives and missed findings. | Publish a small supported-pattern matrix and fixtures before writing the scanner. |
| Live inference | Credentials, privacy, cost, rate limits, and response variability complicate a reproducible demo. | Make the end-to-end sign-off demo fully offline; defer a single live adapter until offline checks pass. |
| Regression semantics | Validators cannot establish semantic equivalence, while semantic judging adds nondeterminism and cost. | Keep only deterministic validators in P0 and make not-comparable explicit. |
| Reporting sensitive data | Inputs and raw outputs can contain secrets or proprietary data. | Decide retention/redaction defaults before report implementation; use synthetic fixtures. |
| Cross-platform work | Packaging and filesystem differences can consume time without improving the core proof. | Test the offline demo on the required platforms late in the sprint; avoid nonstandard system dependencies. |

## Recommended feasible MVP

Recommendation, pending approval: define success as a fully offline, fixture-backed path that scans a constrained Python/config fixture repository, matches exact IDs against a small curated lifecycle registry containing captured official evidence, evaluates stored candidate outputs against saved baselines with the five deterministic validator types, and emits self-contained JSON/HTML reports.

Limit P0 to an approved pattern matrix for OpenAI, Anthropic, and Gemini examples, a fixed set of configuration keys, exact IDs and approved aliases, and a small synthetic migration suite. Treat live retrieval, provider adapters, CI examples, semantic judging, RAG explanations, broad language support, and database selection as deferred unless an approved scope change makes one indispensable.

This MVP directly demonstrates the product’s reliability claims without pretending it can provide live lifecycle coverage or migration safety at broad scale. It also preserves a credible extension path once the data, security, and acceptance boundaries are decided.

## Unresolved decisions

See [OPEN_DECISIONS.md](OPEN_DECISIONS.md). In particular, the team must approve the support matrix, lifecycle-evidence operating model, live-inference scope, manifest and retention rules, exit-code policy, and the definition of an MVP sign-off run before drafting the TRD.
