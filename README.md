# Cequence Security

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
