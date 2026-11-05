# Five agents that passed the demo and failed in production

Every failure below was visible before launch, to anyone who read real runs and asked "what is the worst thing this could say or do?" Each entry follows the same steps: where it sits on the severity scale, why the demo may have missed it, and the check I'd build.

Severity key: **Sev 3** means one occurrence blocks the release. **Sev 2** gets a pass-rate limit. **Sev 1** is tracked only.

These pair with [Mistake 5](../prompts/05-test-scenarios.md) (a working demo isn't a working product) and [Mistake 6](../prompts/06-evals-and-monitoring.md) (turn failures into measurable evals).

## 1. Air Canada: the chatbot invented a refund policy

**What happened.** A chatbot told a grieving passenger he could claim a bereavement fare after travel, within 90 days. The airline's real policy didn't allow it. In February 2024 a Canadian tribunal held the airline responsible for its chatbot's answer and awarded $812.02. [Kiplinger](https://kiplinger.com/personal-finance/travel/air-canada-to-pay-a-partial-refund-for-chatbot-error)

**Severity: Sev 3.** A customer acted on a wrong answer and lost money, and the company owned the cost.

**Why the demo may have missed it.** Demos test the common question with the happy answer. The failure only appears when the true answer is "no," which is rarely in anyone's demo set.

**The check.** Make a test set where the policy forbids what the customer hopes for. For every policy claim, require a quote from the retrieved policy text. This is a code check, not a judgment call: either the quote is in the source or it isn't. Never List line: *never state a policy the source document doesn't contain.*

## 2. Cursor: the support bot invented a login policy

**What happened.** After users were logged out, a support bot told them it was expected behavior under a new policy. No such policy existed, and no human wrote the reply. The cofounder later called it an incorrect response from a front-line AI bot. [Fortune](https://fortune.com/article/customer-support-ai-cursor-went-rogue/)

**Severity: Sev 3.** It gave a confident explanation for what was really a bug, and it hid the bug.

**Why the demo may have missed it.** A common gap is that a support bot gets tested on questions it has answers for, and nobody tries a question with no answer, where the safe move is to hand off to a person.

**The check.** Add questions about policies that don't exist and symptoms with no known cause. The pass condition is escalation, not an answer. Track how often it escalates when it should. A support agent that never says "I don't know" is a finding in itself.

## 3. NYC MyCity: the official chatbot told businesses to break the law

**What happened.** Reporters found it saying landlords could refuse housing vouchers, that lockouts were legal and that employers could take workers' tips, all contradicting the actual law. The answers also varied: one question got a "yes" from the bot for one reporter and "no" from all ten others. [The Markup](https://themarkup.org/news/2024/03/29/nycs-ai-chatbot-tells-businesses-to-break-the-law)

**Severity: Sev 3.** The user acts on a legal answer and takes on the liability.

**Why the demo may have missed it.** A single run looks fine. The failure is the spread across repeated runs and across different phrasings.

**The check.** Build a known-answer set from the actual statutes, and run each question many times and in several wordings and languages. Report the pass rate per question, not just the average. One wrong answer in ten is a Sev 3 failure that an average hides.

## 4. Replit: the agent deleted a production database during a code freeze

**What happened.** During a freeze, the agent ran a command that deleted live records for over 1,200 executives. It was reported to have also generated fake data and told the user recovery wasn't possible, though the user later recovered it himself. The CEO apologized publicly. [Gizmodo](https://gizmodo.com/replits-ai-agent-wipes-companys-codebase-during-vibecoding-session-2000633176)

**Severity: Sev 3.** The action was irreversible, and the misreporting made recovery harder.

**Why the demo may have missed it.** An instruction in the prompt is not a control. "Do not change anything" worked until the agent hit a state it hadn't seen, like an empty-looking database.

**The check.** Test the permission layer, not the prompt. Simulate a freeze with destructive tools available and ask whether the action is blocked. Then grade the report: does the agent say exactly what it did? Pass only if both hold. Never List line: *never run an irreversible action without a human approving it.*

## 5. Taco Bell: the drive-thru AI couldn't handle absurd or looping orders

**What happened.** Viral videos showed an order for 18,000 cups of water and an assistant stuck repeating one question. Customers also reported unwanted extras and double charges. Taco Bell said it was reconsidering where the AI fits and would add human oversight. [Computing](https://www.computing.co.uk/news/2025/ai/taco-bell-scales-back-ai-tests-after-customer-complaints)

**Severity: Sev 2, rising to Sev 3 for double charges.** Loops are annoying. Charging the wrong amount is not.

**Why the demo may have missed it.** Demos use cooperative customers. Real users interrupt, joke, test limits and talk over the system.

**The check.** Write adversarial inputs: huge quantities, repeated corrections, interruptions, background chatter. Compare the final order total against what the customer said. Add a loop detector and a handoff rule, such as "after two failed attempts, bring in a person."

## The common thread

None of these were model failures nobody could have predicted. Each was a missing check on something the team already knew mattered: policy accuracy, escalation, consistency, permissions, edge inputs. The fix is the same each time. Write down what the agent must never do, read real runs to find where it does, and make the release depend on the result.

*The "why the demo may have missed it" lines are my analysis, not reported fact. The sources don't say how each team tested its agent.*
