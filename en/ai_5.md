### 5. LLM agents for software development: practical autonomy, not magic

An LLM agent for software development is a tool built on top of a large language model. It reads repository context, plans small steps, and performs actions (edits files, runs commands, writes tests) on the engineer’s request.

Unlike a simple chat, an agent follows a process: it proposes changes, shows diffs, can repeat iterations, and follows acceptance criteria.

#### Core characteristics of an agent:
- Context awareness: reads multiple files/modules, considers project structure, dependencies, and instructions in `README`/`Makefile`/CI.
- Small‑step planning: decomposes a request into a series of small edits/runs and keeps a history of attempts.
- Tool use: can call the compiler, tests, linters, package managers, scripts.
- Transparency: shows diffs/plans before applying; you can accept/decline parts.
- Reproducibility: keeps intermediate artifacts (logs, errors) and can form a PR.
- User control: any significant action only after confirmation; rollback is available.

#### Honest note on “full autonomy”.
Fully autonomous agents for complex development (multi‑module systems, non‑functional requirements, integrations, security) are not achievable today. Most end‑to‑end demos work for narrow, controlled scenarios. The “autonomous developers” in media, such as Devin, use marketing language; in real conditions their quality and stability drop sharply outside trivial tasks. In practice we need checks, reviews, tests/CI runs, and human supervision.

So the focus is on limited‑autonomy agents that work synchronously and “next to” the engineer.

#### A typical workflow in agent mode (Cursor / Copilot):
1) Define the task: select code or describe changes in natural language (e.g., “migrate library X from v4 to v5; update imports and tests”).
2) Build a plan and choose files: the agent gathers context (imports, config, dependencies) and proposes a change plan.
3) Propose diffs: it shows a series of edits per file; you accept or edit parts.
4) Local checks: runs linters/tests/build; collects logs and refines the plan on failures.
5) Wrap‑up: updates docs/scripts if needed; creates a commit or a PR draft.

#### Brief overview of popular agents

Cursor
- Pros:
  - The strongest agent core today: stable multi‑file diffs and the “plan → edits → checks” loop; it appeared earlier and has more polished scenarios.
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
  - Strong for inline suggestions; convenient for small local edits.
- Cons:
  - As an agent for multi‑step/multi‑file changes, it lags behind Cursor; fewer tool‑based scenarios inside the IDE.
  - Less control over model choice; harder to optimize for specific tasks/cost.
  - Autocomplete quality depends more on the active file and sometimes looks more general.

Console agents (e.g., Claude Code) - when it is convenient:
- Editor‑agnostic: you work in terminal, tmux/SSH, remote environments/containers without a heavy IDE.
- Scripting and CI: CLI/API lets you run tasks non‑interactively, store artifacts (logs, reports), output diffs/patches to files, and return exit codes. It is convenient for GitHub Actions/GitLab CI to run mass lint/fix, generate tests/docs, and audits with pipeline fail on violations.
- Scale and overview: run repository‑wide tasks (mass searches/refactors, dependency inventory, deprecated API search). Form summary reports (HTML/Markdown/JSON), return diffs as `.patch` for review. Works the same locally, in CI, and on remote machines.

#### Non‑autonomous scenarios - autocomplete/inline chat in the IDE - are sometimes better than agent mode:
- Small local changes and the “hot” edit loop when the cost of plan/diffs exceeds the benefit.
- High style/security demands: you want full control of every line.
- Learning a new API: hints/snippets help wire up sample code faster without extra transformations.

#### More autonomous scenarios: asynchronous agents
- Cursor and Claude Code have async mode: long tasks (mass refactors, generating tests/docs, metrics, dependency inventory) run in the background; after completion you get a report and diffs for review. This is useful when work takes tens of minutes and should not block active editing.
- There are “mostly async” products like Google Jules, aimed at longer, multi‑step tasks with minimal user involvement. Their strengths are planning, environment watching, and plan repair on failures; but quality and predictability are still far from what is acceptable for critical production without human control.

For specific tasks, for example upgrading dependencies with breaking changes using release notes, this can be useful. Or replacing one framework or library with an equivalent. In the future this may become useful for a wider set of tasks.

#### Practical advice for choosing a mode:
- Minimal necessary autonomy: pick the level that solves the task with the least overhead.
- Inline suggestions - for local edits, templates, and small functions.
- Agent in the editor - for changes across several files, mechanical migrations, systemic refactorings.
- Async agent - for long, noisy, resource‑intensive procedures that can be described unambiguously in one prompt and are easy to verify with reports/diffs.
- Always demand transparency: preliminary plan, per‑file diffs, run logs, and repeatable steps.

The lower bound of truth is this: agents already save hours on routine, but without human engineering judgment - not a step. The best results come from combining clear task formulation, small iterations, test checks, and careful code review. This is how agents become a productivity multiplier rather than a source of hidden debt.



#### Sources and further reading

- Overview: Lilian Weng - “LLM Powered Autonomous Agents” (`https://lilianweng.github.io/posts/2023-06-23-agent/`)
- ReAct (Yao et al., 2022): “ReAct: Synergizing Reasoning and Acting in Language Models” (`https://arxiv.org/abs/2210.03629`)
- Toolformer (Schick et al., 2023): “Language Models Can Teach Themselves to Use Tools” (`https://arxiv.org/abs/2302.04761`)
- Reflexion (Shinn et al., 2023): “Language Agents with Verbal Reinforcement Learning” (`https://arxiv.org/abs/2303.11366`)
- LangGraph (LangChain, 2024): graph-based agents and orchestration (`https://langchain-ai.github.io/langgraph/`)
- LangChain - Agents: concepts and examples (`https://python.langchain.com/docs/concepts/agents/`)
- LlamaIndex - Agents: overview and guides (`https://docs.llamaindex.ai/en/stable/module_guides/agent/`)
- Microsoft AutoGen: multi-agent conversations and coordination (`https://microsoft.github.io/autogen/`)
- Anthropic Claude - Tool Use / Function Calling (`https://docs.anthropic.com/claude/docs/tool-use`)
- OpenAI - Assistants API and tools (`https://platform.openai.com/docs/assistants/overview`)
- AgentBench: benchmarking agents (`https://github.com/THUDM/AgentBench`)
- SWE-bench: benchmark for software-engineering agents (`https://github.com/princeton-nlp/SWE-bench`)