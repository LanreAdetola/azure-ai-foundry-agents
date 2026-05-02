# Agent868 — Special Olympics Belgium Strategic Advisor

An AI agent that provides strategic advisory support for Special Olympics Belgium (SOB), grounded in organisational documents and supplemented with live web search. Built with Azure AI Foundry using GPT-4.1.

## What It Does

Agent868 answers strategic questions about Special Olympics Belgium — its positioning, competitive landscape, partnerships, technology initiatives, and governance challenges. It is designed for use in a nonprofit strategic planning context, not a commercial one.

## Domain Context

Special Olympics Belgium operates as a **system integrator** within Belgium's broader inclusion ecosystem. This framing is central to how the agent reasons:

- SOB is not a traditional sports competitor — it is a coordination layer between athletes, federations, municipalities, and sponsors
- Paralympic structures are **not direct competitors** — they serve elite performance, SOB serves participation and inclusion
- Partnership coordination is both SOB's core strength and its primary operational challenge
- Digital initiatives (registration platforms, data systems) are treated as foundations for governance and institutional legitimacy, not just transactional tools

These constraints are enforced in the agent's system prompt to prevent the model from defaulting to generic commercial strategy patterns.

## Key Design Decisions

### Dual retrieval — documents + web
The agent combines file_search (internal SOB documents in a vector store) with web_search_preview (live web context). This allows it to ground strategic advice in organisational reality while staying current on sector developments.

### Constrained framing
The system prompt explicitly defines what the agent must avoid — profit-maximisation framing, treating Paralympic structures as competitors, proposing technology without governance consideration. This is necessary because GPT-4.1's default strategic reasoning defaults to commercial patterns that are inappropriate for a mission-driven nonprofit.

### No hallucination on sensitive stakeholder content
Advice on partnerships, funding, and governance is grounded in retrieved documents. The agent is not permitted to invent stakeholder relationships or funding structures.

## Use Cases

- Strategic positioning analysis
- Partnership development framing
- Technology adoption recommendations (governance-first)
- Competitive landscape clarification (inclusion ecosystem vs. Paralympic vs. mainstream sports)
- Mission sustainability planning

## Configuration

```yaml
model: gpt-4.1
tools:
  - type: file_search
    vector_store_ids:
      - <your-vector-store-id>
  - type: web_search_preview
```

> Vector store ID removed. To replicate, create an Azure AI Foundry vector store, upload SOB strategic documents, and substitute the ID above.

## Known Gaps & Planned Improvements

- No temperature set — should be low (0.3–0.4) for a strategic advisory context where consistency matters
- No explicit output format defined — responses vary in structure between sessions
- No guardrail for off-domain questions (e.g. general nonprofit finance questions unrelated to SOB)
- No description field set — limits API discoverability

These are documented improvement targets, not oversights.

## What's Next

- Set temperature to 0.4 and add output format instructions
- Add an off-domain redirect guardrail
- Expose via Python SDK for integration into a simple web interface
- Explore Responsible AI evaluation using Azure AI Foundry's built-in evaluation tools
