---
name: Build an evaluation dataset with test cases
description: Create a dataset under a pipeline and populate it with test cases (inputs and expected outputs) for evaluation.
api: openapi/gentrace-openapi-original.json
operations: [createDataset, listDatasets, createTestCase, listTestCases, deleteTestCase]
---

# Build an evaluation dataset with test cases

A **dataset** groups **test cases**; each test case carries `inputs` and
`expectedOutputs` used to grade model output.

## Auth
Bearer API key: `Authorization: Bearer <api_key>`. Base URL
`https://gentrace.ai/api`.

## Steps
1. **Create a dataset** — call `createDataset` (`POST /v4/datasets`) with a
   `name` and either `pipelineId` or `pipelineSlug`. Set `isGolden: true` to
   make it the pipeline's golden reference dataset.
2. **List datasets** — call `listDatasets` (`GET /v4/datasets`) to find an
   existing dataset (filter by `pipelineId`).
3. **Add test cases** — for each example call `createTestCase`
   (`POST /v4/test-cases`) with `datasetId`, `name`, `inputs`, and
   `expectedOutputs`.
4. **Review** — call `listTestCases` (`GET /v4/test-cases`) filtered by
   `datasetId`.
5. **Remove a bad case** — call `deleteTestCase`
   (`DELETE /v4/test-cases/{id}`); it returns `204 No Content`.

## Rules
- Every test case `belongs_to` a dataset via `datasetId` (see
  `data-model/gentrace-data-model.yml`).
- Errors: `{ "message": string }` (`errors/gentrace-problem-types.yml`).
