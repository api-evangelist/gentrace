---
name: Set up an evaluation pipeline
description: Create and manage a Gentrace pipeline, the top-level container for datasets, experiments, and test cases.
api: openapi/gentrace-openapi-original.json
operations: [createPipeline, listPipelines, getPipeline, updatePipeline]
---

# Set up an evaluation pipeline

A **pipeline** is the top-level object in Gentrace; datasets, experiments, and
test cases all reference a pipeline.

## Auth
All requests use a bearer API key: `Authorization: Bearer <api_key>`.
Base URL: `https://gentrace.ai/api`. API version is in the path (`/v4`).

## Steps
1. **Check for an existing pipeline** — call `listPipelines`
   (`GET /v4/pipelines`). Filter with query params such as `slug` or
   `folderId`.
2. **Create a pipeline** — call `createPipeline` (`POST /v4/pipelines`) with a
   `slug` and `displayName`. Optionally set `folderId`.
3. **Read it back** — call `getPipeline` (`GET /v4/pipelines/{id}`) to confirm
   fields and note the `goldenDatasetId` if one is set.
4. **Update it** — call `updatePipeline` (`POST /v4/pipelines/{id}`) to change
   the display name, folder, or golden dataset.

## Rules
- Errors return `{ "message": string }` with status 400/401/404/500 — see
  `errors/gentrace-problem-types.yml`.
- No idempotency-key header is supported; guard against duplicate creates by
  checking `listPipelines` first (see `conventions/gentrace-conventions.yml`).
