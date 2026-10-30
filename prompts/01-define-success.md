# Mistake 1: Building before you define success

It's tempting to start prompting and coding. A little time up front on three questions changes a lot:

1. What is the expected job of your agent?
2. How will you measure success?
3. What should it never do? (your Never List)

You don't need a perfect list on the first try.

## Prompt to paste into your coding assistant

```text
I'm about to build an AI agent. Before writing any code, help me write a one-page spec in agent-spec.md with three sections:

1. The job: what the agent is expected to do, and for whom.
2. How we'll measure success: measures I can actually check, including at least one about quality and not only volume.
3. The Never List: things the agent must never do, written as plain sentences.

Ask me up to five questions first, one at a time, about who uses the agent, what it can touch, and what a bad outcome would look like. Then draft the spec. Don't invent numbers: where I haven't given a target, leave a clearly marked blank for me to fill in. Draft the Never List from the bad outcomes I describe, and say which Never List item each one came from.

When we're done, add a short section to my project instructions file that points to agent-spec.md and says: if a change would conflict with the Never List, stop and ask.
```

## Check your result
- Could a stranger tell, from your success measures alone, whether the agent is working?
- Does every Never List item come from a bad outcome you can name?
- Is the spec referenced from your project instructions, so your coding assistant sees it on every task?
