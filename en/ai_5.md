# 5. LLM agents for software development: practical autonomy, not magic

_This article was updated for spring 2026. Updates are marked with italic notes._

An LLM agent for software development is a tool built on top of a large language model. It reads repository context, plans small steps, and performs actions (edits files, runs commands, writes tests) on the engineer’s request.

Unlike a simple chat, an agent follows a process: it proposes changes, shows diffs, can repeat iterations, and follows acceptance criteria.

## Core characteristics of an agent

- Context awareness: reads multiple files/modules, considers project structure, dependencies, and instructions in `README`/`Makefile`/CI.
- Small‑step planning: decomposes a request into a series of small edits/runs and keeps a history of attempts.
- Tool use: can call the compiler, tests, linters, package managers, scripts.
- Multi-agent work: can delegate separate subtasks to other agents or specialized subprocesses and then merge the results back into one working flow.
- Transparency: shows diffs/plans before applying; you can accept/decline parts.
- Reproducibility: keeps intermediate artifacts (logs, errors) and can form a PR.
- User control: any significant action only after confirmation; rollback is available.

## Honest note on “full autonomy”

_Update as of spring 2026:_

Fully autonomous agents for complex development (multi-module systems, non-functional requirements, integrations, security) are still closer to fantasy than reality. In early spring 2026 this mode looks technically closer than before, but truly reliable autonomy is still very far away. Most end-to-end demos work only for narrow, controlled scenarios. The "autonomous developers" mentioned in media, such as Devin, use marketing language; in real conditions their quality and stability drop sharply outside trivial tasks. A newer hype example is OpenClawn: it shows well that such modes became technically closer, but it does not prove that they are already safe for real work. In practice we still need checks, reviews, tests/CI runs, and human supervision.

**THE SAFETY PROBLEM OF THIS APPROACH IS ABSOLUTELY NOT SOLVED. YOU SHOULD EXPERIMENT WITH SUCH TOOLS ONLY USING PRACTICES SIMILAR TO WORKING WITH MALWARE. SEE [warn_1.md](warn_1.md).**

So the focus is on limited‑autonomy agents that work synchronously and “next to” the engineer.

## A typical workflow in agent mode (Cursor / Copilot)

1) Define the task: select code and describe desired changes in natural language (e.g., “migrate library X from v4 to v5; update imports and tests”).
2) Build a plan and choose files: the agent gathers context (imports, config, dependencies) and proposes a change plan.
3) Propose diffs: it shows a series of edits per file; you accept or edit parts.
4) Local checks: runs linters/tests/build; collects logs and refines the plan on failures.
5) Wrap‑up: updates docs/scripts if needed; creates a commit or a PR draft.

_Update as of spring 2026:_

In early spring 2026, multi-agent work became especially important. Earlier it looked more like a research scenario, but now it is much easier to use in practice. The idea is simple: instead of one agent pulling everything into one context window, it can delegate separate subtasks to subordinate agents - for example one for code analysis, one for plan building, one for result verification, sometimes even on other models. This saves context because each agent works only with its own local slice of the task. At the same time, it speeds up work because some subtasks can run in parallel, and it improves quality because instead of one overloaded context you get several narrowly focused passes that are merged afterward.

## Brief overview of popular agents

_Update as of spring 2026:_ the comparison below already reflects the current practical state of these tools, not only their basic description.

Cursor

- Pros:
  - As of early spring 2026, it still has a very good agent core, though no longer clearly the best: stable multi-file diffs and the "plan -> edits -> checks" loop; it appeared earlier and has more polished scenarios.
  - Fast autocomplete with good retention of the active work context.
  - A wider choice of models (OpenAI/Anthropic/Google/XAI), so you can pick for task, budget, and speed.
  - Suitable as an agent: synchronous sessions, command execution, iterations on errors.
- Cons:
  - A separate IDE (a fork of VS Code): not all VS Code Marketplace extensions are available due to licensing; alternatives are often weaker - verify critical plugins.
  - Habit factor: moving to another IDE can be painful for a team (shortcuts, configs, ecosystem).

GitHub Copilot

- Pros:
  - Almost “native” for VS Code; minimal friction in existing environments.
  - Available in Visual Studio with helpful features during debugging (explanations, fix suggestions using collected variable values).
  - Available in Xcode; also works in JetBrains/Neovim - covers most popular IDEs.
  - As of early spring 2026, it can run external agents such as Claude Code or OpenAI Codex directly inside Copilot with unified billing, which is very convenient if you do not want to assemble a custom tool stack yourself.
  - Strong for inline suggestions; convenient for small local edits.
  - It also got its own CLI, so it can be used without an IDE.
- Cons:
  - As an agent for multi‑step/multi‑file changes, it lags behind Cursor; fewer tool‑based scenarios inside the IDE.
  - Less control over model choice; harder to optimize for specific tasks/cost.
  - Autocomplete quality depends more on the active file and sometimes looks more general.

Windsurf

- Pros:
  - Still interesting because of its focus on an agent-first way of working and reducing manual coding.
  - Good as a transition option: you can start with integration into your usual IDE and later move into a separate environment if needed.
  - In spring 2026 it remains a good candidate for teams that want a more agent-centered workflow.
- Cons:
  - Like before, a separate IDE based on VS Code still brings old compatibility problems with part of the extension ecosystem.
  - In practice, the choice between Windsurf, Cursor, and Copilot is now more often defined not by absolute superiority, but by which flow fits the team better.

Google Antigravity

- Pros:
  - Interesting because of its agent capabilities and its approach to different levels of autonomy.
  - Looks like a serious candidate in this niche, not just an experimental demo product.
- Cons:
  - Still very early by the standards of real daily development.
  - Ecosystem, stability, and integration maturity still do not allow it to be treated as a default choice.

## Console agents (e.g., Claude Code / OpenAI Codex / Gemini CLI)

- Pros
  - IDE-agnostic: complete independence from the development environment - just open a terminal in your favorite IDE and work with the agent.
  - Remote execution: the CLI/API allows running tasks non-interactively, storing artifacts (logs, reports), outputting diffs/patches to files, and returning exit codes. This is convenient for embedding into GitHub Actions/GitLab CI for bulk lint/fix, test/doc generation, and audits with pipeline failure on violations.
  - These tools often get useful new features among the first, because vendors usually develop their own native agent shells first.
  - Very often the best pricing is here too, especially if you already prefer one specific model vendor.

- Cons
  - CLI flow is still not as comfortable for everyone as full IDE work.
  - For some tasks, console mode is still worse in visibility and control over small local edits.
  - At the same time, in early spring 2026 these disadvantages became much less important: such agents more and more often have IDE integrations instead of living fully separately.
  - The need for Tab completion also dropped sharply, because manual code writing is less and less the main way to work with these tools.

More specifically, in early spring 2026 Claude Code and OpenAI Codex deserve special attention. Claude Code is one of the strongest console agents in practical use: it gets new capabilities fast, works well for iterative repository work, and is a very strong option if your main development model is Anthropic. OpenAI Codex is especially interesting for people who already live in the OpenAI ecosystem. Both tools show how much CLI agent workflows have grown as a class.

## Non‑autonomous scenarios - autocomplete/inline chat in the IDE - are sometimes better than agent mode

- Small local changes and the “hot” edit loop when the cost of plan/diffs exceeds the benefit.
- High style/security demands: you want full control of every line.
- Learning a new API: hints/snippets help wire up sample code faster without extra transformations.

_Update as of spring 2026:_ in early spring 2026 it is important that the number of situations where this approach is truly better than agent mode keeps shrinking. Inline mode is still useful, but much less often the best default choice.

## More autonomous scenarios: asynchronous agents

- Cursor and Claude Code have async mode: long tasks (mass refactors, generating tests/docs, metrics, dependency inventory) run in the background; after completion you get a report and diffs for review. This is useful when work takes tens of minutes and should not block active editing.
- There are “mostly async” products like Google Jules, aimed at longer, multi‑step tasks with minimal user involvement. Their strengths are planning, environment watching, and plan repair on failures; but quality and predictability are still far from what is acceptable for critical production without human control.

_Update as of spring 2026:_ multi-agent scenarios also became much more accessible in practice. Earlier they often required custom orchestration, but now it is more and more common that you only need to start the right agent mode or delegate a subtask from the interface. That is what turns multi-agent work from a theoretical feature into a real daily tool.

Asynchronous modes in general-purpose products are used more and more often in spring 2026 and are becoming more practical. At the same time, products that are async-first by design are still relatively rare in real applied work: technically interesting, but not as broadly useful as general-purpose agents with a good async mode.

For specific tasks, for example upgrading dependencies with breaking changes using release notes, this can be useful. Or replacing one framework or library with an equivalent. In the future this may become useful for a wider set of tasks.

## Practical advice for choosing a mode

- Minimal necessary autonomy: pick the level that solves the task with the least overhead.
- Inline suggestions - for local edits, templates, and small functions.
- Agent in the editor - for changes across several files, mechanical migrations, systemic refactorings.
- Async agent - for long, noisy, resource‑intensive procedures that can be described unambiguously in one prompt and are easy to verify with reports/diffs.
- Always demand transparency: preliminary plan, per‑file diffs, run logs, and repeatable steps.

The lower bound of truth is this: agents already save hours on routine, but without human engineering judgment - not a step. The best results come from combining clear task formulation, small iterations, test checks, and careful code review. This is how agents become a productivity multiplier rather than a source of hidden debt.

## Sources and further reading

- [LLM Powered Autonomous Agents](https://lilianweng.github.io/posts/2023-06-23-agent/) - Lilian Weng, overview of approaches.
- [ReAct: Synergizing Reasoning and Acting in Language Models](https://arxiv.org/abs/2210.03629) - S. Yao et al., 2022.
- [Toolformer: Language Models Can Teach Themselves to Use Tools](https://arxiv.org/abs/2302.04761) - T. Schick et al., 2023.
- [Reflexion: Language Agents with Verbal Reinforcement Learning](https://arxiv.org/abs/2303.11366) - N. Shinn et al., 2023.
- [LangGraph](https://langchain-ai.github.io/langgraph/) - LangChain, 2024: graph agents and orchestration.
- [LangChain - Agents](https://python.langchain.com/docs/concepts/agents/) - concepts and examples.
- [LlamaIndex - Agents](https://docs.llamaindex.ai/en/stable/understanding/agent/) - overview and guides.
- [Microsoft AutoGen](https://microsoft.github.io/autogen/) - multi-agent scenarios and coordination.
- [Anthropic Claude - Tool Use / Function Calling](https://docs.anthropic.com/claude/docs/tool-use)
- [OpenAI - Assistants API and tools](https://platform.openai.com/docs/assistants/overview)
- [AgentBench](https://github.com/THUDM/AgentBench) - comparative evaluation of agents.
- [SWE-bench](https://github.com/princeton-nlp/SWE-bench) - benchmark for software engineering agents.
- [Cursor documentation](https://docs.cursor.com)
- [GitHub Copilot documentation](https://docs.github.com/en/copilot)
