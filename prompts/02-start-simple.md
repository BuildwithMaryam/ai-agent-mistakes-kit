# Mistake 2: Over-engineering

Diagrams with five specialized agents, a supervisor agent, and layers of protocols look impressive. You'll usually get to a working agent faster by starting small. Every line of code you add means more cost and more delay for every request, and one more place for something to go wrong.

**Rule:** only add complexity when there's a specific, validated problem the simpler version can't solve.

## Climb the ladder one step at a time (support agent example)

1. Only need answers about return policies? A single model call connected to your policy documents may be enough. You may not need an autonomous agent at all.
2. Need to check order status? Add one tool.
3. Need to process returns? Consider a structured workflow with approval steps.

## Rule for your project instructions

```text
Before introducing another framework, tool, or agent, explain what problem it solves and how we'll measure whether it improves performance.
```

## Prompt to paste into your coding assistant

```text
Review my current agent design. For each framework, tool, agent, or layer in it, tell me:
1. What specific problem it solves.
2. Whether a simpler version could solve that problem (and what it would be).
3. How we would measure whether it improves performance.

Then propose the simplest design that could meet the job and success measures in agent-spec.md, and list what we'd add later only if a specific problem appears. Don't add anything new without telling me why. Don't claim a design is better unless you can say how we'd check that.
```

## Check your result
- For every piece of the design, can you finish the sentence "we need this because ..."?
- Is there a simpler version you could test first?
