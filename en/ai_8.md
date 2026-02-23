# Specification Driven Development

## Philosophy

Specification Driven Development is a return to a more classical waterfall strategy of working with code. The idea can be described in a single paragraph, but there are many practical aspects and they change dynamically: what was important for models half a year ago is now losing relevance. It is a philosophy that everyone tailors to their own structure.

There is no need to use any specific tool. But if you want to — you can, as long as it fits and doesn't become a problem getting in the way of your flow.

In essence — do everything that the old books wrote about and that the methodologies of the last ten years have been cutting corners on.

## Mindset Shift

You need to shift your mindset to accept that you can spend half the time on a task — or even more — on the specification. The coding task as such has been solved today and no longer exists.

The key is to allow yourself to have no code until the very last moment, and instead work with text at a higher level of abstraction, where knowledge is compressed to its essence and it is easier to stay within the model's context size.

## Specification Building Process

Every step below is documented — the specification is a living artifact that accumulates all decisions.

### Description

1. Clearly define the problem.
2. Sketch out the solution.
3. Describe individual important scenarios in detail — how they work.
4. Describe technical solutions at various scales.
5. Describe the code style.
6. Describe the testing approach.
7. Describe integrations, the role of the current module within them, etc.

### Decomposition

8. Decompose into subtasks.
9. For each subtask — detail the business problem.
10. For each subtask — detail the technical solution.
11. If needed — hierarchical nesting. Depth is determined by complexity: a simple feature — a flat list, a complex system — a tree of subtasks with multiple levels.

### Validation

12. Completeness check — are all scenarios covered.
13. Consistency check — are there any conflicts between decisions.
14. Feasibility check — does each atomic unit of the plan fit within the model's context.
15. Improve the spec based on validation results — by yourself and with AI. Repeat until the AI stops finding issues that are significant to you. The higher the quality of the specification, the faster AI will implement the plan.

If there is a technical challenge — it can be quickly PoC'd through AI as well, separately from the main solution.

### Specification Updates

The specification is not a static document. During implementation, new details, clarifications, and edge cases emerge — the spec is updated alongside the code. AI is excellent at this: you describe what changed — it updates the relevant sections of the specification.

## Specification Format

- The spec is best stored in `*.md` format — it offers both full textual freedom and anchors that are convenient for both AI and humans to latch onto.
- Embed diagrams in `*.md` using **Mermaid**. AI builds them excellently from text descriptions or from a picture (in Paint or pencil on paper — whatever is faster for you), and also perfectly understands the essence of a diagram from its source.
- **Do not add** diagrams drawn in DrawIO or images to the spec — they bloat the context and are often interpreted inaccurately. Convert sketches and ideas into Mermaid at the spec-building stage.

## Working with AI

With AI there is no reason to cut corners — specs are written quickly. You dump your thoughts and facts to AI — it structures and formats — you review the result. That's why spec documents are produced very quickly.

### Model Context

A single minimal atomic unit of the plan must fit within the model's context — currently this is, depending on task complexity, from 1k to 3k lines of code.

> Exceeding this threshold is critically unacceptable — context rotting is practically the **only** cause of errors in modern models, provided that everything needed for implementation is known and the model makes no assumptions.

### Model Assumptions

To make the model assume less when there are gaps in the spec, your system prompt must firmly state to never make assumptions, **never**, but to ask questions instead.

Model assumptions are very often wrong and destroy velocity while consuming tokens — modern AI is an excellent translator (unsurprising given the architecture), but a poor analyst and decision-maker (which is also expected).

### Prompts and Formulation

There are no magic prompts — this is no longer relevant for modern AI and agents, which already have all these prompts built in. Simply articulate your thoughts clearly, without fluff, in the language you know best.

## Results

If the plan in the spec is correct — code generation itself takes ~10% of the time compared to traditional programming of the same feature. Building a quality specification can take significantly more time than code generation, but the total time is still noticeably less than the traditional approach — with a noticeable increase in quality.

With a quality spec, a good agent with a good model implements each item of the plan with phenomenal quality and speed that is unattainable by the best human teams.

> Less total time, significantly higher quality, full test coverage, no magic code and no cut corners.

Requires no more review than code written by a mid-level developer, or even less — provided the spec is clear and context size is respected.

## Compatibility

All top models and agents fully support this approach and require no additional tools:

- **Models:** Opus 4.6, Gemini 3.1 Pro, GPT 5.3 Codex
- **Agents/IDEs:** Cursor, Copilot, Windsurf, Antigravity, Claude Code, OpenAI Codex
