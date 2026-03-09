# 7. Bringing AI into development processes

_This article was updated for spring 2026. Updates are marked with italic notes; outdated claims are shown with strikethrough._

_Update as of spring 2026:_

By early spring 2026, we can already speak not only about future impact, but about the fact that AI has really started to change familiar software development processes and methodologies. This still does not mean the whole industry has already moved to one new "correct" way of working, but old processes are more and more often not optimal for an environment where a large part of analysis, coding, checks, and preparation is done by agent tools. At the same time, there is still no clear universal "map" of what exactly must be changed and how, and the constant growth of model capability adds uncertainty. This should not stop adoption: start with point integrations into those places of existing processes where AI already gives a clear boost in speed and quality.

_This was true in August 2025, but is outdated now:_
~~AI will significantly change familiar processes and methodologies of software development in the coming years.~~

## Safe use of AI in corporate development

The main rule: for any work tasks, use only corporate licenses and accounts of approved AI tools; personal or free accounts for working with company code and data are prohibited. This ensures enterprise privacy: data isolation, no training on your content, audit, SSO/SAML, and access control. The rest is common sense: do not paste secrets/PII into prompts and minimize the volume of context you send to the model.

An extra risk-reduction option is running LLMs locally. For example, models like Gemma 3 can be run via Ollama or LM Studio, keeping data inside your infrastructure. This greatly reduces the probability of leaks, but in early 2026 the practical balance here became worse: the quality gap between local models and the best hosted models grew even more, and the hardware demands for running strong local models also grew. The worst part is that hosted models already crossed the quality threshold after which agent-based development can often be treated as the default mode, while local models still usually do not reach that threshold in most real scenarios. So local LLMs remain important for privacy, experiments, and narrow internal tasks, but in 2026 they usually do not look realistic as a universal replacement for strong cloud agents.

There is also a less likely but real risk of license incompatibility: an LLM can generate code fragments whose license does not comply with company policies. Protection against such situations relies on provider reliability and careful use of LLMs when generating analogs of commercial algorithms.

## Tools for developers

In early spring 2026, developer tools should already be understood not only as "chat + autocomplete," but as a set of agent modes with different levels of autonomy. The practical difference between an IDE tool, a separate AI IDE, and a CLI agent became much smaller than before: the borders between these product classes are getting blurred, and the choice is more and more defined not by the mere presence of agent features, but by how well a specific tool fits your process, access policies, and normal ecosystem.

GitHub Copilot in new versions goes far beyond autocomplete: it is effectively an agent that understands workspace context, helps with PRs and issues, generates tests, explains code, navigates projects, and runs commands. It is available in most popular IDEs - from VS Code and JetBrains to Visual Studio. In enterprise settings, Copilot is purchased within GitHub organizations; if the tool is set up in one organization and repositories are in another or outside GitHub, some features may be limited by access and integration policies. It is also important that Copilot is working more and more as a shell for running different agent modes, not only as one isolated assistant.

Cursor is a separate IDE designed for agent-assisted development. It works deeply with the working folder, enabling "conversational" edits and running common tasks in the background with asynchronous agents. Since Cursor is a fork of VS Code, not all extensions are compatible: the authors offer their own alternatives for the most popular plugins, but sometimes they are not powerful or convenient enough. Even so, products like this helped make agent mode an everyday workflow for many developers.

Windsurf evolved from an extension into a full IDE tailored for AI-assisted development needs. Results are often similar to Cursor, but the approach has specifics: it has its own lightweight models for trivial tasks (they are fast, though less powerful) and limited plugins for other IDEs. The separate IDE implementation makes the environment fast and light, but some functions may be missing; before adoption, check support for your stack. Extensions partly reduce the problem but do not eliminate it.

CLI agents deserve separate attention. By early spring 2026 this is no longer a "secondary" format for enthusiasts, but one of the strongest tool classes for serious agent-based development. CLI mode is especially good for long iterative repository tasks, for running on remote servers, in CI, or in semi-autonomous scenarios with strict boundaries. Claude Code is especially worth naming: it is one of the strongest practical agent tools for developers in general, not only among CLI tools. It gets new capabilities fast, works well on large repositories, fits multi-step changes, and shows how powerful native console agents from vendors have become. OpenAI Codex and Gemini CLI should also be mentioned nearby: such tools look less and less like a compromise compared to IDE mode, and more and more like a full and often even preferred way of working for some users.

At the same time, it is important to remember that a stronger tool does not remove the need for control. The closer an agent gets to real command execution, repository changes, service access, or browser interaction, the more important it is to restrict its environment, transparently review diffs and results, and not replace engineering judgment with belief in demo effects.

## Access to model APIs

Access via Copilot, Cursor, or Windsurf does not provide “free” API keys to models. If you need integration into internal services or backends, buy APIs directly from providers like OpenAI, Google, or Anthropic (Claude) or through aggregators like OpenRouter, which provide access to different models under one contract.

API keys are useful to developers to build their own agents and RAG systems, create internal tools and bots, integrate checks into CI, and for semi‑automated migrations and refactoring. For a quick start you can use AnythingLLM as a boxed RAG. For semi‑manual testing of UIs, BrowserUse can help - an agent that can control a browser from text instructions and needs access to an LLM. If the infrastructure is in the cloud, Azure AI Foundry and AWS Bedrock let you connect external keys or buy models directly, providing enterprise‑level access control, monitoring, and billing.

## AI for working with requirements and tickets

In Atlassian products, Rovo is useful - a built‑in assistant in Jira and Confluence that helps search, summarize, and generate content. You can also reach Jira/Confluence via extensions or MCP servers from Copilot or agent IDEs like Cursor. In practice, LLMs save time with requirements: they concisely summarize epics and tickets, extract facts and risks, propose links between tasks, and detect duplicates. They can form acceptance criteria, checklists, and basic test scenarios, and speed up grooming - from splitting an epic and estimating complexity to refining wording. After work is done, an LLM can help with release notes and short status updates based on PRs and commits.

## Transcription and meeting summaries

Transcription gives the full text of a meeting, but the main practical value is summarization: quick highlighting of key decisions, action items, risks, and open questions. For example, Fireflies integrates with calendars and video-conferencing systems and provides APIs through which notes can be automatically loaded into internal tools.

## Separate warning about highly autonomous agents

By early spring 2026, this is worth repeating once again: highly autonomous agents remain dangerous, and the risk scenarios can look very different. This is not only about "the agent accidentally wrote bad code." Problems can come from tool bugs, excessive permissions, unsafe integrations, prompt injection during web work, compromised artifacts, legally toxic actions done in your name, or gradual loss of control when marketing hype creates a false feeling of product maturity. That is why loud demos of autonomous modes should not be confused with safe corporate reality.

The practical rule is simple: if a tool claims high autonomy and broad access to a repository, commands, browser, cloud, or external services, you should treat it with maximum distrust and very strict limits. For more detail, see [warn_1.md](warn_1.md).

## Sources on data‑leak and security risks

- [OWASP Top 10 for LLM Applications](https://owasp.org/www-project-top-10-for-large-language-model-applications/) - key threats (prompt injection, data leakage, access escalation) and mitigations.
- [NIST AI Risk Management Framework 1.0](https://www.nist.gov/itl/ai-risk-management-framework) - risk management framework for AI, including privacy and security.
- [NCSC (UK): Guidelines for secure AI system development](https://www.ncsc.gov.uk/files/Guidelines-for-secure-AI-system-development.pdf) - guidelines for secure AI system development.
- [OpenAI: API data usage policies](https://openai.com/policies/api-data-usage-policies) - API data usage policy: whether data is used for training and what privacy controls are available.

## Links to tools and providers

- [OpenAI](https://openai.com/) - provider of GPT models; APIs for text/vision with enterprise privacy options.
- [Anthropic Claude](https://www.anthropic.com/claude) - Claude model family focused on safety and reasoning.
- [Google Gemini](https://ai.google.dev/) - Gemini models; access via Gemini API and Vertex AI.
- [xAI (Grok)](https://x.ai/) - provider of the Grok model; text‑focused APIs.
- [Copilot for Microsoft 365](https://www.microsoft.com/microsoft-copilot) - assistant across Microsoft 365 apps with org data and enterprise controls.
- [GitHub Copilot](https://github.com/features/copilot) - coding assistant in IDE/CLI with chat and completion; enterprise variants.
- [Cursor](https://www.cursor.com/) - IDE with deep LLM integration and agentic workflows.
- [Windsurf](https://codeium.com/windsurf) - AI‑first IDE by Codeium.
- [OpenRouter](https://openrouter.ai/) - aggregator offering multiple models behind a single API and billing.
- [Atlassian Rovo](https://www.atlassian.com/software/rovo) - built‑in assistant in Jira/Confluence for search, summarization, generation.
- [Fireflies](https://fireflies.ai/) - meeting transcription and summarization with integrations.

## Summary

The potential of LLMs for development is very large, and by spring 2026 it already moved from promise to practical reality: these tools started showing visible results both in development speed and in code quality. There is no single "ideal" methodology yet, but it is time to systematically adopt individual elements. Right now, SDD (Specification Driven Development) looks especially interesting and practical for enterprise development, because it combines AI advantages with control, reproducibility, and manageable quality; more on that is in [ai_8.md](ai_8.md). The era when these tools were toys has ended, and by spring 2026 the period when using them was optional has in practice ended as well.

_This was true in August 2025, but is outdated now:_
~~The era when these tools were toys has ended, and the period when using them was optional is quickly ending.~~
