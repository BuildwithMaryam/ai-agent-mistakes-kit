# Mistake 6: Not turning failures into measurable evaluations

Testing before launch isn't enough. Evaluations should be part of your agent's whole life.

If your agent completes 90% of conversations, is that good? Maybe. But what happened in the other 10%? Did it misunderstand the question, use the wrong tool, or make something up? If you only track completion rates, you can't tell. A formatting glitch is not the same as leaking customer information.

Two ideas to keep apart:
- **Observability:** seeing what your agent does: the steps it takes, the tools it calls, and where things go wrong.
- **Evaluations:** measuring whether it behaves correctly.

Your agent can also get worse after you've made it better. A model update can change its behavior. A small instruction change can fix one problem and cause three others. Real customer behavior can shift over time.

## What to do
- Log agent interactions and tool calls.
- Track different types of failures separately, and rank them by how much they matter.
- Set alerts for critical issues like data leaks.
- Regularly read real conversations.
- Rerun your evaluation suite every time you change the model, the instructions, or the tools.
- Keep monitoring after launch. Reliability isn't a one-time achievement.

## Prompt to paste into your coding assistant

```text
Help me turn failures into repeatable checks.

1. Read failure-log.csv. For each failure, write a yes/no check that would catch it (for example "Did the agent promise a refund the policy doesn't allow?"). Prefer checks I can run in code. Where only a person can judge, mark it "needs human review".
2. Add a severity to each failure type. Anything that exposes private data or takes an unauthorized action is critical.
3. Add every failure as a new row in test-scenarios.csv so it's rerun from now on.
4. Write a short script that reruns all scenarios and prints passed and failed counts per category, so I can compare before and after any change to the model, instructions, or tools.
5. Suggest what the agent should log (steps, tool calls, failure type) and which alerts matter, starting with critical ones. Don't set up anything that sends data to a third-party service without asking me.

Tell me what the checks can't tell us, and what you couldn't test.
```

## Failure log
Use [`templates/failure-log.csv`](../templates/failure-log.csv). One row per failure: what happened, what type it was, how bad it was, and which check now catches it.

## Check your result
- If a model or instruction change makes things worse, will you find out before your users do?
- Can you say what the failures were, not just how many?
- Does every critical failure have a check, an alert, or both?
