# Example Session: Team Work-Mode Decision

> **Context**: A team lead wants to switch the entire team to async-first remote work.  
> **Skill**: Maieutics v2.0  
> **Outcome**: The user discovers that "async remote" is a solution label hiding several unexamined problems and constraints.

---

## Phase 1: Conceptual Clarification

**User**: We should move the whole team to async-first remote work. It will make us more productive and people will be happier.

**Agent**: When you say "async-first remote work," what does that look like day-to-day? Are you talking about no fixed working hours, no synchronous meetings, or both? And when you say "more productive," what kind of productivity do you mean — more output per person, faster project completion, fewer interruptions, or something else?

**User**: I mean no required meetings and no required working hours. People work when they're most productive. By productivity I mean fewer interruptions and more deep-work time.

> ✅ *Exit condition met*: "Async-first remote" = no required meetings + no required hours; "productive" = fewer interruptions + more deep-work time.

---

## Phase 2: Premise Excavation

**Agent**: For "switching the whole team to async-first" to be the right move, there must be an assumption that the team's current pain is caused by synchronous work itself, not by something else — too many meetings, poor documentation, unclear ownership, or the specific tools you use. Is that an assumption you've tested?

**User**: I haven't really tested it. People just complain about meetings and not having focused time.

**Agent**: There's another hidden premise: that everyone on the team has the same kind of work that benefits from deep, uninterrupted time. Some roles, like onboarding new hires or coordinating with external partners, might require synchronous presence. Are you assuming async works for everyone, or have you looked at the different roles?

**User**: I guess I was thinking mostly about the engineers. I didn't think about support, sales, or the new people we're hiring.

> ✅ *Exit condition met*: Two hidden premises surfaced — (1) current pain is caused by synchronicity itself [untested], (2) async-first fits all roles equally [unexamined].

---

## Phase 3: Logical Stress-Testing

### Counterexample Probe

**Agent**: Can you imagine a scenario where you switch to async-first perfectly — no required meetings, flexible hours — but the team actually produces less valuable work or ships slower?

**User**: Hmm. If decisions that used to take a 15-minute meeting now take two days of threaded comments, then yes, we could ship slower even though everyone has more focused time.

### Boundary Probe

**Agent**: So the value of async might depend on the type of decision. At what point does a discussion become too complex or urgent to handle asynchronously? And which decisions in your team currently cross that boundary most often?

**User**: I think architectural decisions and urgent customer escalations probably can't be fully async. And onboarding new people definitely needs real-time interaction. I hadn't separated these out.

> ✅ *Exit condition met*: User acknowledged logical tension — async benefits some work types but may harm decision speed and onboarding quality.

---

## Phase 4: Information Gap Mapping

**Agent**: You've identified a few places where async might not fit. What don't you know yet that would change how strongly you hold this proposal?

**User**: I don't know how much of people's time is actually consumed by meetings versus other interruptions. I don't know which meetings are truly necessary. I don't know how the non-engineers would be affected. And I don't know whether our documentation culture is strong enough to support async.

**Agent**: Of these gaps, which ones are closable with data, which are guesses you could make, and which are inherent to the choice?

**User**: The time-in-meetings data is closable — we have calendars. Which meetings are necessary is partly a guess, but we could survey the team. How non-engineers are affected is closable by asking them. Whether our documentation culture is strong enough... that's harder. I think it's an inherent uncertainty we'd have to grow into.

> ✅ *Exit condition met*: Gaps catalogued and classified — 2 closable with data, 1 closable with team input, 1 inherent uncertainty.

---

## Phase 5: Aporetic Summary

**Agent**: Here's the map of your reasoning as it stands:

**Conclusion**: Move the whole team to async-first remote work.

**Premises**:
1. The team needs more deep-work time and fewer interruptions.
2. Async-first remote work will provide that.
3. The change will make people happier.

**Hidden Premises Surfaced**:
- The current pain is caused by synchronicity itself, not by meeting hygiene, ownership clarity, or tooling.
- Async-first fits all roles equally.

**Logical Tension**:
- Async may increase deep-work time but slow down decisions that currently rely on quick synchronous alignment.
- Some roles and activities (onboarding, customer escalations, cross-functional coordination) may not fit the async model.

**Information Gaps**:

| Gap | Classification |
|-----|---------------|
| How much time is lost to meetings vs. other interruptions | Closable — calendar analysis |
| Which meetings are truly necessary | Closable — team survey |
| Impact on non-engineering roles | Closable — role-by-role inquiry |
| Whether documentation culture can support async | Inherent — must grow into it |

**What you now know that you didn't know before**:
- "Async remote" is not a single uniform policy; it interacts differently with different roles and decision types.
- Your original framing treated a solution as if it were the only possible response to a vaguely defined problem.

**Agent**: Given this clarity — including its strengths and its fractures — what do you see now that you didn't see before?

**User**: I see that I was proposing a solution before I understood what problem I was solving, and I was ignoring half the team. I need to diagnose the actual time sinks and role constraints before I can decide what to change.

> ✅ *Exit condition met*: User achieved autonomous clarity. Maieutic act complete.

---

## Post-Session Notes

**What happened**:
- The user entered with a confident policy proposal ("move the whole team to async-first remote").
- Through 5 phases of questioning, they discovered that "async remote" was a label hiding multiple unexamined assumptions about cause, role fit, and decision speed.
- They independently concluded that the proposal was premature and that they needed to diagnose before prescribing.

**What did NOT happen**:
- The agent never told the user that async remote work is bad or wrong.
- The agent never proposed a hybrid model or specific meeting policy.
- The agent never provided facts about remote-work research or best practices.
- The agent never filled in the information gaps with its own knowledge.

**Next steps (user-determined)**:
- The user could invoke `brainstorming` to design a team time-use investigation or a hybrid work-policy experiment.
- The user could invoke `direct-answer-fallback` to ask "What are common async-first meeting policies?"
- The user could continue maieutics on a narrower branch (e.g., "What makes a meeting necessary vs. replaceable?").

**Key insight**: The user gave birth to their own clarity. The agent only asked questions.
