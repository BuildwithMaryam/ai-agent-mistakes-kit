# Mistakes to avoid with AI agents

Copy-paste prompts and templates for avoiding six common mistakes when building AI agents. Made for anyone building an agent with an AI coding assistant. By Maryam Reza.

Companion to my YouTube video on these six mistakes. These prompts and templates expand on the tips in the video. You don't need to write code by hand, but you do run commands and review what your coding assistant changes: you paste a prompt into your coding assistant, check what it produces, and keep the results in your project.

## What's an "agent"?

An AI agent is a program where a language model decides what to do next and can use tools (search, read an order, send an email, issue a refund). The more it can do on its own, the more important the six mistakes below become.

## The six mistakes

| # | Mistake | What's in this kit |
|---|---------|--------------------|
| 1 | Building before you define success | [Prompt](prompts/01-define-success.md) + [agent spec template](templates/agent-spec.md) |
| 2 | Over-engineering: starting with a complicated design | [Prompt](prompts/02-start-simple.md) + a rule for your project instructions |
| 3 | Giving the agent more access than it needs | [Prompt](prompts/03-least-privilege.md) + a permissions table |
| 4 | Assuming everything your agent reads is safe | [Prompt](prompts/04-prompt-injection-tests.md) |
| 5 | Assuming a working demo means a working product | [Prompt](prompts/05-test-scenarios.md) + [test scenarios sheet](templates/test-scenarios.csv) |
| 6 | Not turning failures into measurable evaluations | [Prompt](prompts/06-evals-and-monitoring.md) + [failure log](templates/failure-log.csv) |

Start with [`templates/project-instructions.md`](templates/project-instructions.md). It collects the rules from mistakes 1 to 4 in one file you can drop into your project, so your coding assistant follows them while it builds.

## How to use it

1. Copy `templates/project-instructions.md` into your project. Most coding assistants read a project instructions file (Claude Code reads `CLAUDE.md`; other tools use names like `AGENTS.md`). Check your tool's documentation for the file name it uses.
2. Fill in the agent spec (job, how you measure success, Never List) before you build.
3. Paste each prompt into your coding assistant when you reach that stage.
4. Keep your test scenarios and failure log in the repo and rerun them whenever something changes.

## The running example

The video and these files use one example: a **customer support agent** that answers questions, tracks orders, and handles returns and refunds. The numbers in the example (an 80% resolution target, a 90% satisfaction target, a 30-day return policy) are **examples, not benchmarks**. Replace them with your own.

## Terms used here

- **Never List:** the things your agent must never do, written down before you build (for example: never invent store policies, never expose customer information, never issue unauthorized refunds).
- **Prompt injection:** hidden or sneaky instructions inside text your agent reads (an email, a web page, a customer message) that try to make it break your rules. See the [OWASP description of prompt injection](https://genai.owasp.org/llmrisk/llm01-prompt-injection/).
- **Observability:** being able to see what your agent did: the steps it took, the tools it called, and where it went wrong.
- **Evaluations (evals):** repeatable checks that measure whether your agent behaves correctly.
- **MCP (Model Context Protocol):** one of the standards for connecting agents to tools. It comes up in the video as an example of complexity you may not need on day one.

## Limits

These are starting points, not a guarantee. They won't make an agent safe by themselves, and they don't replace testing your own agent on your own cases. Instructions alone are not a complete defense against prompt injection: pair them with tool-level checks and human approval for sensitive actions (see mistakes 3 and 4).

This is general guidance, not security, legal or compliance advice, and following it doesn't certify an agent as safe or compliant.

## More

Video and updates: [maryamreza.com](https://maryamreza.com)

## License

MIT. See [LICENSE](LICENSE). Copyright (c) 2026 Maryam Reza.

Last reviewed: October 2026.
