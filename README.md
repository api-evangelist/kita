# Kita

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

Kita is an AI-native loan origination and underwriting company (Y Combinator W26, San Francisco) building document intelligence and credit decisioning for lenders in emerging and undertapped markets. Kita ships two developer-facing APIs. Kita Capture is a document-intelligence API that turns scanned or photographed bank statements, payslips, government IDs, credit reports, tax filings and 30+ other document types into structured, validated, fraud-checked JSON, with cross-document verification, batch processing, custom extraction schemas and HMAC-signed webhooks. Kita Underwriter is a credit-file API that creates loan applications, ingests borrower documents, computes a deterministic credit picture (adjusted EBITDA, DSCR, margins, debt-to-worth, sensitivity and a policy-engine decision produced by a versioned calculation engine rather than an LLM) and synthesizes a cited credit memo. The platform is region-pinned across Singapore and Mexico deployments and is used by microfinance institutions, SME lenders, CDFIs and community banks across Southeast Asia, Latin America and the United States.

**Areas:** Company · Fintech · Lending · Underwriting · Credit Scoring · Document Intelligence · Document Extraction · Fraud Prevention · Artificial Intelligence · Computer Vision · Emerging Markets · Loan Origination

## Kita on APIs.io

Everything profiled for Kita is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/kita/](https://apis.io/providers/kita/)** — or go straight to one of the APIs or properties below.

### APIs (14)

- [Kita Applications API](https://apis.io/apis/kita/kita-applications-api/) — Loan application records.
- [Kita Batch API](https://apis.io/apis/kita/kita-batch-api/) — Process up to 100 documents from URLs in one request.
- [Kita Conversation API](https://apis.io/apis/kita/kita-conversation-api/) — Borrower message thread.
- [Kita Credit API](https://apis.io/apis/kita/kita-credit-api/) — Deterministic credit picture — spread, adjustments, policy decision.
- [Kita Documents API](https://apis.io/apis/kita/kita-documents-api/) — Borrower document upload and extraction.
- [Kita Exports API](https://apis.io/apis/kita/kita-exports-api/) — PDF and XLSX exports.
- [Kita Folders API](https://apis.io/apis/kita/kita-folders-api/) — Group documents into containers.
- [Kita Memo API](https://apis.io/apis/kita/kita-memo-api/) — Cited credit memo synthesis and retrieval.
- [Kita Processing API](https://apis.io/apis/kita/kita-processing-api/) — Submit documents for extraction.
- [Kita Results API](https://apis.io/apis/kita/kita-results-api/) — Retrieve extraction results, summaries and exports.
- [Kita Schemas API](https://apis.io/apis/kita/kita-schemas-api/) — Custom extraction schemas.
- [Kita Transcripts API](https://apis.io/apis/kita/kita-transcripts-api/) — Plain-text document transcripts.
- [Kita Verification API](https://apis.io/apis/kita/kita-verification-api/) — Cross-document verification checks.
- [Kita Webhooks API](https://apis.io/apis/kita/kita-webhooks-api/) — Register and manage HMAC-signed outbound webhooks.

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### AsyncAPI (1)

Event-driven and webhook contracts.

- [Kita Capture Webhooks](https://apis.io/asyncapis/kita/kita-capture-webhooks/)

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [kita-docs](https://apis.io/servers/kita/kita-docs/)

#### Agentic access (1)

Which operations an agent can call, which act, and which need a human in the loop.

- [Kita Agentic Access](https://apis.io/agentic-access/kita/kita-agentic-access/)

#### Collections (28)

Postman and Open Collection request collections.

- [Kita Capture Applications API](https://apis.io/collections/kita/open-kita-applications-api/)
- [Kita Capture Applications Batch API](https://apis.io/collections/kita/open-kita-batch-api/)
- [Kita Capture Applications Conversation API](https://apis.io/collections/kita/open-kita-conversation-api/)
- [Kita Capture Applications Credit API](https://apis.io/collections/kita/open-kita-credit-api/)
- [Kita Capture Applications Documents API](https://apis.io/collections/kita/open-kita-documents-api/)
- [Kita Capture Applications Exports API](https://apis.io/collections/kita/open-kita-exports-api/)
- [Kita Capture Applications Folders API](https://apis.io/collections/kita/open-kita-folders-api/)
- [Kita Capture Applications Memo API](https://apis.io/collections/kita/open-kita-memo-api/)
- [Kita Capture Applications Processing API](https://apis.io/collections/kita/open-kita-processing-api/)
- [Kita Capture Applications Results API](https://apis.io/collections/kita/open-kita-results-api/)
- [Kita Capture Applications Schemas API](https://apis.io/collections/kita/open-kita-schemas-api/)
- [Kita Capture Applications Transcripts API](https://apis.io/collections/kita/open-kita-transcripts-api/)
- [Kita Capture Applications Verification API](https://apis.io/collections/kita/open-kita-verification-api/)
- [Kita Capture Applications Webhooks API](https://apis.io/collections/kita/open-kita-webhooks-api/)
- [Kita Capture Applications API](https://apis.io/collections/kita/postman-kita-applications-api/)
- [Kita Capture Applications Batch API](https://apis.io/collections/kita/postman-kita-batch-api/)
- [Kita Capture Applications Conversation API](https://apis.io/collections/kita/postman-kita-conversation-api/)
- [Kita Capture Applications Credit API](https://apis.io/collections/kita/postman-kita-credit-api/)
- [Kita Capture Applications Documents API](https://apis.io/collections/kita/postman-kita-documents-api/)
- [Kita Capture Applications Exports API](https://apis.io/collections/kita/postman-kita-exports-api/)
- [Kita Capture Applications Folders API](https://apis.io/collections/kita/postman-kita-folders-api/)
- [Kita Capture Applications Memo API](https://apis.io/collections/kita/postman-kita-memo-api/)
- [Kita Capture Applications Processing API](https://apis.io/collections/kita/postman-kita-processing-api/)
- [Kita Capture Applications Results API](https://apis.io/collections/kita/postman-kita-results-api/)
- [Kita Capture Applications Schemas API](https://apis.io/collections/kita/postman-kita-schemas-api/)
- …and 3 more published on APIs.io

#### Overlays (2)

OpenAPI overlays, including conversational phrasing for each operation.

- [Kita Capture Overlay](https://apis.io/overlays/kita/kita-capture-overlay/)
- [Kita Underwriter Overlay](https://apis.io/overlays/kita/kita-underwriter-overlay/)

#### Security (4)

Authentication, trust centre, and vulnerability disclosure.

- [Kita Authentication](https://apis.io/security/kita/kita-authentication/)
- [Kita Domain Security](https://apis.io/security/kita/kita-domain-security/)
- [Kita Trust Center](https://apis.io/security/kita/kita-trust-center/)
- [Kita Vulnerability Disclosure](https://apis.io/security/kita/kita-vulnerability-disclosure/)

#### Plans and pricing (1)

Published plans, tiers and prices.

- [Kita Plans](https://apis.io/plans/kita/kita-plans/)

#### Rate limits (1)

Published request limits.

- [Kita Rate Limits](https://apis.io/rate-limits/kita/kita-rate-limits/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://www.kita.ai/)
- [Documentation](https://www.kita.ai/documentation)
- [Getting started](https://www.kita.ai/documentation)
- [API reference](https://www.kita.ai/documentation)
- [Pricing](https://www.kita.ai/pricing)
- [Sign up](https://portal.usekita.com/)
- [Blog](https://www.kita.ai/blog)
- [Security](https://www.kita.ai/security)
- [Compliance](https://www.kita.ai/security)
- [Terms of service](https://www.kita.ai/terms)
- [Privacy policy](https://www.kita.ai/privacy)
- [GitHub](https://github.com/Kita-Technologies)

## API Evangelist rating

**Kin Score 60.8** — strong · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 71.7 |
| Contract quality | 63.3 |
| Contract governance | 4.5 |
| Operational transparency | 21.1 |
| Developer ergonomics | 74.4 |
| Access clarity | 92.1 |

**Agent readiness 39.5** — agent-native

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | derived (partial credit) |
| Reversibility Documented | — |
| MCP Server | documented (partial credit) |
| Auth Clarity | bearer (partial credit) |
| Idempotency | documented (partial credit) |
| Error Semantics | documented (partial credit) |
| OpenAPI Examples | partial |
| Rate Limit Signal | verified |
| Event Surface Described | yes |
| Agent Skills | derived (partial credit) |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | — |
| Dry Run Mode | — |
| Delegated Identity | — |
| Protected Resource Metadata | — |
| Dynamic Client Registration | — |
| Agentic Commerce | — |
| Pagination Ratio | — |
| Operation Distinctiveness | distinct |

**Regulatory alignment 29.5** — Insurance

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/kita/](https://apis.io/providers/kita/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for Kita: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/kita/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
