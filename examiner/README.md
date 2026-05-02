# Examiner

An AI agent that generates high-quality multiple-choice questions (MCQs) grounded in uploaded study notes. Built with Azure AI Foundry using GPT-4.1.

## What It Does

Examiner retrieves content from a personal vector store of study notes and generates MCQs at varying difficulty levels. It cannot invent questions from topics not present in the source material — if the content isn't in the notes, it says so.

## Key Design Decisions

### Grounding is mandatory
`tool_choice: required` forces the agent to invoke file_search on every request. It cannot bypass retrieval and answer from model memory. This is critical for an exam preparation context where accuracy matters more than fluency.

### Low temperature for consistency
`temperature: 0.4` keeps the agent measured and reliable. MCQ generation requires deterministic reasoning — the same concept should produce a well-formed question every time, not a creatively varied one.

### Explicit failure mode
If file_search returns nothing relevant, the agent responds:
> *"That topic isn't covered in the uploaded notes."*

It does not fabricate plausible-sounding questions from topics it cannot retrieve. This was a deliberate guardrail added during iteration (v3 → v4).

### Cognitive level variation
Questions are distributed across recall, application, and conceptual understanding. Distractors are drawn from related concepts in the notes — not obvious wrong answers. This reflects standard MCQ design principles.

## Modes

| Mode | Trigger | Behaviour |
|---|---|---|
| Default | Any request | Questions + answers + explanations inline |
| Exam mode | "exam mode" or "quiz me" | Questions only, answer key revealed after `---` |
| Topic mode | Named topic | Targets that section of the notes |
| Difficulty | "easy / medium / hard" | Adjusts cognitive load accordingly |

## Iteration History

| Version | Change |
|---|---|
| v1 | Initial prompt — basic MCQ generation |
| v2 | Added 4-option constraint and distractor rules |
| v3 | Added exam mode and topic mode |
| v4 | Added explicit failure mode for empty retrieval |
| v5 | Added difficulty levels and cognitive level variation |
| v6 | Fixed option formatting (each option on its own line), added closing engagement prompt |

## Configuration

```yaml
model: gpt-4.1
temperature: 0.4
tool_choice: required
tools:
  - type: file_search
    vector_store_ids:
      - <your-vector-store-id>
```

> Vector store ID removed. To replicate, create an Azure AI Foundry vector store and upload your study notes, then substitute the ID above.

## What's Next

- Wrap in a Python script using the Azure AI Agents SDK for programmatic access
- Add session memory so the agent tracks which questions have already been asked
- Add an evaluation pipeline to score agent output against a ground truth answer key
