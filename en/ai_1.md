## 1. AI - tool #2 right after the developer’s mind

Modern AI in development is a jump beyond a “better IDE”: it adds speed, reduces routine to near zero, and raises quality by freeing human time that can be used for well‑known quality practices that never had time. Used correctly, AI does not replace thinking; it amplifies it, turning ideas into results much faster and more reliably.

### Why now

- **Accessibility**: getting started is very simple. You can proceed step by step, adding new AI use cases as needed and as you are ready. Start with tools you already use and install AI extensions for them.
- **Context**: models can already hold enough context to complete a step of a typical decomposed task in a typical project.
- **Quality**: under the supervision of a person who can manage task decomposition, verify and adjust the plan, AI can perform tasks with an acceptable level of quality.
- **Speed**: some tasks, especially simple and typical ones, AI can do much faster than a person. AI can also quickly complete complex but very clearly described and bounded tasks that a person might spend a lot of time on. Even if the share of such tasks is small, AI reduces their duration by an order of magnitude, which noticeably increases overall development speed.
- **Tools**: today AI is not just a bare model that can only chat, but a powerful tool that can do many tasks with minimal human involvement. This almost solves last years’ problem where explaining context to AI and applying the result took longer than doing the task yourself.

## Where and how can you start using AI in development today?

This is a surface‑level list of short examples you can start using today. Do not treat it as exhaustive, but it is a good start. How to do it is also described very briefly, but this will already be a good beginning.

### 1) Tests: unit and integration

- **Describe the API**: describe the API of the module you test right away. Add the file or folder with it into context.
- **Work step by step**: do not give the agent a too general request like “write tests for all methods.” Describe each test separately: name, preconditions, steps, expectations, and what to mock. This is a bit longer, but you get exactly the tests you need and you also re‑check the validity of the requirement.
- **Grow gradually**: “happy path” → negative scenarios → edge cases. The more tests the module has, the better AI generates the next, more complex tests.

Result: good test coverage for little cost that can grow gradually; the cost of each new test keeps decreasing.

### 2) XML comments, logs, traces: autocomplete “out of the box”

- **Automate built‑in documentation**: if the method body is clean and without “spaghetti,” AI confidently completes XML comments, parameter and return descriptions.
- **Logging and tracing**: provide a template for what and how to log, and the agent will do it quickly. For new code, rely on autocomplete which adds the needed log by context in seconds.

Result: documentation and diagnostics do not slow you down, do not overload the developer, but sharply improve observability and clarity of the program’s behavior.

### 3) Implement business logic by contract

- **Business logic**: copy the required fragment of the requirements into context or refer to the ticket number in Jira (if MCP is available).
- **Contract**: define the contract and create an empty method with the signature that needs to be implemented.
- **Tests**: write tests for the contract according to the requirements; if the ticket has acceptance criteria, AI will cope with minimal interventions.
- **Implementation**: ask AI to provide the implementation - it will write code that meets the requirements, the contract, and the tests.
- **Iterate**: adjust the code as needed, by hand or with the agent, until it is correct and meets the desired quality.

Result: fast and high‑quality implementation of business logic.

### 4) Work by analogy and spread solutions

- **Create an example**: create the example manually or with assistance that you need to spread.
- **Add to context**: add the example to context and describe what to pay attention to in it.
- **Spread**: specify where to apply the example, and AI will do it for you.

Result: scaling best practices without manual routine and standardization of style and practices.

### 5) Test HTTP requests and SQL scripts

- **HTTP**: by looking at the code, especially if it has well‑documented public contracts, AI can create the needed test request for the VS Code REST Client according to your wishes.
- **SQL**: using database extensions (for example, PostgreSQL for VS Code), AI can create a script to create test data or collect data from the DB and analyze it. For its work, AI can rely on the DB schema, example data, and how your code uses it, so even a basic task description gives a good result. The main rule is to never grant write access to the production DB.
- **HTTP + SQL**: together this allows AI to perform the needed check from your text description. If the check scenario is successful, you can save it as an integration test.

Result: faster testing and problem diagnostics.

## The importance of AI in development

Today, starting to use AI in development is more important than the switch from a plain text editor to an IDE was a decade ago.

The switch “Notepad → IDE” gave autocompletion, refactoring, and debugging. Adding an AI agent gives:

- **Artifact creation**: tests, mocks, built‑in documentation, telemetry, method implementations, mappings, validations - not just “helps write,” but “writes itself” from your task description.
- **Structured transformations**: complex refactoring by example or by a description across a large volume of code.
- **Code behavior analysis**: answers to how the code works, what problems are possible, what solutions exist; explanations of the cause of an already found problem.

This is a larger step than just a “better editor.” It is adding a second performer to your team. Right now, using AI in development is more important than using an IDE has been in the last 15 years.

### Not only speed: quality and reliability

- **More time for design**: AI removes routine and frees hours for domain modeling, contract alignment, and simplifying the architecture.
- **Large refactorings**: multi‑stage changes can be made quickly, and better test coverage (thanks to their low cost) increases refactoring safety.
- **Less “magic”**: where there used to be “magical” frameworks to reduce boilerplate, now you can write explicit, transparent code - the agent will generate the boilerplate. Clarity > magic.

### Synergy with DDD

- **Unambiguous context**: bounded context, ubiquitous language, aggregates, invariants - this is exactly what LLMs need. Clear names and boundaries minimize ambiguity.
- **Turning design into code**: time spent on design pays back immediately because AI can work faster and more autonomously when there is a clear technical design.
- **Evolution without breaking the language**: when the business changes, the agent allows quick updates while keeping the unity of the ubiquitous language in reality and in code.

Conclusion: DDD reduces complexity and gives AI a high‑quality, bounded context; AI reduces the cost of implementing DDD and prevents Time‑to‑Market growth.

### Synergy with TDD

- **Cheaper tests**: the time spent on writing tests is the main pain of TDD. AI radically lowers the cost of creating and maintaining tests.
- **Tests as a specification for LLM**: every test is a precise expectation. The agent “understands” what is wanted and has an explicit success criterion.

Together: TDD makes requirements clearer for AI, and AI removes the cost barrier for tests.

### Anti‑patterns to avoid

- Overloaded “do everything at once” prompts. Better: small, sequential tasks with clear artifacts at each step.
- Unclear names and no contracts. Introduce a glossary and fix interfaces before code generation.
- Using LLMs for complex, non‑typical tasks with fuzzy requirements - the result will be unclear with wasted time and tokens.

## In closing

The most important synergy is between the human brain and AI. LLMs generate many simple, trivial things instantly and reliably solve complex but standard and deterministic tasks. Humans remain unmatched where there is uncertainty: they form hypotheses, choose trade‑offs, see meaning, accumulate experience, and can abstract. Together this lets you move faster and more reliably: the machine does what can be described unambiguously, and the human directs, defines, and improves the description. AI is tool #2, and because of that it turns a strong developer’s mind into a team able to build a quality product significantly faster.

## Recommended links

- Vaswani et al., "Attention Is All You Need" (2017): [arxiv.org](https://arxiv.org/abs/1706.03762)
- Kaplan et al., "Scaling Laws for Neural Language Models" (2020): [arxiv.org](https://arxiv.org/abs/2001.08361)
- Wei et al., "Chain‑of‑Thought Prompting Elicits Reasoning in Large Language Models" (2022): [arxiv.org](https://arxiv.org/abs/2201.11903)
- Wang et al., "Self‑Consistency Improves Chain of Thought Reasoning in Language Models" (2022): [arxiv.org](https://arxiv.org/abs/2203.11171)
- Schick et al., "Toolformer: Language Models Can Teach Themselves to Use Tools" (2023): [arxiv.org](https://arxiv.org/abs/2302.04761)
- GitHub Blog - "Research: quantifying GitHub Copilot's impact on developer productivity" (2022): [github.blog](https://github.blog/2022-09-07-research-quantifying-github-copilot-s-impact-on-developer-productivity/)
- Microsoft Learn - "Develop with GitHub Copilot" (learning path): [learn.microsoft.com](https://learn.microsoft.com/en-us/training/paths/ai-developer-github-copilot/)
- Vaughn Vernon - "Implementing Domain‑Driven Design" (Addison‑Wesley): [informit.com](https://www.informit.com/store/implementing-domain-driven-design-9780321834577)
- Vaughn Vernon - "Domain‑Driven Design Distilled" (Addison‑Wesley): [informit.com](https://www.informit.com/store/domain-driven-design-distilled-9780134434421)
- Kent Beck - "Test‑Driven Development: By Example": [informit.com](https://www.informit.com/store/test-driven-development-by-example-9780321146533)
- Martin Fowler - "Refactoring: Improving the Design of Existing Code": [martinfowler.com](https://martinfowler.com/books/refactoring.html)


