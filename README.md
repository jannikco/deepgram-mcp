# Deepgram MCP server

Inspect accessible projects and request history, then approve a single URL transcription. Long audio may exceed the bounded HTTP timeout; inspect request history before retrying an uncertain paid request.

A direct-provider MCP server with useful local execution. No PipMCP account is required for local use. Provider API access and any provider charges are your responsibility.

## Quick start

Requires Node.js22+. Clone this repository, then run:

```sh
npm ci --ignore-scripts
npm test
npm start
```

The default command inspects the tools offline. Configure your own credentials in your environment:

- `DEEPGRAM_API_KEY`



Credential help: https://raw.githubusercontent.com/deepgram/deepgram-api-specs/main/openapi.yml

## Execute a real read

Replace example record IDs with records you are authorized to access.

```sh
npm start -- --call list_projects '{}'
```

## Use with an MCP client

Launch `node /absolute/path/deepgram-mcp/server.mjs` using stdio transport; pass credentials through the client environment. Stdout is reserved for JSON-RPC.

## Tools

| Tool | Effect | Purpose |
| --- | --- | --- |
| list_projects | Read | List projects accessible to the supplied API key. |
| list_project_requests | Read | Review a project’s request history; page and limit are explicit, not automatically exhausted. |
| transcribe_audio_url | Explicit approval required | Billable URL transcription; explicit write approval required. Returns the provider JSON transcript; no file upload or realtime audio. |

## Concrete workflow

Inspect accessible projects and request history, then approve a single URL transcription. Long audio may exceed the bounded HTTP timeout; inspect request history before retrying an uncertain paid request.

1. list_projects
2. list_project_requests
3. transcribe_audio_url

## Optional writes

Writes are disabled by default. Set CONNECTOR_ALLOW_WRITES=true and supply `_approval: {approved:true,idempotencyKey:"unique-request-id"}` on the specific call. Do not reuse a key for a different request. Uncertain outcomes are never automatically replayed; inspect the provider before another attempt.

## Capability evidence

Local: **Tested — HTTP fixtures and real stdio tools/call**. Managed: **Documented**. Provider authentication and live operations have not been established by these fixture tests. Evidence applies per operation and execution mode; setup discovery does not imply provider execution.

## Managed production

[Activate with PipMCP](https://pipmcp.com/github/start?app=deepgram&integration=deepgram-mcp&utm_source=github&utm_campaign=github-deepgram-mcp&utm_content=readme) when you want the hosted service.  Local credentials are not uploaded by this code. Review provider permissions in the managed onboarding. [Directory and related projects](https://jannikco.github.io/pipmcp-connectors/integrations/deepgram/).

## Provenance and maintenance

- https://raw.githubusercontent.com/deepgram/deepgram-api-specs/main/openapi.yml

Maintainer:jannikco. MIT license for this code. See connector.json for selected operations and integration.json for evidence. Runtime dependencies retain their own licenses. Report sensitive issues through https://pipmcp.com/contact; do not post credentials or customer data in public issues.
