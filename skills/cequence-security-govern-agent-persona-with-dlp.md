---
name: govern-agent-persona-with-dlp
description: Compose an Agent Persona from tools across multiple Cequence AI Gateway MCP servers, scope it to a Team, attach reusable skills, and protect it with a DLP policy.
api: Cequence AI Gateway
surface: mcp
server: Cequence AI Gateway MCP (first-party, tenant-provisioned)
operations:
  - list_mcp_servers
  - list_tools_for_mcp_server
  - list_teams
  - list_skills
  - get_skill
  - create_agent_persona
  - update_agent_persona
  - get_agent_persona
  - list_sdp_categories
  - list_dlp_policies
  - recommend_dlp_policy
  - attach_dlp_policy
generated: '2026-08-02'
method: generated
source: https://docs.aigateway.cequence.ai/docs/remote-mcp-servers/cequence-ai-gateway
---

# Govern an Agent Persona with a DLP policy

An Agent Persona combines tools from multiple MCP servers into a single endpoint
with SSO and access-key authentication. This is where least privilege is actually
enforced, so build the persona and its data protection together — never ship the
persona first and add DLP later.

## Steps

1. **Inventory the tool surface.**
   `list_mcp_servers` for the deployed servers, then `list_tools_for_mcp_server`
   for each one you intend to draw from. Write down exactly which tools the persona
   needs.

2. **Decide who may use it.**
   `list_teams` returns the SSO-mapped user groups. Scope the persona to a team
   rather than the whole tenant.

3. **Attach reusable skills, if any.**
   `list_skills` and `get_skill` read the Skill Registry (SKILL.md documents agents
   discover and load on demand). Use `create_skill` only when no existing skill
   covers the flow.

4. **Create the persona in dry-run first.**
   `create_agent_persona` supports a `dryRun` validation mode. Run it dry, read the
   validation result, then run it for real. Use `update_agent_persona` for partial
   edits afterwards rather than recreating.

5. **Build the DLP policy.**
   `list_sdp_categories` returns the standard sensitive-data-protection categories.
   `list_dlp_policies` (optionally scoped to the persona) shows what already exists.
   `recommend_dlp_policy` produces a deterministic recommendation for the persona —
   review it, do not apply it blind.

6. **Attach and verify.**
   `attach_dlp_policy` creates and attaches the policy to the existing persona.
   Finish with `get_agent_persona`, which returns the persona including its connect
   URL — that URL is what you hand to the agent client.

## Rules that apply to every call

- **Narrow, then narrow again.** Endpoints are selected at API registration, and
  *"each persona can be granted an even narrower subset."* The persona is the
  tightest ring; keep it that way.
- **Authorization failures are 403** with audit reason `access_control_denied`;
  authentication failures are 401 with `auth_denied`. Do not retry either — fix the
  team membership or reconnect the SSO flow.
- **Write tools are not idempotent.** No idempotency key is documented, so confirm
  with `get_agent_persona` / `list_dlp_policies` before re-issuing
  `create_agent_persona` or `attach_dlp_policy`.
- **Every call is audited** with tool name, server, user identity, client IP,
  status, action, reason, durations, request ID and session ID. Assume attribution.
