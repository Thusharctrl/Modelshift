# Open Decisions

All entries are pending approval. The proposed defaults are recommendations intended to bound a one-month part-time MVP; they are not final product or architecture decisions.

| Decision | Why it must be finalized before the TRD | Proposed default | Status |
| --- | --- | --- | --- |
| Supported detection matrix | Determines scanner behavior, fixtures, false-positive policy, and acceptance tests. | Python AST plus a written, fixture-backed set of OpenAI, Anthropic, Gemini, and config-key patterns only. | Pending approval |
| Supported input boundaries | Determines what is scanned and the secret-safety model. | `.py`, `.json`, `.yaml`, `.yml`, `.toml`, and opt-in `.env.example`; exclude real environment files, binaries, vendor/build folders, and secret-bearing files by default. | Pending approval |
| Lifecycle evidence model | Determines whether P0 requires network access and how claims remain verifiable. | Versioned local registry with captured excerpts, official URLs, verification timestamps, stale/fetch-failed states, and manual review; live refresh deferred. | Pending approval |
| Lifecycle taxonomy and freshness | Determines alert meanings, conflicts, and CI behavior. | `active`, `deprecated`, `scheduled_for_retirement`, `retired`, `unknown`, `unverified`, and `stale`; unknown/unverified never pass as active. Define a freshness threshold in the TRD. | Pending approval |
| Alias and matching policy | Prevents incorrect alerts for similar model names or deployments. | Exact ID matching plus explicitly curated aliases; near matches are review-only. | Pending approval |
| MVP live inference | Affects privacy, credentials, budget, test reproducibility, and provider adapter scope. | Offline stored-output comparison is required; defer live adapters until the offline end-to-end path works. | Pending approval |
| Test manifest contract | Needed to validate inputs and make test results reproducible. | Versioned YAML or JSON manifest with stable case ID, input, baseline/expected value, validators, tags, and declared parameters. | Pending approval |
| Baseline and comparison policy | Determines whether incomplete evidence can incorrectly pass. | No baseline or suitable validator means `not_comparable`; retain deterministic exact/contains/regex/required-field/JSON Schema validators only. | Pending approval |
| Sensitive-data retention and redaction | Required before storing reports, inputs, or outputs. | Synthetic fixtures by default; local artifacts; explicit output-retention option; redact likely credentials from console and reports. | Pending approval |
| Report contents and artifact policy | Determines privacy, reproducibility, and what reviewers receive. | Self-contained local JSON and HTML with evidence pointers, case-level failures, configuration/run metadata, and a non-equivalence disclaimer. | Pending approval |
| CLI and CI exit-code policy | Needed for testable automation behavior. | Separate commands for scan, lifecycle check, test, and report; non-zero only for configuration errors or explicitly configured critical findings. | Pending approval |
| Performance and portability evidence | Determines realistic sign-off obligations. | Measure the 1,000-file/15-second target on declared hardware and verify offline behavior on macOS, Windows, and Linux. | Pending approval |
| MVP sign-off definition | Prevents scope expansion and ambiguous completion. | An offline fixture demo: scan -> evidence-backed alert -> saved-baseline validation -> HTML/JSON report, with all stated acceptance tests passing. | Pending approval |
