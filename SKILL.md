---
name: project-bootstrapper
description: A reusable, domain-agnostic scaffold for any multi-session project that has raw data and must produce traceable, auditable, handoff-ready deliverables — literature review, paper writing, data analysis, engineering R&D, knowledge-base building. Triggers: "start a new project", "set up a project spec / control document", "create a project startup prompt", or when an existing project shows drift (stale summaries, inconsistent naming, lost context). The skill creates one single-source-of-truth control document and enforces a set of lightweight disciplines that survive context compression, handover, and long collaborations — (1) single source of truth, (2) semantic raw-data renaming, (3) deliverable numbering & lifecycle with `_退役_`/`_作废_` retired-file markers, (4) intermediate-vs-final-text separation, (5) verification log + changelog, (6) context-drift correction, (7) handover checklist, (8) process-reply style (clear / concise / no fluff), (9) destructive-write pre-flight gate, (10) attempt budget & escalation ceiling, (11) reusable-script harvesting, (12) feasibility tiering; and (13) functional folder taxonomy. The control-doc skeleton includes two always-empty slots — integration-contract / known-pitfalls and environment-contract — that each project fills with its own concrete instances. Ships a copy-paste universal startup prompt and a section skeleton template. Documentation-only; no executable code, no network calls.
agent_created: true
---

# Project Bootstrapper

## Overview

Establish a runnable, traceable, extensible project skeleton for any work that spans multiple sessions, has raw data, and produces deliverables that must stay auditable and handoff-ready. The skeleton centers on one control document (single source of truth) plus a set of lightweight disciplines that survive context compression, handover, and long collaborations.

## When to use

- User says "start a new project", "set up a project spec", "build a project scaffold", "create a project startup prompt", or similar.
- Any task that will run across sessions, involve raw data, and need traceable deliverables.
- When an existing project shows drift (stale summaries, inconsistent naming, lost context).

## How to use

1. On the first task, create `{{PROJECT_NAME}}_项目规范.md` as the single control document. Copy the section skeleton from `references/bootstrap_template.md` (§三) and fill the `{{...}}` placeholders.
2. Brief the user on the disciplines below and apply them on every subsequent step.
3. Provide the universal startup prompt (full block in `references/bootstrap_template.md` §二) so the user can re-bootstrap any future project with one paste.
4. After each deliverable, update the control doc's progress / verification-log / changelog sections.

## Disciplines (enforce on every step)

1. **Single source of truth** — one control doc with fixed sections (动因 / 目标 / 范围 / 原始数据 / 流程 / 规则 / 进度 / 风险 / 验证日志 / 术语 / 变更 / 交接 / 写作规范 / 集成契约-已知坑 / 环境契约); all conclusions trace back to it; never edit a report without editing the spec. The last two sections are empty slots by default — each project fills them with its own concrete instances.
2. **Semantic raw-data renaming & archival** — every external input MUST be archived into the project (default location `data/raw/`, per discipline 13) on entry and renamed to `<type>_<desc>_<n>`; the external original (Downloads/email/cloud) is never relied upon and may be deleted once archived. The archived raw is **immutable** — never edited in place; any derived/processed copy goes to `data/processed/`. Record provenance (source/origin, date received, size, content hash e.g. SHA-256) in the control doc §4 so integrity is verifiable. Sync every script `open()` path and citation after renaming.
3. **Deliverable numbering & lifecycle** — pick one naming pattern per project; both keep the mandatory retired/voided marker discipline:
   - **Default — document-centric / research / consulting / knowledge projects:** `<主题>_<类型>_<版本>_<日期>.md` (theme + type + version + date). Groups files by theme, encodes the supersession chain via version (v1→v2→v3), and stays sortable via the date suffix. Control/index files keep fixed semantic names.
   - **Alternative — high-volume automated artifact streams** (batch-produced intermediates, per-record exports): `YYMMDD-NNN_<semantic>.md` with NNN a project-global increasing 3-digit counter (never reset across days/batches) to prevent collisions.
   - **Mandatory for both:** a file superseded by merge/replacement gets a `_退役_` or `_作废_` marker placed after the sequence/version token and before the semantic name (e.g. `<主题>_<类型>_<版本>_退役_<日期>.md` or `202401-001_退役_*.md`) — kept on disk, rewritten as a pointer to the replacement, logged as "superseded/voided", never physically deleted, so historical traceability survives.
4. **Intermediate vs final-text separation** — produce a paper-ready "成稿文字" alongside reports: objective, traceable, inline `[待…]` annotations, verification step. One final text per finding, in the target language (avoid parallel CN/EN duplicates).
5. **Verification log + changelog** — independent checks with fact-vs-inference separation; forms the audit chain.
6. **Context-drift correction** — after any compression/continuation, re-read disk (Python `io.open`) before editing; never trust stale summaries. Long-session memory decay is the top invisible risk.
7. **Handover checklist** — a permanent "next steps" list so any future self or collaborator can continue without an information island.
8. **Process-reply style** — every progress/question reply is clear (layered, conclusion-first), appropriately detailed, concise, no fluff; prefer tables/short sentences over long paragraphs.
9. **Destructive-write pre-flight gate** — any write/delete to an external system (database, library, API, bulk filesystem) must, before execution: (a) capture a named read-only snapshot of the affected state; (b) run in DRY_RUN by default, printing the exact set of targets to be changed for human confirmation; (c) record the rollback artifact's location in the verification log. Project survivability rests on this gate, not on memory.
10. **Attempt budget & escalation ceiling** — at project start, fix an explicit ceiling on automated retries for any single blocked sub-task, plus a pre-agreed fallback ladder (automated → semi-automated → manual-in-browser → human). When the ceiling is hit, stop and switch tiers instead of re-hammering; log the switch in the changelog.
11. **Reusable-script harvesting** — a "deliverable" is not only a document; a workaround script that proved necessary becomes a first-class project asset. Promote it to a named, documented tool or skill once it is reusable, so the next project inherits the fix instead of re-discovering the pain.
12. **Feasibility tiering** — classify each deliverable's production path by tier (automated / semi-automated / manual-in-browser / human-only). This prevents re-attempting an automatable-but-blocked path and makes discipline 10 actionable.
13. **Functional folder taxonomy** — assign every file to a folder by *functional attribute*, not by date or batch: `deliverables/` (final outputs), `workings/` (drafts, per-batch reports, intermediates), `data/raw/` (semantic-renamed imports per discipline 2), `data/processed/` (cleaned/extracted intermediates), `references/` (primary-source originals: PDFs, archived webpages, policy texts), `scripts/` (helper + reusable scripts, the harvest target of discipline 11), `memory/` (cross-session memory). The SSoT control doc and the index file keep fixed semantic names at root so re-bootstrap stays one-paste. This is a **default layout** — a project with a natural alternative (e.g. `chapters/`, `figures/`, `src/`) may adapt it, but MUST record the chosen layout in the control doc (§3 范围 or a dedicated §布局) and reflect it in the index. The `_退役_`/`_作废_` markers (discipline 3) apply inside whatever folder a file lives. Moving files between folders is a destructive write under discipline 9: snapshot + DRY_RUN + logged rollback first.

## Why these disciplines (design principles)

- SSoT prevents divergent multi-file accounts; semantic naming + (version or sequence) numbering make every artifact traceable and de-duplicated; retired/voided files keep their `_退役_`/`_作废_` marker and stay on disk, so the traceability chain is never broken.
- Intermediate/final separation keeps the reproduction chain while preserving migratable material.
- Verification log + changelog form an audit chain that survives compression and handover.
- Drift correction treats memory decay as a hard risk, not an afterthought.
- Process-reply style extends "clear/concise" from deliverables to every conversation, suppressing long-session information dilution.
- Destructive-write pre-flight gate converts irreversible external mutations into recoverable ones: the snapshot + DRY_RUN + logged rollback artifact are what make a mistake survivable, because the discipline does not trust memory.
- Attempt budget & escalation ceiling bounds exploration cost up front; it is the explicit rule that stops re-hammering a blocked path and forces a tier switch, which the changelog records.
- Reusable-script harvesting treats a hard-won workaround as portable capital, not a one-off; the next project starts where the last one finished.
- Feasibility tiering makes the attempt-budget rule operational by pre-labeling which paths are even open.
- Functional folder taxonomy groups files by *what they are for* (deliverable / working / raw / reference / tool), so the directory tree itself becomes a navigation aid and a drift detector — a misfiled file is visible at a glance, and the control doc + index at root stay one-paste findable.
- Raw-data archival + provenance (discipline 2) makes every external input reproducible and tamper-evident: the immutable `data/raw/` copy plus a recorded SHA-256 means a later byte-change or a "which version did we analyze?" question is answerable from the control doc alone.

## Security note

This skill is documentation-only. It contains no executable code, network calls, or external dependencies. Safe to use.
