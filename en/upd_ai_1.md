# Update on Models and Capabilities as of End of 2025 (November 26, 2025)

In general, my predictions and expectations regarding models and their capabilities have not changed significantly. As I said before, the capabilities of the transformer architecture are almost exhausted, and now we only see quantitative improvements. Such quantitative improvements do not change the approaches to using AI in development described by me in previous articles, but significantly increase the performance gain and comfort from their use. If back in the summer, even those tasks that AI solves well were not always profitable to entrust to it due to unreliability and slow speed, now entrusting a suitable task to AI almost always brings more benefits than losses. The idea that AI is the main tool of a developer has now been fully confirmed (but one should not forget about the rest of the tools).

## Models

Here I describe my experience; on the one hand, it may be biased, but considering the marketing boom, practical experience is often much more useful than advertising charts and benchmarks far from real tasks. It is worth noting that all the latest models from top players (OpenAI, Anthropic, Google) are very close in capabilities, but still, there are certain strengths and weaknesses of each model.

### 1. GPT-5.1 and GPT-5.1 Codex

Models from OpenAI. The first is more general, the second is more specialized in development.
Very versatile, inexpensive in terms of tokens. They show themselves quite well in complex tasks.
But there is a big minus - like their predecessors GPT-5 and GPT-5 Codex, they are quite slow, with unstable speed, which greatly reduces productivity and comfort of working with them.
They can be interesting in cases where the main model failed, or the result raises doubts and requires verification. I would not recommend it as a default model for development.

### 2. Claude Sonnet 4.5 and Claude Opus 4.5

Models from Anthropic, basically designed for programming tasks. Sonnet 4.5 is cheaper and suitable for simple tasks. Opus 4.5 is more expensive and suitable for complex tasks. But in version 4.5, the differences between them are not as great as in previous versions; in terms of price, Opus 4.5 is sometimes cheaper on complex tasks because it finds a solution in fewer tokens. Therefore, both Opus and Sonnet can become your default models depending on your preferences, or you can change them depending on the task. The models are fast, and somewhat verbose, but this can be controlled using prompt engineering. Compared to other leaders, they will probably be the most expensive, especially on simple tasks, where if you are already used to Anthropic models, you can use Haiku 4.5 to save money. But in any case, they are worth their money and are a good default choice for development.

### 3. Gemini 3 Pro

A model from Google. It is not specialized for programming tasks, but has good capabilities for development. The model is approximately equal in speed to Claude Sonnet 4.5, but more stable in this performance, which is pleasant for working in interactive mode. A very big plus of the model is the combination of its obedience, minimum of self-activity, and stable considerable speed of work. This is especially valuable when a developer uses the model for interactive work on small subtasks - and it is this mode of operation that is most productive and does not degrade code quality. In addition, the model works great with tools, for example, a browser, emulates spatial imagination well, which makes it perhaps the best for frontend development. And for the backend, the model is also a good candidate for the role of default, and the choice between it and Anthropic models is a matter of taste.

## Tools

Little has changed here, but I will describe the main points again; perhaps it will be interesting for those who are choosing now.

### 1. GitHub Copilot

Still lags behind the leaders in capabilities and speed. But it still leads in ease of use and adaptation to your stack, as it is present for most popular IDEs in almost full form. It works best in VS Code, but in other IDEs, the limitations and problems are insignificant. It also received its own CLI, which allows using it without an IDE. It remains the optimal choice for those who do not want to change their usual development tools. But one should not forget about the binding to GitHub and the limitations associated with it (described in the previous article).

### 2. Cursor

Still leads in capabilities and speed. It has the best autocomplete, which is fast and of very high quality. And it still has certain problems and limitations for some development stacks, which depend on licensed components and extensions for VS Code. The possibilities for working with asynchronous agents have grown significantly, and there is a convenient interface for controlling them. New, more powerful models increase the range of effective application of the approach with asynchronous agents, but so far there are few tasks where this is really justified.

### 3. Windsurf

Also a great option for transition if the developer uses an IDE with Windsurf plugin support. Since the developer has the opportunity to use an extension for the start, which provides basic capabilities in their usual IDE, and in parallel, if possible, without loss of productivity, master a separate Windsurf IDE (fork of VS Code, like Cursor, with the same problems). Interesting for its focus specifically on the agent approach, with minimization of manual code writing, which becomes increasingly relevant with the development of the quality and speed of models.

### 4. Claude Code from Anthropic or Codex Cli from OpenAI or Gemini CLI from Google

Purely console tools tailored to the models of their vendor. They are the first to receive many interesting features, but still, on their own, they are suitable only for agent development. And banal AI autocomplete is often more optimal for many tasks. I still cannot recommend it as a main tool, but if there is an opportunity to try it as an addition to other tools, it can be useful, as the agent approach to development becomes increasingly viable.

### 5. Google Antigravity

IDE based on VS Code, with great agent capabilities. A novelty from Google, suitable for development with different levels of agent autonomy. So far only a preview, but it looks very similar to Cursor in its current form both in idea and capabilities. If Google can ensure better support for plugins for VS Code, develop its own or agree with Microsoft, then this can become a very interesting option for development. For now, we are observing and playing, it is too early for real projects.

*And finally, let's not forget that although AI is growing very well quantitatively, qualitatively it is standing still for now. Therefore, despite all the hype and marketing, do not forget about the rest of the developer's tools, and most importantly about the developer's mind and skills!.*
