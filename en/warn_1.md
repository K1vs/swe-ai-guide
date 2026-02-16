# Warning About Autonomous Agent Tools (OpenClawn as an Example)

## TL;DR

OpenClawn (ex. ClawdBot, Moltbot) is a highly autonomous agent with elevated permissions by default, built-in web search, and additional modules — thousands of which have already been created.

Despite the hype (and buying of the tool by OpenAI), it is **not recommended** for any real-world tasks, as the current risk level is unacceptable. In its present form, it is more of a dangerous "toy" that should only be experimented with using approaches similar to malware research.

**Important:** although this text uses OpenClawn as an example, the risks described apply to **any** highly autonomous agent with broad permissions. This is a problem of the solution class, not a specific product.

## Risk Categories

Risks can be divided into two groups:

- Accidental (bugs, errors, incorrect actions without malicious intent)
- Intentional (attacks/influence by malicious actors)

---

## 1) Accidental Errors and Bugs

The tool may be raw and buggy. Combined with auto-approvals, this can lead to severe situations due to errors, for example:

- deletion or corruption of your data;
- populating data with content that looks "normal" on the surface but is incorrect;
- sending an email/message with absurd or dangerous content;
- deploying a flawed product to the cloud with reputational or financial losses;
- other scenarios where the result looks plausible but is wrong.

Practical takeaway: everything you give such an agent access to can be ruined simply due to a bug.

### Why Running in a VM Doesn't Always Help

You can run the agent in a VM without personal data or credentials, with limited internet access (only to the model provider). But if you **don't give the agent "hands"** (tools/access for actions in the system, network, repositories, cloud), it essentially becomes a **regular chatbot**, and the practical value of an autonomous agent disappears.

Between the extremes of "full autonomy" and "chatbot without hands" there is a spectrum of intermediate options: human-in-the-loop (confirmation for each dangerous action), read-only modes, sandboxed execution with a limited set of allowed operations. While this does not guarantee safety, having a human as a validator can eliminate most of the most powerful and destructive errors and attacks. This is currently the recommended way to apply AI in real-world tasks.

Separately: even in a well-isolated environment, **artifacts created by the agent can be compromised** (code, scripts, configs, IaC, containers, documents, etc.). Therefore, everything you take out of the VM should be treated as untrusted and verified (change audits, scanning, reproducible builds, manual review of critical sections).

If you give the agent full authority for real tasks without additional confirmations, there is a risk that everything will be botched in the worst-case scenario.

---

## 2) Intentional Actions by Malicious Actors

This is more dangerous than accidental errors.

### Legal Aspect

You may involuntarily become both a victim of a crime and an unwitting accomplice. Everything done on the network from your machine or from a server purchased in your name legally appears as your actions — making the risks of "complicity" no less serious than the risks of being a "victim."

### Typical Attack Vectors

- Backdoors in modules/plugins from the author (who may be a malicious actor) or modules that have been compromised.
- Prompt injection during web browsing by the agent: a malicious instruction that forces the agent to perform a dangerous action.

### Why Prompt Injection Works

In current LLMs, there is no reliable separation between context and commands/data. When the agent feeds website content to the model, the subsequent output — which the agent interprets as an action plan — can be dictated by instructions hidden in the page content.

It is especially dangerous that even "trusted" sites with UGC (where third-party users can add content) can contain such instructions, because it is just text.

Prompt injection techniques include:

- hidden text on a page (white text on white background, `display:none`, HTML comments), invisible to humans but read by the agent;
- instructions split across different parts of a page (or even across different sites), which only combine into a single command within the agent's context;
- "poisoning" popular resources (Stack Overflow, GitHub issues, forums) — an attacker posts an answer with a hidden instruction that the agent finds while searching for a solution.

### Why Defense Is Hard

Countermeasures typically lag behind attack tools:

- a malicious prompt can be well hidden;
- spread across different parts of a site or across multiple sites;
- the attack can be multi-step, where each step appears safe to LLM filters.

In fresh, hyped tools like OpenClawn, even primitive attacks can work.

### Potential Consequences

In practice, you should assume that an attacker can gain effective access to everything the agent has access to.

Even if the agent "only collects data from the web," this too can be used against the user:

- an attacker can force your agent (for whose actions you are legally responsible) to perform harmful actions on the network;
- restricting to GET requests only does not guarantee safety: not all content on the web is legal to even retrieve, which can be used for blackmail;
- the attack may target not the agent's host, but rather making it produce a compromised product — for which you are also responsible (since legally you are the product's author).

---

## Recommendations

- Don't fall for the hype — do not use such agents for production tasks with real data, credentials, and consequences until the risks become manageable.
- For research and educational purposes, treat them as potentially malicious software:
  - in a non-personalized virtual machine;
  - with constant monitoring and analysis;
  - with restricted actions and traffic;
  - with detailed analysis of artifacts created by the agent.
