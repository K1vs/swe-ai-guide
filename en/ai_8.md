# 8. Specification Driven Development

_Update as of spring 2026: this approach already looks not just interesting, but like the most practical base candidate for an enterprise AI development methodology._

## Philosophy

Specification Driven Development is a return to a more classical waterfall strategy of working with code. The idea can be described in one paragraph, but there are many practical details and they change dynamically: what mattered for models half a year ago may already be losing relevance now. It is a philosophy that each team adapts to its own structure and process.

The approach is not tied to one specific tool. If needed, you can use specialized tools, but the main condition is that they fit your process and do not create extra friction.

In essence, this is a return to practices described in classic engineering literature, but later abandoned because teams did not have enough time for them under the methodologies of the last decade.

## Mindset Shift

The key mindset change is this: it is normal to spend half of a task's time, or even more, on the specification, because the direct act of writing code has in practice already been solved.

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

1. Decompose into subtasks.
2. For each subtask — detail the business problem.
3. For each subtask — detail the technical solution.
4. If needed — hierarchical nesting. Depth is determined by complexity: a simple feature — a flat list, a complex system — a tree of subtasks with multiple levels.

### Validation

1. Completeness check — are all scenarios covered.
2. Consistency check — are there any conflicts between decisions.
3. Feasibility check - does each atomic unit of the plan fit into the model's context.
4. Improve the specification based on validation results - by yourself and with AI. Repeat until AI stops finding issues that are significant for you. The better the specification is, the faster AI will implement the plan.

If there is a technical risk, it can be checked quickly with a PoC using AI, separately from the main solution.

### Specification Updates

The specification is not a static document. During implementation, new details, clarifications, and edge cases appear, so the specification is updated together with the code. AI is very good at this: you describe what changed, and it updates the relevant parts of the specification.

## Specification Format

- The specification is best stored in `*.md` format - it gives both full text freedom and anchors that are convenient for both AI and humans.
- Embed diagrams in `*.md` using **Mermaid**. AI builds them excellently from text descriptions or from a picture (in Paint or pencil on paper — whatever is faster for you), and also perfectly understands the essence of a diagram from its source.
- **Do not add** DrawIO diagrams or images to the specification - they bloat the context and are often interpreted incorrectly. Convert sketches and ideas into Mermaid while building the specification.

## Working with AI

With AI there is no need to cut the specification short - it is written quickly. You give AI a dump of thoughts and facts, it structures and formats them, and then you review the result. That is why specification documents can be created very fast.

### Model Context

A single minimal atomic unit of the plan must fit into the model's context - today this is, depending on task complexity, around 1k to 3k lines of code.

> Crossing this threshold should be treated as critical - context degradation is practically the **main** reason for errors in modern models when everything needed for implementation is known and the model does not have to make assumptions.

### Model Assumptions

To reduce assumptions when there are gaps in the specification, your system prompt should state firmly that the model must **never** make assumptions and must ask questions instead.

Model assumptions are very often wrong, reduce speed, and waste tokens. Modern AI is an excellent translator, which is expected from the architecture, but an unreliable analyst and decision-maker.

### Prompts and Formulation

There are no magic prompts - this is no longer relevant for modern AI and agents, which already have built-in system prompts. It is enough to express your thoughts clearly, without extra noise, in the language you know best.

## Results

If the plan in the specification is correct, code generation itself takes about 10% of the time compared to traditional implementation of the same feature, based on the author's practice. Building a good specification can take much more time than code generation, but the total time is still clearly lower than in the traditional approach, with clearly better quality.

With a good specification, a good agent with a good model can implement each item of the plan with phenomenal quality and speed that even very strong human teams cannot reach. The important distinction is this: "full autonomy" without clear boundaries and decomposition is hype and a huge risk of mistakes, while autonomous execution of a well-specified and tightly bounded task atom inside SDD is already a reliable practical reality.

> Less total time, significantly higher quality, full test coverage, no magic code and no cut corners.

It needs no more review than code written by an average developer, and often less, provided the specification is clear and the context size is respected.

## Compatibility

All top models and agents fully support this approach and do not require any extra tools:

- **Models:** Opus 4.6, Gemini 3.1 Pro, GPT 5.3 Codex
- **Agents/IDEs:** Cursor, Copilot, Windsurf, Antigravity, Claude Code, OpenAI Codex

## Tools

The first well-known ready-made tool in this direction is [spec-kit](https://github.com/github/spec-kit) from GitHub. It gives an easy way to start with the approach, so you can try SDD without building your own process from zero. At the same time, it imposes many structures and conventions that may be unnecessary or not suitable for your project. Anything unnecessary consumes precious context window size and can make the result worse. Also, spec-kit is too universal to let you fully use newer and more specific agent tools. If you want to start somewhere but do not know where, it can be a good option. But once you have enough understanding and experience, a custom SDD process usually gives a better result.

## Sources

- [Spec-Driven Development & Spec-Kit - Microsoft Developer Blog](https://developer.microsoft.com/blog/spec-driven-development-spec-kit)
- [Spec-Driven Development with AI: Get Started with a New Open Source Toolkit - GitHub Blog](https://github.blog/ai-and-ml/generative-ai/spec-driven-development-with-ai-get-started-with-a-new-open-source-toolkit/)
- [SDD Tools - Martin Fowler](https://martinfowler.com/articles/exploring-gen-ai/sdd-3-tools.html)
