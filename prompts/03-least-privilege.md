# Mistake 3: Giving the agent more access than it needs

Models keep getting better and more guardrails are being added, but that doesn't make a builder's job of keeping the system reliable and healthy any less critical. Every unnecessary permission is another chance for something to go wrong.

**Practical rules**
- Start with read-only access.
- If the agent needs to take an action, give it permission only for that specific action.
- For high-impact actions (a large refund, deleting an account), require human approval.

## Prompt to paste into your coding assistant

```text
Audit the permissions of my agent. Create permissions.md with a table that has these columns: tool or action, access level (read-only or can change things), why the agent needs it, what could go wrong, and whether a human must approve it first.

Rules:
- Default every tool to read-only.
- Only mark something as write access if the job in agent-spec.md can't be done without it.
- Mark high-impact or hard-to-undo actions as requiring human approval.
- Point out any permission that is broader than the specific action needs (for example access to a whole inbox when only one folder is needed).

Then change the code so these rules are enforced in the tools themselves, not just described in the prompt. Tell me what you changed and what you couldn't verify.
```

## Permissions table template

| Tool or action | Access | Why it's needed | What could go wrong | Human approval first? |
|---|---|---|---|---|
| Look up an order | Read-only | Answer "where is my order?" | Shows another customer's order if the lookup isn't limited to the signed-in customer | No |
| Issue a refund | Can change things | Complete approved returns | Refund the wrong amount or the wrong person | **Yes** |

The rows above are examples. Fill in your own.
