# PromptMaster

A Claude Code skill that turns Claude into a prompt engineering orchestrator. When you invoke `/prompt-master`, it discovers every agent available in your session, selects the right ones for your task, and delegates the work to them — it never writes the final output itself.

Works with any agent setup. Each person on the team can have different agents installed and the skill adapts to whatever is available.

---

## Installation

**Step 1 — Add the marketplace**

```bash
claude plugin marketplace add BurhanPasha/prompt-master
```

**Step 2 — Install the skill**

```bash
claude plugin install prompt-master
```

That's it. No restart needed.

---

## Usage

In any Claude Code session, type:

```
/prompt-master <your task or request>
```

**Examples:**

```
/prompt-master write a system prompt for a customer support agent that handles refund requests

/prompt-master improve this prompt: "You are a helpful assistant. Answer questions about our product."

/prompt-master I need a prompt for an agent that reads invoices and extracts line items into JSON

/prompt-master build me a LinkedIn post about our new AI feature launch
```

You can also invoke it without arguments and describe your task after:

```
/prompt-master
```

---

## How it works

When you invoke the skill, PromptMaster runs four steps:

1. **Discovers agents** — reads the Agent tool definition to find every available `subagent_type` in your session. Outputs the full roster so you can see exactly what it's working with.

2. **Selects agents** — reads your request and picks agents from the discovered roster whose descriptions best match what needs to be done. States its selection and reasoning before invoking anything.

3. **Delegates** — calls each selected agent via the Agent tool with a precise brief (goal, task, context, output format). Runs independent agents in parallel, dependent agents sequentially.

4. **Synthesizes** — combines all agent outputs into one clean deliverable.

PromptMaster never writes the final artifact itself before agents have run. It never invents or assumes an agent exists — only agents confirmed in the discovery step are used.

---

## Updating

```bash
claude plugin update prompt-master
```

## Uninstalling

```bash
claude plugin uninstall prompt-master
claude plugin marketplace remove prompt-master
```

---

Built by [Silverthread Labs](https://silverthreadlabs.com)
