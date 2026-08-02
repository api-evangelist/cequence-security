---
name: audit-agent-tool-activity
description: Investigate what agents did through the Cequence AI Gateway — denials, rate limiting, DLP findings, upstream failures — using the tool activity log.
api: Cequence AI Gateway
surface: mcp
server: Cequence AI Gateway MCP (first-party, tenant-provisioned)
operations:
  - query_tool_activity
  - list_mcp_servers
  - list_agent_personas
  - get_agent_persona
  - list_dlp_policies
generated: '2026-08-02'
method: generated
source: https://docs.aigateway.cequence.ai/docs/guides/observability
---

# Audit agent tool activity

Use this when someone asks "what did the agent actually do", "why is this tool
failing", or "did anything sensitive leave the building".

## Steps

1. **Frame the question.**
   `query_tool_activity` is the single observability tool and covers logs, summary,
   facets, trends, log detail and findings. Decide which of those you need before
   calling — a summary or facet query answers most questions without pulling raw
   logs.

2. **Scope it.**
   `list_mcp_servers` and `list_agent_personas` give you the server and persona
   names to filter on. `get_agent_persona` confirms which tools a persona was even
   allowed to call, which usually explains a 403 straight away.

3. **Read the status and reason, not just the count.**
   Tool activity status is one of `success`, `error`, `blocked`, `rate_limited`.
   The `action.reason` field carries the machine-readable cause:

   | reason | meaning | fix |
   |---|---|---|
   | `auth_denied` | inbound credential missing/invalid (401) | reconnect SSO/OAuth, check the key |
   | `access_control_denied` | caller not permitted (403) | grant the tool to the persona, or add the SSO group to the Team |
   | `rate_limit_exceeded` | per-tool rolling window hit (429) | wait for the window, or raise Max Requests |
   | `circuit_breaker_open` | upstream halted after repeated failures (503) | restore upstream health |
   | `upstream_error` | upstream errored/unreachable (502) | check upstream + egress policy |
   | `outbound_auth_failed` | injected upstream credential rejected (502) | reconnect the app authorization or rotate the stored credential |

4. **Check DLP findings separately.**
   `query_tool_activity` exposes findings; `list_dlp_policies` tells you which
   policy was in force for the persona. A `blocked` status with no auth or rate
   reason is usually a security interceptor.

5. **Correlate outside the gateway.**
   Every event carries `request.id` and session ID and is exported to Splunk (HEC),
   Datadog, OTLP (gRPC or HTTP) or syslog (TCP/UDP/TLS). Use the request ID to join
   against the upstream's own logs; `duration.total_ms` versus `duration.upstream_ms`
   separates gateway overhead from upstream latency.

## Event fields you can rely on

`timestamp`, `request.id`, `tool.name`, `mcp.server_name`, `user.email`,
`client.ip`, `status`, `action`, `action.reason`, `duration.total_ms`,
`duration.upstream_ms`, `http.status_code`.

Operational (non-tool) events include `config_change`, `component_lifecycle` and
`reconciliation_complete` — useful when behaviour changed but no tool call failed.
