# Azure AI Foundry Agents

A collection of AI agents built and deployed using **Azure AI Foundry**, demonstrating real-world applications of grounded retrieval, prompt engineering, and responsible AI design.

## Agents

| Agent | Purpose | Tools |
|---|---|---|
| [Examiner](./examiner/) | Study assistant that generates grounded MCQs from personal notes | File Search (RAG) |
| [Agent868](./agent868/) | Strategic advisor for Special Olympics Belgium | File Search + Web Search |

## Stack

- **Platform:** Azure AI Foundry (AI Agents SDK)
- **Models:** GPT-4.1
- **Retrieval:** Azure AI Search vector stores (file_search)
- **Grounding:** Web Search Preview (Agent868)
- **Config format:** YAML (agent definition exports)

## Design Philosophy

Both agents are built around three principles:

1. **Grounding over generation** — agents retrieve before they respond. Neither agent is allowed to answer from parametric memory alone when a knowledge source is available.
2. **Explicit failure modes** — instructions define what the agent should do when retrieval returns nothing, rather than leaving it to hallucinate.
3. **Purposeful constraints** — temperature, tool_choice, and output format are set deliberately, not left at defaults.

## Structure

```
azure-ai-foundry-agents/
├── README.md
├── examiner/
│   ├── agent-config.yaml
│   └── README.md
└── agent868/
    ├── agent-config.yaml
    └── README.md
```

## Author

**Lanre Adetola** — AI Engineer & Cloud Practitioner based in Antwerp, Belgium.  
Microsoft Azure stack: AI engineering, cloud security, DevOps, data.  
[GitHub](https://github.com/LanreAdetola) · [LinkedIn](https://linkedin.com/in/lanreadetola)
