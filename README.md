# StarCi — AI-native design-system canon + Claude Code skills

An AI-native engineering workspace: a self-improving, **source-grounded** knowledge base + a skill
pipeline for Claude Code that turns a feature request into a **clickable prototype**, then real code.

## Skills (`skills/`)
- **`starci-fe-layout-brainstorm`** — pick a page's shell by its JOB → map zones/states → render a
  clickable HTML flow prototype (host on `:8080`, walk it like slides) → an approved proposal.
- **`starci-fe-layout-apply`** — build the proposal: **Opus writes a meticulous impl-spec, Sonnet codes it**, then verify.
- **`starci-fe-block-brainstorm` / `starci-fe-block-apply`** — the lighter, single-block-scope pair.
- **`starci-doc-audit`** — audits the knowledge base for dead links · mis-shelving · staleness vs source · drift.

## FE design-system (`fe/`)
Grounded in the real codebase, organized the way the code already is:
`foundations` (tokens) → `layouts` (shells · region model) → `components` → `patterns` (flows) → `principles`.
Plus `prototypes/` — the reusable interactive-prototype kit.

## Backend canon (`be/`)
`rules` (coding conventions) + `concepts` (architecture: CQRS + Debezium CDC, GraphQL resolver pattern,
TypeORM, NATS/Kafka messaging, Socket.IO, 5 payment gateways, RAG, Judge0…).

---
> **Public read-only mirror.** Project/business-specific shelves (feature analysis, monetization
> axioms, the proposal backlog, conversion psychology) are **redacted** — the skills reference them as a
> workflow, but their content stays private. Grounded in the StarCi Academy codebase
> (Next.js + React 19 + HeroUI v3 · NestJS + TypeORM + GraphQL + CQRS).
