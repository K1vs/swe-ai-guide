### 6. Agent extensibility

Although modern agents include the most needed tools, more specialized tools are usually not available “out of the box.” For developers these can be integrations with ALM systems (Jira, Azure DevOps), design prototyping (Figma), API contract schemas, or databases. Since these integrations are often complex and vendors offer different capabilities, baking all of them directly into an agent is not practical. So even early generations of popular agents provided extension mechanisms that allowed adding separate modules with extra functionality.

A typical and very useful example from practice is the PostgreSQL extension for VS Code with Copilot. It lets the agent run queries against PostgreSQL, quickly create seed or test data, check current data state, and draw useful conclusions. The advantage is that the extension is “perfectly fitted” to a specific client (editor/agent). The drawback is duplicated effort: maintaining separate extensions for each agent and each tool is very costly.

This is a classic case for a “bridge” - a shared protocol understood by both agents and tools. In 2024, Anthropic proposed the Model Context Protocol (MCP) - a standard for exchanging commands, data, and context between an agent and external services. MCP defines roles and transport so that integrations can be reusable and portable across agents.

### Roles in MCP: agent as client, tool as server

- The agent acts as an MCP client. It initiates a connection, discovers server capabilities, requests resources, calls tools, subscribes to events, and sends relevant session context to the server.
- The tool/service implements an MCP server. It describes available resources (documents, datasets, endpoints), commands (tools/actions), parameters, access rights, and response formats. The server can also offer streaming events or notifications for reactive scenarios.

The key idea: the agent does not embed support for a specific system. Instead, it calls MCP servers in a unified way. As a result, the same MCP server (for example, for Jira) can work with different agents, and any agent that supports MCP can use any compatible server.

### Connection transports: pipes and HTTP

MCP supports several ways to connect:

- Pipes/stdio: local connection via standard streams or named pipes (on Windows). Minimal latency; simpler to run locally next to the agent/IDE.
- HTTP(S): network connection to a remote MCP server. Suitable for cloud services, team work, and scaling. Allows TLS, proxies, and network‑level access control.

“Remote MCP” is also gaining momentum - deploying servers outside the local dev environment (in the cloud or internal infrastructure) that agents connect to over HTTP(S). This simplifies centralized access control, updates, and shared use of integrations by the whole team.

### Useful examples of MCP servers

- Atlassian Remote MCP (Jira, Confluence): practical value - quick enrichment of task context. If the description is spread across several Jira tickets and Confluence pages, the agent follows the links, gathers relevant fragments, builds a concise context, and uses it for planning or implementation. After finishing, the agent can update the ticket: set status, fill fields (for example, affected area), add links to MR/PR - the things developers often postpone.
- GitHub MCP: useful for microservice architectures with separate repositories. The agent can automatically fetch the expected service contract (OpenAPI/Protobuf/GraphQL schema), compare versions, find breaking changes, and create a PR with client updates or compatibility tests.
- Figma MCP: for frontend developers - a strong accelerator. The agent extracts specs from designs (sizes, styles, tokens), generates component/page skeletons, forms a checklist for layout, and compares implementation with the design.

The advantage for vendors like Atlassian is that they do not need a plugin for each agent or IDE. One MCP server is enough. In turn, agent authors do not need separate integrations with each ALM - they only need a stable MCP client.

### MCP security: risks and mitigations

Standardizing integrations raises the risk of wrong or excessive access. Key security practices:

- Least privilege: use separate technical accounts with the minimum rights; split read and write; disable dangerous actions by default.
- Explicit action approvals: the agent should request explicit user confirmation for destructive operations (status changes, mass updates, DB writes). Use allowlists of tools and domains.
- Authentication and audit: OAuth/OIDC, short‑lived tokens, key rotation, binding to specific workspaces. Access logs, call tracing, and storing artifacts for investigations.
- Data‑leak protection: filter PII/secrets in server responses, redaction policies, encryption in transit (TLS) and at rest when needed. Limit the amount of content returned into the LLM context.
- Prompt‑injection defense: when the agent “clicks through” Jira/Confluence pages or repository READMEs, normalize content and isolate unknown HTML/scripts. Apply content security policies and heuristics to detect instructions that change agent behavior.
- Network controls: segmentation, egress filtering for HTTP transport, rate limits, SSRF protection, and restrictions on external domains.
- Sandbox for write operations: for repos - work in forks/branches with protection; for DBs - separate test schemas or read‑replicas for reads; for ALM - sandbox projects.

### Implementation practice

#### Connect a ready MCP server to a ready agent

- This is really simple: usually a few lines in configuration that the agent itself suggests or generates. In new versions of VS Code, adding many servers is available right from the marketplace with auto‑filled configuration.
- Typical scenario: choose a server (for example, GitHub/Brave/Figma), confirm the launch command, and add needed environment variables (token/key). The agent shows status (running/failed) and available tools.
- In Cursor, servers are added via settings; in VS Code - via the “MCP: Add Server” command or the extension card. Connection time is 1–2 minutes without deep technical details.

#### Practices for developing MCP servers and clients in agents

- Servers: clear contract (capabilities/tools/resources), stable response schemas, versioning. Pagination/limits for context control, transparent error model, idempotence for write operations. Authentication (OAuth/OIDC), observability (logs/tracing), prompt‑injection protection, and filtering of secrets/PII.
- Clients (agents): discovery flow and feature gating, parameter validation before calls, timeouts/retries. Context budgeting, explicit confirmations for destructive actions, allowlists of tools/domains. Graceful degradation on outages, usage telemetry.
- Important: in many modern products, you should plan and offer an MCP server to the customer at the design stage. This lets not only people but also LLM agents use the service - without separate plugins for each tool/IDE.

### Summary

MCP removes the barrier “one tool - one extension - one agent” and moves integrations to a shared bus. The agent as a client opens tools in a unified way, and tools as servers publish reusable capabilities.

Pipes are a good fit for local scenarios with minimal latency, and HTTP(S) works for remote and team scenarios, remote MCP makes integrations a shared team resource.

Practical wins include fast task‑context building (Jira/Confluence), automatic access to contracts (GitHub), and faster layout work (Figma).

All this needs security discipline: least privilege, confirmations for dangerous actions, audit, and protection from leaks and prompt injection. Following these principles, MCP gives a balanced way to scale agent capabilities without exploding integration costs.



### Sources

- Official MCP docs/spec: https://modelcontextprotocol.io
- GitHub organization: https://github.com/modelcontextprotocol
- TypeScript SDK: https://www.npmjs.com/package/@modelcontextprotocol/sdk
- Python SDK: https://pypi.org/project/mcp/
- Example servers and frameworks: https://github.com/modelcontextprotocol/servers
- Using MCP with agents (OpenAI Agents): https://openai.github.io/openai-agents-js/guides/mcp
- Build an MCP server (Cloudflare Workers): https://developers.cloudflare.com/agents/guides/build-mcp-server/
- Using MCP with Claude Desktop: https://docs.anthropic.com/claude/docs/mcp
- Azure agents with MCP: https://learn.microsoft.com/en-us/azure/developer/ai/intro-agents-mcp