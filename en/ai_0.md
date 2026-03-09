# AI in Software Development

## Foreword

This series is meant to inform and discuss the use of AI in software development. The field is very dynamic, and many developers find it hard to follow news and technologies.

Marketing often raises expectations about AI in programming, which leads to two extremes: either developers consider AI unusable, or they expect AI to do everything for them. The truth is somewhere in the middle.

The goal of this series is to give a realistic picture of the capabilities and ways to use modern AI in software development, based on practical experience rather than marketing promises.

## Status as of early spring 2026

_This article was updated for spring 2026. Updates are marked with italic notes; outdated claims are shown with strikethrough._

1. As of spring 2026, just like in August 2025, AI in development is the main tool for software development after human judgment, more important, for example, than the IDE. Some teams still have not fully integrated AI into their process because of inertia and caution, but developers who actively use modern AI tools show very large productivity gains, and for most of them the central role of AI is no longer a bold assumption but a fact. The debate is now mostly not about whether AI became a central tool, but about how to fit it correctly into a team's own process, stack, and engineering practices. This is very different from 2022-2023, when AI was mostly a toy, and from 2024, when it was already useful but not yet the key tool for developers.
2. The key factor behind the current AI boom is the transformer architecture and powerful LLMs (Large Language Models), which can imitate human language and to some extent reasoning. Unlike earlier neural network architectures, transformers scale well, which made it possible to train modern models on almost all text data available on the internet.

   _Update as of spring 2026:_ direct model scaling has slowed down, but progress did not stop. The situation now looks more and more like CPU evolution: clock speed stopped being the main source of progress, but total system power kept growing through architecture and engineering improvements. For LLMs this means better quality, higher stability, better tool use, and a lower practical cost of mistakes. At the same time, the core limitation of the architecture is still here: models still do not have native STM and LTM, and attempts to compensate for this only by increasing context did not lead to a truly major breakthrough.

3. The first way to use LLMs was a simple chat. Despite the apparent simplicity, in practice things are not so straightforward. Because an LLM is not intelligence in the broad sense but a statistical next-token predictor, it is critical to ask high-quality prompts. The request is called a prompt, and the methods of crafting it are prompt engineering.

   _Update as of spring 2026:_ the importance of clever prompt engineering has clearly gone down. Models became better, and users now more often work not directly with a bare model but through agents with strong system prompts, action templates, and built-in workflows. What matters much more now is the ability to control context size and context quality.

   _This was true in August 2025, but is outdated now:_
   ~~Writing prompts by hand is a difficult task that requires experience and practice.~~

4. Even though new models are no longer breakthroughs compared to previous ones, their capabilities keep growing. The achieved level of "smartness" enabled wide development and deployment of tools based on LLMs. These tools give models "eyes and hands," allowing them to do real work and save time. They are called LLM agents.

   _Update as of spring 2026:_ the biggest practical jump probably happened in agents. Both the number and the quality of tools grew a lot. Agent progress now plays a role comparable to model progress, and in some scenarios it matters even more, because the agent is what turns model capability into real productivity.

5. LLM agents perform different tasks using models. Usually they include a set of prepared prompts that tune the model for specific tasks and define the protocol of interaction between the model and the agent. In addition, an agent has a protocol interpreter that performs actions on the machine where it runs: browsing the file system, reading/writing files, running commands, searching the web, and so on.

   _Update as of spring 2026:_ multi-agent work deserves special attention. A scenario where one agent can launch subordinate agents, sometimes even on other models, and coordinate their work is no longer exotic but a practical tool. This is one of the most effective ways to fight context overflow and loss of focus on large tasks.

6. It is hard to build one agent that can interact with all tools. Specialized extensions exist. In November 2024, the MCP protocol was proposed; it lets a tool implement an interface for an agent. This allows an agent with an MCP client to interact with a tool that has an MCP server without prior direct integration.

   _Update as of spring 2026:_ MCP servers appeared for almost everything they could be practically useful for. Their quality, support, and security are still very uneven, but the approach itself already became ordinary. Besides MCP, the way agents are extended with "skills" also became more or less standardized. These are ready packages of behavior, instructions, and tool integrations.

7. Deep AI adoption in the development process is a complex path that needs legal and technical decisions. At the same time, you can start using AI in a basic form and get most of the benefits quickly and simply. Most software development companies have an AI usage policy that you must read. Its main goal is to prevent data leaks through AI services, which is possible when using non-corporate or personal accounts. For your personal open-source projects, you can use any AI tool from a trusted vendor with any pricing plan, including free.

   _Update as of spring 2026:_ deep AI adoption in development is still hard, but the need for it keeps growing because the possible gains keep growing too. As agents become more autonomous, safety becomes much more serious: technical, legal, and organizational safety.

8. _New as of spring 2026:_ SDD (Specification Driven Development) is looking more and more like the practical default standard for enterprise AI use, because it helps keep control over code and quality, and often improves them, while still giving a clear speed-up in development. More on this is in [ai_8.md](ai_8.md).

Details for each point are covered in the later posts of the series. Please respond if you want to help expand this series of publications. I will appreciate any wishes, notes, and suggestions. What is described here is only my personal opinion, though backed by other sources, so discussion in search of truth is welcome. The only request is to not post bare links to AI news without your own conclusion, because there are far too many of them and their reliability is very low.

[List of series updates as of early spring 2026](upd_ai_2.md).
