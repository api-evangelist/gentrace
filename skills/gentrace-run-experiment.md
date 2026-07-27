---
name: Run and track an evaluation experiment
description: Create an experiment against a pipeline, then read and update it to track an evaluation run.
api: openapi/gentrace-openapi-original.json
operations: [createExperiment, listExperiments, getExperiment, updateExperiment]
---

# Run and track an evaluation experiment

An **experiment** records an evaluation run against a pipeline. Use it to group
results and attach metadata.

## Auth
Bearer API key: `Authorization: Bearer <api_key>`. Base URL
`https://gentrace.ai/api`.

## Steps
1. **Create an experiment** — call `createExperiment`
   (`POST /v4/experiments`) with `pipelineId`, an optional `name`, and optional
   `metadata`.
2. **List experiments** — call `listExperiments` (`GET /v4/experiments`),
   filtering by `pipelineId`.
3. **Inspect one** — call `getExperiment` (`GET /v4/experiments/{id}`).
4. **Update it** — call `updateExperiment` (`POST /v4/experiments/{id}`) to
   change the name or `metadata` (e.g. mark the run complete).

## Rules
- Each experiment `belongs_to` a pipeline via `pipelineId`.
- POST creates are not idempotent — list first to avoid duplicates
  (`conventions/gentrace-conventions.yml`).
- Errors: `{ "message": string }` (`errors/gentrace-problem-types.yml`).
