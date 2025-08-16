### 7. Bringing AI into development processes

AI will significantly change familiar processes and methodologies of software development in the coming years. At the same time, there is still no clear “map” of what and how exactly to change, and the constant expansion of model capabilities adds uncertainty. This should not stop adoption: start with point integrations into those places of existing processes where AI already gives a clear boost in speed and quality.

### Safe use of AI in corporate development

The main rule: for any work tasks, use only corporate licenses and accounts of approved AI tools; personal or free accounts for working with company code and data are prohibited. This ensures enterprise privacy: data isolation, no training on your content, audit, SSO/SAML, and access control. The rest is common sense: do not paste secrets/PII into prompts and minimize the volume of context you send to the model.

An extra risk‑reduction option is running LLMs locally. For example, models like Gemma 3 can be run via Ollama or LM Studio, keeping data inside your infrastructure. This greatly reduces the probability of leaks but requires hardware resources and some ML expertise, and results are usually more modest than flagship cloud models.

There is also a less likely but real risk of license incompatibility: an LLM can generate code fragments whose license does not comply with company policies. Protection against such situations relies on provider reliability and careful use of LLMs when generating analogs of commercial algorithms.

### Tools for developers

GitHub Copilot in new versions goes far beyond autocomplete: it is effectively an agent that understands workspace context, helps with PRs and issues, generates tests, explains code, navigates projects, and runs commands. It is available in most popular IDEs - from VS Code and JetBrains to Visual Studio. In enterprise settings, Copilot is purchased within GitHub organizations; if the tool is set up in one organization and repositories are in another or outside GitHub, some features may be limited by access and integration policies.

Cursor is a separate IDE designed for agent‑assisted development. It works deeply with the working folder, enabling “conversational” edits and running common tasks in the background with asynchronous agents. Since Cursor is a fork of VS Code, not all extensions are compatible: the authors offer their own alternatives for the most popular plugins, but sometimes they are not powerful or convenient enough.

Windsurf evolved from an extension into a full IDE tailored for AI‑assisted development needs. Results are often similar to Cursor, but the approach has specifics: it has its own lightweight models for trivial tasks (they are fast, though less powerful) and limited plugins for other IDEs. The separate IDE implementation makes the environment fast and light, but some functions may be missing; before adoption, check support for your stack. Extensions partly reduce the problem but do not eliminate it.

### Access to model APIs

Access via Copilot, Cursor, or Windsurf does not provide “free” API keys to models. If you need integration into internal services or backends, buy APIs directly from providers like OpenAI, Google, or Anthropic (Claude) or through aggregators like OpenRouter, which provide access to different models under one contract.

API keys are useful to developers to build their own agents and RAG systems, create internal tools and bots, integrate checks into CI, and for semi‑automated migrations and refactoring. For a quick start you can use AnythingLLM as a boxed RAG. For semi‑manual testing of UIs, BrowserUse can help - an agent that can control a browser from text instructions and needs access to an LLM. If the infrastructure is in the cloud, Azure AI Foundry and AWS Bedrock let you connect external keys or buy models directly, providing enterprise‑level access control, monitoring, and billing.

### AI for working with requirements and tickets

In Atlassian products, Rovo is useful - a built‑in assistant in Jira and Confluence that helps search, summarize, and generate content. You can also reach Jira/Confluence via extensions or MCP servers from Copilot or agent IDEs like Cursor. In practice, LLMs save time with requirements: they concisely summarize epics and tickets, extract facts and risks, propose links between tasks, and detect duplicates. They can form acceptance criteria, checklists, and basic test scenarios, and speed up grooming - from splitting an epic and estimating complexity to refining wording. After work is done, an LLM can help with release notes and short status updates based on PRs and commits.

### Transcription and meeting summaries

Transcription gives the full text of a meeting, but the main practical value is summarization: quick highlighting of key decisions, action items, risks, and open questions. For example, Fireflies integrates with calendars and video‑conferencing systems and provides APIs through which notes can be automatically loaded into internal tools.

### Sources on data‑leak and security risks

- [OWASP Top 10 for LLM Applications](https://owasp.org/www-project-top-10-for-large-language-model-applications/) - key threats (prompt injection, data leakage, access escalation) and mitigations.
- [NIST AI Risk Management Framework 1.0](https://www.nist.gov/itl/ai-risk-management-framework) - risk management framework for AI, including privacy and security.
- [NCSC (UK): Using public generative AI safely](https://www.ncsc.gov.uk/collection/guidelines-for-securing-ai/using-public-generative-ai-safely) - practical guidance to adopt gen‑AI safely and minimize leaks.
- [OpenAI: API data usage policies](https://openai.com/policies/api-data-usage-policies) - API data usage policy: whether data is used for training and what privacy controls are available.

### Links to tools and providers

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

### Summary

The potential of LLMs for development is very large. There is no single “ideal” methodology yet, but it is time to systematically adopt individual elements. The era when these tools were toys has ended, and the period when using them was optional is quickly ending.


