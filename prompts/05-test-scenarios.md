# Mistake 5: Assuming that a working demo means a working product

You ask your agent five questions and it gets all five right. Real customers behave differently.

Example: your support agent explains a 30-day return policy correctly. Then someone asks, "I bought this 45 days ago, but it arrived damaged. Can I still get a refund?" What happens if the agent confidently promises a refund the policy doesn't allow?

A good demo tells you your agent *can* work. It doesn't tell you how often it *will*.

## What to do
1. Start with about 20 test scenarios: simple requests, complicated situations, and edge cases.
2. For each one, write down what a good response looks like.
3. Run your agent, review what went right and wrong, and look for patterns in the mistakes.
4. Improve the agent and rerun the same scenarios.
5. As soon as real customers use it, read real interactions. Every new failure becomes a new scenario.

## Prompt to paste into your coding assistant

```text
Help me build a test set for my agent in test-scenarios.csv (columns: id, category, input, what_good_looks_like, severity, result, notes).

1. Read agent-spec.md. Propose 20 scenarios: simple requests, complicated multi-step situations, edge cases (for example a request that almost fits the policy but doesn't), and a few that test the Never List.
2. For each scenario, write what a good response looks like in a way I can check yes or no. Where the right answer depends on a policy I haven't given you, don't guess: mark it "needs my policy" and ask me.
3. Show me the list and wait for my edits before running anything.
4. After I approve, run the agent on every scenario in a safe test setup, record the result, and group the failures into patterns.

Report counts of passed and failed, list the failures, and say which kinds of cases the scenarios don't cover yet.
```

## Check your result
- Could someone else look at the "what good looks like" column and mark each result pass or fail?
- Does your set include cases where the honest answer is "I can't do that" or "let me get a human"?
- Once real conversations exist, are you adding the failures you find to this file?

See [`templates/test-scenarios.csv`](../templates/test-scenarios.csv) for example rows.
