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
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

Kita is an AI-native loan origination and underwriting company (Y Combinator W26, San
Francisco) building document intelligence and credit decisioning for lenders in emerging and
undertapped markets — the Philippines, Indonesia, Mexico and the United States.

Kita ships two developer-facing APIs:

- **Kita Capture** — document intelligence. Turns scanned or photographed bank statements,
  payslips, government IDs, credit reports, tax filings and 30+ other document types into
  structured, validated, fraud-checked JSON. Cross-document verification, batch processing,
  custom extraction schemas, per-document cost reporting and HMAC-signed webhooks.
  Base URL `https://portal.usekita.com`.
- **Kita AI Underwriter** — the credit file. Creates loan applications, ingests borrower
  documents, computes a deterministic credit picture (adjusted EBITDA, DSCR, margins,
  debt-to-worth, sensitivity, policy decision — from a versioned calculation engine, not an
  LLM) and synthesizes a cited credit memo with PDF and XLSX exports.
  Base URL `https://underwriter.kita.ai/api/v1`.

Backed by: y-combinator

## Links

- Website — https://www.kita.ai/
- Documentation — https://www.kita.ai/documentation
- Pricing — https://www.kita.ai/pricing
- Security — https://www.kita.ai/security
- Guided demo — https://demo.kita.ai/
- Dashboard / sign-up — https://portal.usekita.com/
- GitHub — https://github.com/Kita-Technologies
- Python SDK — https://pypi.org/project/kita/
- MCP server — https://www.npmjs.com/package/kita-docs-mcp

## Artifacts in this repository

| Directory | What it holds |
|---|---|
| `openapi/` | OpenAPI 3.1 for both APIs, generated from Kita's published documentation |
| `overlays/` | API Evangelist enhancement overlays for each spec |
| `authentication/` | API key model, prefixes, key scopes, rotation |
| `conventions/` | Idempotency, pagination, envelopes, async model, versioning |
| `errors/` | Error catalog and envelopes for both APIs |
| `rate-limits/` | Rate-limit signalling and published constraints |
| `plans/` | Pricing tiers and the credit model |
| `asyncapi/` | Webhook catalog (Kita publishes no AsyncAPI) |
| `data-model/` | Entity-relationship graph across both domains |
| `lifecycle/` | Versioning, deprecation, regions, maturity |
| `conformance/` | Standards conformance assertions |
| `sandbox/` | Hosted demo, free tier, and the absence of a test mode |
| `mcp/` | The official `kita-docs-mcp` server, its tools and resources |
| `packages/` | First-party packages on PyPI and npm |
| `examples/` | Official example programs and worked responses |
| `skills/` | Agent Skills for the three marquee flows |
| `llms/` | Generated `llms.txt` |
| `well-known/` | `/.well-known/` probe results (none published) |
| `security/` | Domain security probe, vulnerability disclosure, trust posture |
| `agentic-access/` | Recommended `x-agentic-access` contracts per operation |

Kita publishes no machine-readable OpenAPI description. The specifications in `openapi/` were
generated by the API Evangelist enrichment pipeline from Kita's own published documentation —
https://www.kita.ai/documentation, the `API.md` in
[Kita-Technologies/kita-api-examples](https://github.com/Kita-Technologies/kita-api-examples),
and the docs bundle shipped verbatim inside the official `kita-docs-mcp` npm package. Only
operations, fields and status codes that Kita documents are represented.
