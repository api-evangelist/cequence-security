# Cequence Security

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

Cequence Security (<https://www.cequence.ai/>) is an application, API, and AI protection vendor.
Its Unified API Protection (UAP) platform discovers documented, undocumented, shadow and third-party
APIs, builds a runtime API inventory, scores risk and compliance, tests APIs in CI/CD, and mitigates
bot, fraud and business-logic abuse at runtime. Its Cequence AI Gateway makes existing enterprise
applications agent-ready by publishing REST APIs (registered from an OpenAPI spec) and third-party
remote MCP servers as governed Model Context Protocol endpoints.

## API surface

| Surface | Status |
|---|---|
| Public REST OpenAPI | **None served anonymously.** UAP 9.0 ships "a published, versioned OpenAPI specification for the API Security component" *from inside the product*, not from a public URL. |
| GraphQL | None. |
| MCP | **Yes** — a first-party, Cequence-hosted MCP server (25 documented tools) provisioned automatically for every AI Gateway tenant. The endpoint URL is tenant-specific and OAuth-gated. |
| A2A agent card | None (`/.well-known/agent-card.json` and `/.well-known/agent.json` 404 on `www.cequence.ai`; the app and docs hosts are SPA catch-alls). |
| AsyncAPI / webhooks | None. Event delivery is SIEM export only (Splunk HEC, Datadog, OTLP, syslog). |
| CLI | **Yes** — `@cequenceai/mcp-cli` on npm (`cequence-mcp`), MIT, 48 releases. |

## Key links

- Docs: <https://docs.aigateway.cequence.ai/docs/introduction>
- Getting started: <https://docs.aigateway.cequence.ai/docs/getstarted>
- MCP tool reference: <https://docs.aigateway.cequence.ai/docs/remote-mcp-servers/cequence-ai-gateway>
- Support / knowledge base: <https://helpdesk.cequence.ai/hc/en-us>
- Release notes index: <https://helpdesk.cequence.ai/hc/en-us/articles/34708505561495-Latest-Releases>
- Trust center: <https://trust.cequence.ai/> (SOC 2 Type 2, PCI DSS v4.0.1, ISO 27001:2022)
- Responsible disclosure: <https://www.cequence.ai/responsible-disclosure-policy/> (security@cequence.ai)
- GitHub: <https://github.com/cequenceai>

> **Do not confuse with `github.com/cequence-io` / `io.cequence` on Maven Central** — that is
> Cequence, a contracting-software company (cequence.io), a different organization.

## Artifacts

`authentication/` · `changelog/` · `cli/` · `conformance/` · `conventions/` · `errors/` ·
`lifecycle/` · `llms/` · `mcp/` · `packages/` · `rate-limits/` · `security/` · `skills/` ·
`well-known/`
