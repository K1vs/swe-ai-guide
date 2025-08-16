### 4. From chat to agents: from miracles to practice

Although the time of miracles is over, the time of practical use has begun. In a few leaps, LLMs jumped into the zone of high practical usefulness and keep improving steadily. But for real results, a simple chat is usually not enough.

There are fundamental limits that are far from fully solved: long‑term memory and context size. This is not only about compute resources but also mathematical complexity. Attention scales poorly, information gets diluted, and “context routing” (picking relevant information from a lot of data) becomes critical. The allowed context size is a compromise for each model. Simply increasing the window does not remove the problem; it only helps the model “not fall over.” Answer quality and speed degrade, cost grows, and errors accumulate.

#### Current fundamental limitations

- **Context length and attention complexity**: the basic attention mechanism has quadratic complexity in sequence length (O(n^2)). Even with optimizations, throughput and latency get worse as the window grows. Extending context is a compromise: the model “does not crash,” but reasoning quality, stability, and speed degrade, and inference cost grows disproportionately.
- **Information dilution and relevance**: in a large window, relevant fragments are lost in noise. The model is prone to positional and recency biases (over‑weighting last or first information), overvalues the last hints and undervalues early ones. So selection mechanisms are needed - context routing and knowledge retrieval - but they have their own errors (false positives/negatives - may pick the wrong things or miss the important ones).
- **Long‑term memory as external state**: a pure LLM has no stable memory between sessions. Any “memory” requires external stores (databases, vectors, notes) and access policies. Problems: addressing (how to find), relevance (what exactly to load), consistency (how to update without conflicts), and privacy.
- **Degradation on long chains of reasoning**: errors accumulate in a cascade. Even with step‑by‑step prompting, there is drift of instructions, loss of intermediate assumptions, and contradictions between steps. Positional encoding and limited internal state do not guarantee reliable “tracing” of long proofs.
- **Reproducibility and sensitivity to context**: the stochastic nature of sampling and high sensitivity to wording lead to variable answers. Small changes in order or form of facts yield different conclusions; full determinization often reduces quality (mode collapse).
- **Cost and latency**: long contexts and large models need significant compute (memory, bandwidth, time). This limits interactive scenarios and production scale, forcing trade‑offs among quality, speed, and price.

#### Using chat only exposes common difficulties:

- **Establishing context**: it is hard to load large material in a structured way, keep it up‑to‑date, and relevant.
- **High prompting demands**: you must craft precise instructions, build chains of hints, and control style and output format.
- **Applying the result**: integrating answers into work artifacts (code, docs, data) is often manual, tedious, and error‑prone.
- **Preserving progress**: you need mechanisms for memory - setup prompts, personal preferences, work contexts, and prompt reuse.
- **Reproducibility and control**: without verification and logging tools, it is hard to guarantee process stability and final quality.

From here the idea of an **LLM agent** grows naturally. An agent is not just a chat, but a system that creates sub‑tasks, plans steps, calls tools (memory, file system, repositories, execution environment), evaluates intermediate results, and corrects the course.

Key properties of an agent: task decomposition, use of tools, iterative checking, stable state/memory, and controlled context routing (selecting needed information) and knowledge retrieval for the task.

The agent’s goal is not “generate an answer to a prompt,” but to organize execution of a process with constraints, acceptance criteria, and checks.

Here is an example in programming where an agent is much stronger than chat: migrating code to a new framework version in a monorepo. The agent:
1) scans the repo and builds a migration plan;
2) finds locations where APIs change;
3) makes local edits in batches, runs tests and linters;
4) collects error logs and refines the plan;
5) updates documentation and prepares a pull request with a clear diff.
Plain chat will give code fragments or advice, but will not run the full “plan → changes → checks → report” cycle.

Another example is fixing a flaky test (a test that sometimes fails for no clear reason). The agent can automatically reproduce the bug, vary the environment, collect artifacts (logs, traces), propose a patch, run tests in a matrix of configurations, and prepare a short cause‑and‑effect report.

The key strength of the agent here is in controlling tools, memory, and feedback loops that go beyond a single chat answer.

I will cover agents in more detail in the next post.



#### Further reading

- [Retrieval-Augmented Generation for Knowledge-Intensive NLP (2020)](https://arxiv.org/abs/2005.11401) - the foundational RAG paper combining retrieval with generation.
- [A Survey on Retrieval-Augmented Generation (2023)](https://arxiv.org/abs/2312.10997) - survey of RAG variants, indexing, knowledge refresh, and evaluation.
- [ReAct: Synergizing Reasoning and Acting in Language Models (2022)](https://arxiv.org/abs/2210.03629) - a pattern for combining reasoning with tool use.
- [Toolformer: Language Models Can Teach Themselves to Use Tools (2023)](https://arxiv.org/abs/2302.04761) - training LLMs to call external tools.
- [Reflexion: Language Agents with Verbal Reinforcement Learning (2023)](https://arxiv.org/abs/2303.11366) - self-correction and memory for agents.
- [LLM-based Agents: A Survey (2023)](https://arxiv.org/abs/2308.11432) - overview of agent architectures, planning, memory, and tool use.