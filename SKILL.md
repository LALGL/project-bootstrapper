---
name: project-bootstrapper
description: A reusable, domain-agnostic scaffold for any multi-session project that has raw data and must produce traceable, auditable, handoff-ready deliverables — literature review, paper writing, data analysis, engineering R&D, knowledge-base building. Triggers: "start a new project", "set up a project spec / control document", "create a project startup prompt", or when an existing project shows drift (stale summaries, inconsistent naming, lost context). The skill creates one single-source-of-truth control document (13 fixed sections) and enforces eight lightweight disciplines that survive context compression, handover, and long collaborations — (1) single source of truth, (2) semantic raw-data renaming, (3) deliverable numbering & lifecycle with `_退役_`/`_作废_` retired-file markers, (4) intermediate-vs-final-text separation, (5) verification log + changelog, (6) context-drift correction, (7) handover checklist, (8) process-reply style (clear / concise / no fluff). Ships a copy-paste universal startup prompt and a 13-section skeleton template. Documentation-only; no executable code, no network calls.
agent_created: true
---

# Project Bootstrapper

## Overview

Establish a runnable, traceable, extensible project skeleton for any work that spans multiple sessions, has raw data, and produces deliverables that must stay auditable and handoff-ready. The skeleton centers on one control document (single source of truth) plus eight lightweight disciplines that survive context compression, handover, and long collaborations.

## When to use

- User says "start a new project", "set up a project spec", "build a project scaffold", "create a project startup prompt", or similar.
- Any task that will run across sessions, involve raw data, and need traceable deliverables.
- When an existing project shows drift (stale summaries, inconsistent naming, lost context).

## How to use

1. On the first task, create `{{PROJECT_NAME}}_项目规范.md` as the single control document. Copy the 13-section skeleton from `references/bootstrap_template.md` (§三) and fill the `{{...}}` placeholders.
2. Brief the user on the eight disciplines below and apply them on every subsequent step.
3. Provide the universal startup prompt (full block in `references/bootstrap_template.md` §二) so the user can re-bootstrap any future project with one paste.
4. After each deliverable, update the control doc's progress / verification-log / changelog sections.

## Eight disciplines (enforce on every step)

1. **Single source of truth** — one control doc with 13 fixed sections (动因 / 目标 / 范围 / 原始数据 / 流程 / 规则 / 进度 / 风险 / 验证日志 / 术语 / 变更 / 交接 / 写作规范); all conclusions trace back to it; never edit a report without editing the spec.
2. **Semantic raw-data renaming** — rename external imports to `<type>_<desc>_<n>` on entry; keep originals untouched; sync every script `open()` path and citation after renaming.
3. **Deliverable numbering & lifecycle** — `YYMMDD-NNN_<semantic>.md`, NNN globally increasing, never reset across days/batches; control/index files keep fixed names but are logged with managed numbers. A file superseded by merge/replacement gets a `_退役_` or `_作废_` marker after the number and before the semantic name (e.g. `202401-001_退役_*.md`) — kept on disk, rewritten as a pointer to the replacement, logged as "superseded/voided", never physically deleted, so historical traceability survives.
4. **Intermediate vs final-text separation** — produce a paper-ready "成稿文字" alongside reports: objective, traceable, inline `[待…]` annotations, verification step. One final text per finding, in the target language (avoid parallel CN/EN duplicates).
5. **Verification log + changelog** — independent checks with fact-vs-inference separation; forms the audit chain.
6. **Context-drift correction** — after any compression/continuation, re-read disk (Python `io.open`) before editing; never trust stale summaries. Long-session memory decay is the top invisible risk.
7. **Handover checklist** — a permanent "next steps" list so any future self or collaborator can continue without an information island.
8. **Process-reply style** — every progress/question reply is clear (layered, conclusion-first), appropriately detailed, concise, no fluff; prefer tables/short sentences over long paragraphs.

## Why these eight (design principles)

- SSoT prevents divergent multi-file accounts; semantic naming + numbering make every artifact traceable and de-duplicated; retired/voided files keep their `_退役_`/`_作废_` marker and stay on disk, so the traceability chain is never broken.
- Intermediate/final separation keeps the reproduction chain while preserving migratable material.
- Verification log + changelog form an audit chain that survives compression and handover.
- Drift correction treats memory decay as a hard risk, not an afterthought.
- Process-reply style extends "clear/concise" from deliverables to every conversation, suppressing long-session information dilution.

## Security note

This skill is documentation-only. It contains no executable code, network calls, or external dependencies. Safe to use.
