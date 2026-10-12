# Engineering Journey — AI-Assisted IT Service Workflows

## Evidence Boundary

The de-identified handoff describes internal operation during 2026-10-06 through 2026-10-12: 51 retained messages and 22 tickets. This portfolio draft relies on that handoff; it does not rerun platform tests or independently inspect the original database, spreadsheet, or logs.

These counts establish recorded activity, not classification accuracy or service acceptance. All 22 tickets have a local `synced=1` state according to the supplied correction, but the spreadsheet has not been independently reconciled in full. LINE reply delivery was owner-reported and lacks retained delivery measurements.

本機同步旗標不能取代外部試算表逐筆核對；有運行紀錄也不等於正式 Production 驗收。公開內容不包含原始對話、群組識別、真實通知位置或現行設定。

## 1. Separate New Issues from Replies

**Problem:** IT responders' replies were initially interpreted as new incidents.

**Hypothesis and decision:** A single message lacked conversational context. Add responder exclusion and recent context, and explicitly distinguish a new unresolved issue from acknowledgments, progress questions, and replies.

**Recorded checks:** Five scenarios covered reply contexts and a new issue. The handoff reports the expected outcomes and an operating record showing responder exclusion.

**Limit:** Five scenarios do not establish an error rate. Identity matching and post-restart context handling need broader validation. No raw examples or identifiable messages are reproduced.

## 2. Preserve Messages Without Assuming the Workflow Completed

**Problem:** Six archived events encountered LLM failures. The original messages were saved, but classification and ticket creation did not complete.

**Investigation:** The handoff distinguishes retained input records from absent downstream results. The claimed reason for inference unavailability is an operational hypothesis, not a proven causal finding.

**Outcome:** Record this as a processing-completion gap rather than message loss. A recovery path and failure notification are follow-up work, not completed fixes.

**Limit:** Recovery after transient inference failure has not been accepted end to end. Exact failure triggers, service endpoints, and current operational configurations are omitted from the public case study.

## 3. Adapt to Reasoning-Model Output Behavior

**Problem:** Development requests could consume their output budget in reasoning and leave the answer field empty.

**Recorded adjustment:** Lower reasoning effort and add handling for an empty answer field. Larger output budgets were explored but did not remove the latency concern.

**Outcome and limit:** The handoff reports a development observation of approximately 20–30 seconds per request after adjustment. It is not a monitored latency benchmark: model revision, exact workload, repeated samples, and measurement method are not provided. A model or parser change requires renewed checks; fallback text is not proof of a valid structured classification.

## 4. Keep Knowledge Consolidation Separate from Ticket Intake

**Decision:** Convert closed-ticket handling notes into de-identified QA drafts, keeping human review before publication. Do not invent procedures absent from the handling record.

**Recorded outcome:** Sample work existed, but the first scheduled attempt failed because the integration components did not agree on the expected action. The handoff describes a version-alignment diagnosis and a proposed end-to-end rerun, not a completed recovery.

**Limit:** Weekly consolidation remains unverified end to end. Deduplication against published knowledge and suggested answers for new tickets are not completed capabilities.

## Reliability: Implementation versus Verification

| Control | Implementation evidence in handoff | Verification limit |
|---|---|---|
| HMAC-SHA256 webhook signature | Documented validation path | Archived incorrect-signature and validation-request checks; no broad security audit claimed |
| Group allowlist | Documented deny-by-default design | Blocking and subsequent authorized operation recorded; identifiers omitted |
| Event deduplication | Database unique-event design | Replay and failure-recovery scenarios not independently accepted here |
| Spreadsheet idempotency and retry delivery | Apps Script and backend logic documented | `synced=1` does not prove external reconciliation or successful retry under every failure |
| Ticket numbering and locking | Transaction and lock controls documented | No retained race-stress acceptance evidence supplied |
| LLM concurrency limit | Control exists in the implementation account | Not a load-test or throughput result |
| Human-reviewed knowledge drafts | Sample workflow documented | Scheduled end-to-end success remains absent |

## Remaining Constraints and Roles

The workflow is text-only. Backups, restoration drills, external monitoring, a labeled accuracy set, and a time-saving baseline are not established by the handoff. Credential lifecycle and operational hardening require private follow-up; no secret values or exploitable configuration details are disclosed.

The Project Owner supplied workflow requirements, architecture choices, required platform setup, and result review. Claude Code performed the recorded development, integration, tests, deployment, and debugging. Colleagues maintained the initial spreadsheet. Codex produced the portfolio documentation, without revalidating the service.

This is a de-identified documentation case study. No original conversations, database exports, operational logs, private reports, code, or settings are included. Public rights and formal acceptance are not inferred from internal operation. See the [project overview](../README.md).
