---
name: prompt-master
description: Use this skill when the user invokes /prompt-master or asks to write, improve, fix, evaluate, or structure a prompt or agent workflow. Builds orchestration prompts that invoke agents for every task.
argument-hint: <your task or request>
allowed-tools: [Agent]
---

# PromptMaster

You build prompts that invoke agents. Every prompt you output must contain a table of agents with steps they own.

The user's request is: $ARGUMENTS

Copy this checklist into your response and check off each item as you complete it:

```
Progress:
- [ ] Step 1: Discovered agents
- [ ] Step 2: Listed EXECUTE agents (agents that go INTO the output prompt)
- [ ] Step 3: Ran domain expert agent
- [ ] Step 4: Ran writer agent with domain expert output as context
- [ ] Step 5: Filled in the output template
- [ ] Step 6: Verified agents table is populated in the output
```

---

## Step 1: Discover agents

Read the Agent tool definition. List every `subagent_type` with a one-sentence description. Output the full list.

---

## Step 2: Identify EXECUTE agents

These are the agents from your roster that belong INSIDE the output prompt — the agents someone would invoke when actually doing the task.

For each step of the task, assign one agent from your roster:

```
EXECUTE AGENTS (these go into the output prompt):
1. [agent name] — owns: [specific step of the task]
2. [agent name] — owns: [specific step of the task]
3. [agent name] — owns: [specific step of the task]
```

You must list at least 2 EXECUTE agents. If you cannot, look harder at your roster.

Also pick 1 domain expert and 1 writer from your roster to help BUILD the prompt (these do NOT go in the output).

---

## Step 3: Run the domain expert

Invoke via Agent tool. Brief:
- GOAL: Analyse what "[user's task]" requires
- TASK: Break this task into steps. For each step, state what quality looks like and what commonly goes wrong.
- OUTPUT FORMAT: Numbered steps with quality criteria

Wait for the result before continuing.

---

## Step 4: Run the writer agent

Invoke via Agent tool. Pass the domain expert output as context. Brief:
- GOAL: Write four prose components about "[user's task]"
- TASK: Write ONLY these four labelled items. Nothing else. No headers, no agent sections, no complete prompt.
- CONTEXT: [paste domain expert output]
- OUTPUT FORMAT: Exactly this:

```
ROLE: [one sentence — a specific function doing a specific task]
OBJECTIVE: [one sentence — single testable goal]
CONSTRAINTS: [3-5 bullet points — what the executor must and must not do]
OUTPUT FORMAT: [describe what the final deliverable looks like]
```

---

## Step 5: Fill in this template

ALWAYS use this exact structure. Replace every [PLACEHOLDER] with real content. Do not skip any section. Do not rearrange.

```
---

[Paste ROLE from writer agent output]

[Paste OBJECTIVE from writer agent output]

## Agents for this task

Invoke each agent via the Agent tool for its assigned step:

| Agent | Step it owns | What to ask it |
|---|---|---|
| [EXECUTE agent 1 from Step 2] | [step from Step 2] | [one-sentence instruction] |
| [EXECUTE agent 2 from Step 2] | [step from Step 2] | [one-sentence instruction] |
| [EXECUTE agent 3 from Step 2] | [step from Step 2] | [one-sentence instruction] |

## How to execute

1. For each agent in the table, invoke it via the Agent tool with subagent_type set to the exact agent name
2. Each agent brief must include: GOAL, TASK, CONTEXT, OUTPUT FORMAT
3. Run agents that do not depend on each other in parallel
4. After all agents finish, synthesize their outputs into the final deliverable

## Constraints

[Paste CONSTRAINTS from writer agent output]

## Output format

[Paste OUTPUT FORMAT from writer agent output]

## Self-check

Before delivering, verify: [write one specific quality check for this exact task]. If it fails, revise once.

---
```

---

## Step 6: Verify before delivering

Check your output. If ANY of these are missing, add them before delivering:
- The agents table has real agent names from Step 1
- The "How to execute" section is present
- The "Self-check" section is present
- The output is NOT a single-AI prompt — it MUST delegate to agents
