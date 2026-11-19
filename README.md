# Valdra for Claude

Valdra is a Canadian privacy and AI governance product from Canuckt Synergy Solutions Inc., a Canadian privacy company based in Nova Scotia. This plugin connects Claude to the Valdra connector and adds three guided skills, in English or French.

## What it adds

- **Canadian privacy readiness check** (`canadian-privacy-readiness`): asks the yes or no questions of Valdra's free readiness check (PIPEDA, Quebec Law 25, CASL and AI governance) in plain words, scores the answers out of 100, and explains the top gaps and the step that closes each, with a link to Valdra's free full assessment.
- **Privacy policy draft** (`privacy-policy-draft`): collects a few facts about a business in a Canadian province or territory and fills Valdra's reviewed privacy policy template, in English or French, then lists what to check before publishing.
- **EU AI Act risk check** (`ai-act-risk-check`): asks the yes or no facts that matter for an AI use case and explains the risk tier, the obligations with their articles and dates, the role of provider or deployer, and other AI laws that may also apply.

Each skill works in French when you write in French.

## What it connects to

The plugin declares one remote MCP server in `.mcp.json`:

```json
{ "mcpServers": { "valdra": { "type": "http", "url": "https://mcp.valdra.ai/mcp" } } }
```

It offers four read only tools: `privacy_readiness_questions`, `privacy_readiness_score`, `privacy_policy_draft` and `ai_act_risk_classify`. The answers and business facts you give in a conversation are sent to this server to produce the result. The tools are rule based, and the server says nothing about the business or the answers is stored. The plugin runs no local code, has no hooks, and needs no account or key.

## Install

Load it for one session with `claude --plugin-dir ./valdra-claude-plugin`, or install it from a marketplace that lists it. Then ask, for example, "Is my Nova Scotia clinic ready for Canadian privacy law?" or "Draft a privacy policy for my Quebec shop."

## Important

Results are a screening and a starting draft from fixed rules, not legal advice. Have a qualified person review anything before you rely on it or publish it.

More information: https://valdra.ai/claude-connector. Privacy policy: https://valdra.ai/privacy. Terms: https://valdra.ai/terms.

## License

MIT. See `LICENSE`.
