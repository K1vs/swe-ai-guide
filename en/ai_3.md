### 3. Basic interaction with an LLM through chat

An LLM is not a thinking subject but a powerful statistical next‑token predictor. Because of this, answer quality depends much more on the wording and context of the input than in usual human communication.

The basic interaction looks like this:
- the user formulates a prompt (instructions, questions, examples) and sends it with the dialog context;
- the model sequentially predicts the next tokens and forms a reply;
- chat history accumulates context, so relevance and clarity of input are critical.

Input to an LLM is called a “prompt,” and the techniques to build effective prompts are “prompt engineering.” These appeared in response to the high sensitivity of models to the wording and structure of the request.

Here is a list of practically effective prompting methods today that I regularly use:
1. Give the AI a role. Copilot already does this, setting a developer role, but you can clarify it with language, framework, and extra technologies. It is very important to state that it must create production‑ready code (with error handling, logging, documentation).

   Examples of roles:
   - “You are a senior .NET developer with 10+ years of experience. Write production‑ready code with error handling and logging.”
   - “You are a QA engineer. Create a test plan for this API, including edge cases.”
   - “You are a security expert. Analyze this code for vulnerabilities and propose improvements.”

2. Explicitly ask to create a plan before doing the task. If needed, split it into sub‑steps; for each step, state the reason and consequence, check causal links, make sure the plan can complete the task and will not cause side effects.

3. For complex tasks first ask only for the plan and tell it to stop. If the plan is poor, stop and describe the problems. For large tasks ask to save the global plan into a separate .md file and mark completed steps - this helps refresh context without losing progress and make intermediate commits.

4. If the task meets a large codebase, ask to explore the seam line, decide whether refactoring is needed, and if yes, add the needed steps to the start of the plan.

5. When designing solutions, it can help to generate alternative plan branches, compare them, criticize them, choose the best, discard dead ends, and go back when needed.

6. To check solutions, ask the AI for a counterexample or a scenario where the proposed approach might fail. For example: “Under what conditions will this algorithm be inefficient?” or “What edge cases can cause problems?” This helps find weak spots at the planning stage.

7. Evaluate solutions by criteria: maintainability, scalability, reusability, security, performance, and so on. Not all at once - pick 3–4 most important for the current task. You can also set priorities.

8. To reduce hallucinations, it sometimes helps to ask for a confidence level from 1 to 10 when creating a plan. This reduces made‑up facts and gives points for extra checking.

9. The best prompt structure:
- Context (what it is about)
- Task (what to do)
- Notes (strategy, what to focus on, what is desired/undesired, etc.)

   Example:
   ```
   **Context:** I have an ASP.NET Core Web API with authorization via JWT tokens.
   The UserService has a method GetUserById() that returns null for non‑existing users.

   **Task:** Create an endpoint GET /api/users/{id} that returns user data or 404.

   **Notes:**
   - Use standard HTTP status codes
   - Add logging at Information level
   - The method must be async
   - Do not use magic strings for logs
   ```

   Sometimes it makes sense to change the order, especially if a note keeps being ignored.

10. Some things are faster to do manually. If you see the AI “stuck,” stop it and help by describing how you did it. Then it can continue and adapt.

11. TDD works well with AI. You can state this explicitly in the planning task: first create empty contracts, then write tests, and only then write code. All these should be separate steps in the plan. This effectively gives another intermediate stage: text plan → contracts + tests → implementation. An extra stage is another chance for timely intervention and correction of drift, which grows catastrophically in LLMs.

12. Ask to support decisions with links, for example for solutions based on facts about technologies or libraries, require links to those facts. Even if you do not read them, this can sometimes protect you from hallucinations.

Many prompting rules that were critical for early LLMs are now either less important or already built into the models. Also, many AI tools apply system prompts and other settings under the hood automatically.

However, the skill of building good prompts remains useful in complex, non‑trivial, and domain‑specific cases where you need control, reproducibility, and precision.



### Sources and further reading

- [Prompt Engineering Guide](https://www.promptingguide.ai) - DAIR‑AI, ongoing.
- [Prompt engineering best practices](https://platform.openai.com/docs/guides/prompt-engineering) - OpenAI, guide.
- [Prompt engineering overview](https://docs.anthropic.com/en/docs/build-with-claude/prompt-engineering/overview) - Anthropic, overview.
- [Prompt Engineering](https://lilianweng.github.io/posts/2023-03-15-prompt-engineering/) - L. Weng, 2023.
- [Chain‑of‑Thought Prompting Elicits Reasoning in Large Language Models](https://arxiv.org/abs/2201.11903) - J. Wei et al., 2022.
- [Self‑Consistency Improves Chain of Thought Reasoning in Large Language Models](https://arxiv.org/abs/2203.11171) - X. Wang et al., 2022.
- [Least‑to‑Most Prompting Enables Complex Reasoning in Large Language Models](https://arxiv.org/abs/2210.14216) - Z. Zhou et al., 2022.
- [ReAct: Synergizing Reasoning and Acting in Language Models](https://arxiv.org/abs/2210.03629) - S. Yao et al., 2022.
- [Tree of Thoughts: Deliberate Problem Solving with Large Language Models](https://arxiv.org/abs/2305.10601) - S. Yao et al., 2023.
- [Program of Thoughts Prompting: Disentangling Computation from Reasoning for Numerical Reasoning](https://arxiv.org/abs/2211.12588) - X. Lei et al., 2022.
- [Pre‑train, Prompt, and Predict: A Systematic Survey of Prompting Methods in Natural Language Processing](https://arxiv.org/abs/2107.13586) - P. Liu et al., 2023.