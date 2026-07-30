---
name: Extract structured data from a document with Kita Capture
description: Submit a bank statement, payslip, ID, credit report or other financial document to the Kita Capture API and retrieve structured, validated, fraud-checked JSON.
api: openapi/kita-capture-openapi.yml
base_url: https://portal.usekita.com
operations:
  - processDocumentAsync
  - getDocumentResult
  - getDocumentSummary
  - listDocuments
  - exportDocument
  - customExportDocument
  - getDocumentJob
generated: '2026-07-19'
method: generated
source: https://www.kita.ai/documentation
---

# Extract structured data from a document with Kita Capture

Use this to turn a scanned or photographed financial or identity document into clean JSON —
transactions, metadata, metrics and fraud signals.

## Before you start

- Auth: `Authorization: Bearer kita_prod_...`. Keys are issued from https://portal.usekita.com
  and are **server-side only**.
- Accepted file types: PDF, PNG, JPG, TIFF, BMP. Encrypted PDFs take a `password` field.
- Every submission consumes credits. There is no test mode — pick the smallest real document
  when validating an integration.
- Errors are `{ "error": ..., "message": ... }`. A `429` carries a `Retry-After` header; wait
  that long before retrying.

## Steps

### 1. Pick the document type

`document_type` is required and case-insensitive. Choose the most specific slug — it selects
the extraction vocabulary, the validators and the fraud signals.

Common slugs: `bank_statement`, `payslip`, `bill`, `receipt`, `sales_invoice`,
`government_id`, `credit_report`, `certificate_of_employment`, `loan_statement`,
`credit_card_statement`, `passbook`, `business_financials`, `remittance_slip`,
`bank_certificate`, `mobile_banking_screenshot`.

Regional: `slik` (Indonesian OJK credit report), `general_information_sheet` (PH SEC GIS),
`barangay_clearance` (PH), `acta_constitutiva` (MX), `mx_legal`, `indo_legal`.

Multi-document bundles: `combined_document` (auto-segmented per page).

If nothing fits, use `other_document`. Slugs without a dedicated vocabulary (`tin_id`,
`business_permit`, `land_title`, `income_tax_return` and the rest of the experimental list)
are accepted but route through the `other_document` extractor and return only the generic
`{ document_data, labeled_fields, signatories }` envelope — no type-specific validators or
signals. Say so when you report the result.

Use `audited_financial_statement`, never the retired `afs` shorthand.

### 2. Submit — `processDocumentAsync`

`POST /api/process-async`, in either mode:

- **Multipart**: `file` + `document_type` (+ optional `password`).
- **JSON**: `file_base64` + `filename` + `document_type`. A `data:` URI prefix is accepted and
  stripped automatically. The extension on `filename` drives file-type validation, so set it
  correctly.

Returns `{ "documentId": ..., "status": "pending" }`. Keep the `documentId`.

Pass `webhook_url` to have the result delivered instead of polling. For many documents from
URLs, use `createBatch` (`POST /api/v1/batch`, up to 100 per request, paid plans only).

### 3. Poll — `getDocumentResult`

`GET /api/results/{documentId}` until `status` is `completed`. States are `pending`,
`processing`, `completed`, `failed`. Poll on backoff, not in a tight loop.

**A 200 does not mean success.** `status: "failed"` is reported in the body, not as an HTTP
error. Check it before reading `extracted_data`.

### 4. Read the result

Every document type shares the envelope: `status`, `document_type`, `document_id`, `filename`,
`processing_time_seconds`, `uploaded_at`, `metadata`, `extracted_data`, and — only when data
exists — `fraud_detection`.

- `metadata` is document-level: account holder, institution, statement dates, currency,
  opening and closing balance.
- `extracted_data` is type-specific: `transactions[]` and `metrics` for a bank statement;
  `payslips[]`, `employment_info`, `signals[]` and `fraud_score` for a payslip; `bill_fields`
  and `signal_summary` for a bill; `credit_report_data` and `metrics` for a credit report;
  `invoices[]` for a sales invoice.
- `fraud_detection` carries `risk_level`, `authenticity_score` and `signals[]` with
  `severity`, `category` and `message`.

For a bank statement or passbook where you only need headline figures, call
`getDocumentSummary` (`GET /api/documents/{id}/summary`, `?format=csv` for CSV) instead of
pulling the whole transaction list.

For an Excel deliverable use `customExportDocument` (the organization's configured format) or
`exportDocument` (schema-driven multi-sheet, for `audited_financial_statement`,
`credit_report`, `slik` and other schema-based types).

### 5. Optional — check cost

`GET /api/v1/documents/jobs/{documentId}` returns `total_cost_usd` and a `cost_report`
breakdown per model call. Use it when the user asks what a run cost.

## Rules

- Never invent a field that is not in the response. Absent extraction is a real result —
  report it as missing, not as zero.
- Report `fraud_detection` and any `signals` alongside the extracted values. A high
  `authenticity_score` is not a guarantee; a low one is a reason to escalate to a human.
- Fraud and risk output is decision *support*. Do not present it as an approval, a denial, or
  a determination that a document is fraudulent.
- Keep the API key out of browsers, logs and repositories.
