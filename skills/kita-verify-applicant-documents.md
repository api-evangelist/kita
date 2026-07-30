---
name: Cross-verify an applicant's documents with Kita
description: Run Kita Capture's cross-document verification over an applicant's already-processed payslip, bank statement and ID to check they corroborate each other, and wire webhooks so results arrive without polling.
api: openapi/kita-capture-openapi.yml
base_url: https://portal.usekita.com
operations:
  - processDocumentAsync
  - getDocumentResult
  - verifyDocuments
  - verifySingleDocument
  - createWebhook
  - testWebhook
  - listWebhookDeliveries
generated: '2026-07-19'
method: generated
source: https://www.kita.ai/documentation
---

# Cross-verify an applicant's documents with Kita

Use this when a credit application arrives with several documents and you need to know whether
they describe the same person and the same financial reality.

## Before you start

- Auth: `Authorization: Bearer kita_prod_...`.
- Verification only accepts documents that are **already `completed`** and belong to the
  calling organization. Process them first with `processDocumentAsync` and confirm with
  `getDocumentResult`.
- Between 2 and 50 document IDs per verification request.

## Steps

### 1. Process each document first

Submit each file with `processDocumentAsync` using its correct `document_type`, then poll
`getDocumentResult` until each is `completed`. Collect the `document_id` values. Skip anything
that came back `failed` — a failed document cannot be verified.

### 2. Run cross-document verification — `verifyDocuments`

`POST /api/v1/verify` with `{ "document_ids": [101, 102, 103] }`. Kita runs 34+ cross-document
checks.

The response gives you:

- `document_count` and `documents[]` — per-document `authenticity_score`, `risk_level` and
  `integrity_checks`.
- `document_summary` — a count by document type, e.g.
  `{ "bank_statement": 1, "payslip": 1, "government_id": 1 }`.
- `cross_doc_score` — the headline corroboration score across the set.
- `signals[]` — the individual cross-document findings.
- `field_verifiability` — which fields could actually be checked against another document.
- `corroboration` — where documents agree and where they diverge.

Read `field_verifiability` before you trust `cross_doc_score`. A high score over a set where
almost nothing was verifiable means "we could not check", not "this is consistent".

### 3. Drill into one document — `verifySingleDocument`

`POST /api/v1/verify/single` returns the full `fraud_detection` block for a single document.
Use it to explain *why* one document dragged the set score down.

### 4. Optional — stop polling, use webhooks

For volume, register a delivery endpoint with `createWebhook` (`POST /api/v1/webhooks`) with a
`url`, the `events` you want and `active: true`. Then:

- `testWebhook` (`POST /api/v1/webhooks/{id}/test`) sends a test delivery.
- `listWebhookDeliveries` (`GET /api/v1/webhooks/{id}/deliveries`) shows status, attempts and
  latency when something looks missing.
- Deliveries that exhaust every retry land in the dead-letter queue
  (`GET /api/v1/webhooks/dlq`).

Verify every delivery before acting on it: Kita signs the **raw request body** with HMAC-SHA256
using the webhook's secret and sends it on the `X-Kita-Signature` header. Check both the
signature and the `t=` timestamp against the tolerance window (5 minutes by default) so a
captured payload cannot be replayed.

For a one-off job you can skip registration entirely and pass `webhook_url` on
`processDocumentAsync` or `createBatch`.

## Rules

- Never call `getWebhookSecret` or `rotateWebhookSecret` on your own initiative. The first
  exposes a live signing secret; the second silently breaks every existing verifier until
  they are updated. Both need an explicit human instruction.
- Verification output is decision support. Report divergences and let a human adjudicate;
  never state that an applicant committed fraud.
- If the applicant set is missing a document type the checks depend on, say which check could
  not run rather than reporting a clean result.
