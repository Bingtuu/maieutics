# Example Session: Backend Rewrite Decision

> **Context**: A team lead wants to rewrite their entire backend in Rust.  
> **Skill**: Maieutics v2.0  
> **Outcome**: The user discovers they don't actually know if Rust solves their real problem.

---

## Phase 1: Conceptual Clarification

**User**: We should rewrite our entire backend in Rust because it's faster and safer.

**Agent**: When you say "faster," are you referring to request latency, throughput under load, or compilation speed? And when you say "safer," what specific failures are you trying to prevent?

**User**: I mean faster request processing, and safer as in no memory leaks.

> ✅ *Exit condition met*: Terms operationalized — "faster" = request processing speed, "safer" = absence of memory leaks.

---

## Phase 2: Premise Excavation

**Agent**: For "rewriting the entire backend" to be the right move, there must be an assumption that our current backend's request speed and memory safety are actually problems for the business. Is that something you've verified, or is it an assumption we should examine?

**User**: We do have latency complaints, but I'm not sure about memory leaks being a real issue.

> ✅ *Exit condition met*: Hidden premise surfaced — "memory leaks are a real problem for us" is unverified.

---

## Phase 3: Logical Stress-Testing

### Counterexample Probe

**Agent**: If we accept that Rust prevents memory leaks, but our current pain points are latency complaints, what bridge connects "memory safety" to "solving our actual problem"? Could we imagine a scenario where we rewrite in Rust, eliminate memory leaks, but the latency complaints persist?

**User**: Hmm. If the latency is from database queries, the language won't matter.

### Boundary Probe

**Agent**: So the value of Rust depends on where the bottleneck lives. What would you need to know to determine whether our latency is a language-level problem, a database problem, or an architecture problem?

**User**: I guess I'd need to profile the current system.

> ✅ *Exit condition met*: User acknowledged logical tension — language choice may be irrelevant to actual pain point.

---

## Phase 4: Information Gap Mapping

**Agent**: Profiling is one gap. What else don't you know? For example: do you know the cost and risk of rewriting the entire backend? And do you know whether the latency complaints come from a specific subset of endpoints or are system-wide?

**User**: I don't know the rewrite cost, and I haven't looked at which endpoints are slow.

**Agent**: Of the gaps you've identified — root cause of latency, actual incidence of memory leaks, cost/risk of rewrite, distribution of latency across endpoints — which ones are closable with research, and which are inherent uncertainties?

**User**: The profiling and endpoint analysis are closable. The rewrite cost... I could estimate but it would be a guess. Whether memory leaks are actually hurting us — I don't even know how to check that.

> ✅ *Exit condition met*: Gaps catalogued and classified — 2 closable, 1 guess, 1 unknown method.

---

## Phase 5: Aporetic Summary

**Agent**: Here's the map of your reasoning as it stands:

**Conclusion**: Rewrite backend in Rust.

**Premises**:
1. Request speed is a problem → [Verified: latency complaints exist]
2. Memory leaks may be a problem → [Unverified]
3. Rust improves request speed → [Unverified for our specific case]

**Hidden Premise Surfaced**: The rewrite will solve the actual pain point.

**Logical Tension**: Memory safety ≠ latency reduction. The bridge between them is unexamined.

**Information Gaps**:
| Gap | Classification |
|-----|---------------|
| Root cause of latency (language/db/architecture) | Closable — profile |
| Distribution of latency across endpoints | Closable — analyze logs |
| Cost/risk of full rewrite | Educated guess — can estimate |
| Actual incidence of memory leaks | Unknown method — need to research how to detect |

**What you now know that you didn't know before**:
- You don't know if Rust would solve the problem you're trying to solve.
- You don't know if memory leaks are a real problem.
- You don't know where the latency bottleneck lives.

**Agent**: Given this clarity — including its strengths and its fractures — what do you see now that you didn't see before?

**User**: I see that I don't actually know if Rust would solve the problem I'm trying to solve. I jumped to a solution before understanding the problem.

> ✅ *Exit condition met*: User achieved autonomous clarity. Maieutic act complete.

---

## Post-Session Notes

**What happened**:
- The user entered with a confident solution claim ("rewrite in Rust")
- Through 5 phases of questioning, they discovered their reasoning rested on unverified premises and unidentified gaps
- They independently concluded that their original position was premature

**What did NOT happen**:
- The agent never told the user they were wrong
- The agent never suggested an alternative solution
- The agent never provided technical facts about Rust, Go, or any other language
- The agent never filled in the information gaps with its own knowledge

**Next steps (user-determined)**:
- The user could now invoke `brainstorming` to design a latency investigation plan
- The user could invoke `direct-answer-fallback` to ask "How do I profile my backend?"
- The user could continue maieutics on a different branch (e.g., "What does 'safer' mean for our team culture?")

**Key insight**: The user gave birth to their own clarity. The agent only asked questions.
