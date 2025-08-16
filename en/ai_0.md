# AI in Software Development

## Foreword

This series is meant to inform and discuss the use of AI in software development. The field is very dynamic, and many developers find it hard to follow news and technologies.

Marketing often raises expectations about AI in programming, which leads to two extremes: either developers consider AI unusable, or they expect AI to do everything for them. The truth is somewhere in the middle.

The goal of this series is to give a realistic picture of the capabilities and ways to use modern AI in software development, based on practical experience rather than marketing promises.

## Status as of August 2025

1. As of August 2025, AI in development is the main development tool, more important even than the IDE. Although many teams have not fully integrated AI yet due to inertia and caution, developers who actively use modern AI tools show very significant productivity gains. This is very different from 2022–2023, when AI was mostly a toy, and from 2024, when it was useful but not yet the key tool for developers.
2. The key factor behind the current AI boom is the transformer architecture and powerful LLMs (Large Language Models), which can imitate human language and to some extent reasoning. Unlike earlier neural network architectures, transformers scale well, which made it possible to train modern models on almost all text data available on the internet.
3. The first way to use LLMs was a simple chat. Despite the apparent simplicity, in practice things are not so straightforward. Because an LLM is not intelligence in the broad sense but a statistical next‑token predictor, it is critical to ask high‑quality prompts. The request is called a prompt, and the methods of crafting it are prompt engineering. Writing prompts by hand is a difficult task that requires experience and practice.
4. Even though new models are no longer breakthroughs compared to previous ones, their capabilities keep growing. The achieved level of “smartness” enabled wide development and deployment of tools based on LLMs. These tools give models “eyes and hands,” allowing them to do real work and save time. They are called LLM agents.
5. LLM agents perform different tasks using models. Usually they include a set of prepared prompts that tune the model for specific tasks and define the protocol of interaction between the model and the agent. In addition, an agent has a protocol interpreter that performs actions on the machine where it runs: browsing the file system, reading/writing files, running commands, searching the web, and so on.
6. It is hard to build one agent that can interact with all tools. Specialized extensions exist. In November 2024, the MCP protocol was proposed; it lets a tool implement an interface for an agent. This allows an agent with an MCP client to interact with a tool that has an MCP server without prior direct integration.
7. Deep AI adoption in the development process is a complex path that needs legal and technical decisions. At the same time, you can start using AI in a basic form and get most of the benefits quickly and simply. Most software development companies have an AI usage policy that you must read. Its main goal is to prevent data leaks through AI services, which is possible when using non‑corporate or personal accounts. For your personal open‑source projects, you can use any AI tool from a trusted vendor with any pricing plan, including free.

Details for each point will be covered in later posts. Please respond to this post if you want to help expand this series of publications. I will appreciate any wishes, notes, and suggestions. What's described here is just my personal opinion, though backed by other sources, so discussions in search of truth are welcome. The only request is to not post bare links to AI news without your own conclusion, since there are too many, and their reliability is very low.


