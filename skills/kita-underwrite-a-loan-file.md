---
name: Underwrite a loan file with Kita
description: Create a loan application, push borrower documents, wait for extraction, read the deterministic credit picture, and generate a cited credit memo using the Kita AI Underwriter API.
api: openapi/kita-underwriter-openapi.yml
base_url: https://underwriter.kita.ai/api/v1
operations:
  - intakeApplication
  - getApplication
  - listDocuments
  - getDocument
  - getCreditPicture
  - synthesizeMemo
  - getMemoStatus
  - getMemo
generated: '2026-07-19'
method: generated
source: https://www.kita.ai/documentation
---

# Underwrite a loan file with Kita

Use this when you need to take a borrower's documents and produce a decision-ready credit
file: normalized financials, a policy decision, and a cited memo.

## Before you start

- Auth: `Authorization: Bearer kita_uw_...` (or `Authorization: ApiKey kita_uw_...`). The key
  needs **both** `read` and `write` scope for this flow. A key missing the scope returns 403.
- There is **no test mode**. Every call here creates real records. Always supply
  `external_ref` so retries are idempotent.
- Errors are `{ "message": "..." }` with a standard HTTP status.

## Steps

### 1. Create the application and push documents in one call — `intakeApplication`

`POST /intake` as `multipart/form-data` with an `application` field holding the JSON metadata
plus repeated `file`/`files` parts.

Required metadata: `business_name`, `borrower_email`, `loan_type` (must match a loan product
configured on the organization), `loan_amount` (> 0). Optional: `borrower_phone`,
`application_context`, `send_outreach`, and — always send this — `external_ref`.

- `201` means a new application was created.
- `200` with `"idempotent": true` means this `external_ref` already existed; the existing
  application is returned and documents are **not** re-uploaded. This is the safe retry.
- `502` means the application **was** created but the document upload failed. Do not blindly
  re-run: either replay `/intake` with the same `external_ref`, or upload the documents with
  `uploadDocuments` against the returned id.

Keep the returned `id` (UUID) or `app_id` (e.g. `APP-1234`). Both work in the path.

### 2. Wait for extraction — `listDocuments` / `getDocument`

`GET /applications/{id}/documents`. Each document's `status` moves
`awaiting` → `processing` → `verified` or `low_confidence`. `missing` means a required
document was never provided.

Poll on backoff: start at 2–3 seconds and back off exponentially. Do not tight-loop.

Treat `low_confidence` as "extracted but flag for human review", not as failure. Call
`getDocument` for the structured `kita_raw` extraction plus `recommendations` and
`inconsistencies` — surface `inconsistencies` to the user, they are the reason to look at the
file.

### 3. Read the deterministic credit picture — `getCreditPicture`

`GET /applications/{id}/credit` returns three layers, each **null until computed**:

- `spread` — adjusted EBITDA and net income, DSCR, margins, debt-to-worth, current ratio,
  reserve months, LTV, a sensitivity table, and per-metric provenance.
- `adjustments` — normalization line items, each tagged `ai` (model-proposed) or `lo`
  (loan-officer entered).
- `decision` — the policy-engine routing recommendation, an auto-route flag, and every rule's
  pass/fail with observed vs expected.

A `null` layer means *not yet computed*, not zero — never report it as a zero or a decline.
These numbers come from a versioned calculation engine, not from a language model. Do not
recompute, restate, or "correct" them; quote them and cite the provenance.

### 4. Synthesize the memo — `synthesizeMemo`, then `getMemoStatus`

`POST /applications/{id}/memo` drafts or redrafts the cited memo and runs **inline for up to
about 120 seconds**. Set your client timeout accordingly.

Then poll `GET /applications/{id}/memo/status` until **both** `synthesis_in_progress` is
`false` **and** `is_stale` is `false`. `is_stale` with `new_doc_count` or `new_message_count`
above zero means documents or borrower messages arrived after the last synthesis — redraft
before presenting the memo. `last_run_status: failed` means the run failed; retry once and
report if it fails again.

### 5. Read the memo — `getMemo`

`GET /applications/{id}/memo` returns `sections[]` with `section_number`, `title`, `body`
(plain text), `locked_by_lo` and `updated_at`. Sections with `locked_by_lo: true` were edited
by a human — never overwrite or paraphrase them away.

## Rules

- The routing recommendation defaults to human review. Do not present it as an approval.
- Never set `status` to `approved` or `declined` on the application on your own initiative —
  that records a lender credit decision and requires an explicit human instruction.
- Never call `deleteApplication`: it permanently removes the application, its documents and
  storage, and the borrower record if orphaned, with no undo and no test environment.
- Cite. Every figure you report should carry the document line the API attributes it to.
