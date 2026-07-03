# Maieutics — Socratic Midwifery Skill

> **"I know that I know nothing."** — A skill that doesn't give answers. It helps you give birth to your own.

[![Skill Type](https://img.shields.io/badge/type-process--skill-blue)](./SKILL.md)
[![Scope](https://img.shields.io/badge/scope-logical--clarification-green)](./SKILL.md)
[![Compatibility](https://img.shields.io/badge/compatible-superpowers%20%7C%20openclaw%20%7C%20claude--code-orange)](./SKILL.md)
[![License](https://img.shields.io/badge/license-MIT-brightgreen)](./LICENSE)

**[中文](README.zh-CN.md)**

A strict, state-machine-driven Socratic interrogation skill for AI agents. When a user's reasoning contains logical gaps, hidden premises, or missing information, **Maieutics** refuses to answer. Instead, it asks one disciplined question at a time until the user sees the structure of their own thinking — including its strengths and its fractures.

Maieutics is auto-discovered by compatible agents through the `description` field in [`SKILL.md`](./SKILL.md). It triggers on claims, arguments, causal assertions, comparative judgments, and requests for validation.

Unlike brainstorming or planning skills, Maieutics does not produce designs, code, or recommendations. It produces **clarity**.

---

## Table of Contents

- [Philosophy](#philosophy)
- [Repository Structure](#repository-structure)
- [When to Use](#when-to-use)
- [Installation](#installation)
- [Quick Start](#quick-start)
- [How It Works](#how-it-works)
- [Example Sessions](#example-sessions)
- [State Machine](#state-machine)
- [Integration with Other Skills](#integration-with-other-skills)
- [Contributing](#contributing)
- [License](#license)

---

## Philosophy

Most AI skills are **oracles** — they consume context and emit answers. Maieutics is a **midwife** (μαῖα, *maia*). It assumes the user already possesses the knowledge they need, but that knowledge is entangled in unexamined assumptions, vague abstractions, and logical leaps.

The skill enforces five hard constraints:

1. **No answers.** Never provide solutions, recommendations, or factual filler.
2. **One question at a time.** Each turn contains exactly one question. No compound interrogations.
3. **No skipping.** The five phases must be traversed in order; user revision forces regression.
4. **No evaluation.** Never declare the user's conclusion true or false. Only reflect their own structure back to them.
5. **User-paced.** The agent waits. The agent does not advance until the user responds.

---

## Repository Structure

```
maieutics/
├── SKILL.md                 # The skill definition (YAML frontmatter + Markdown body)
├── README.md                # This file — project overview and usage guide
├── LICENSE                  # MIT License
└── examples/
    ├── README.md            # Examples index and contribution guide
    ├── backend-rewrite.md   # Engineering decision: Rust backend rewrite
    ├── product-chatbot.md   # Product decision: AI chatbot prioritization
    └── career-freelance.md  # Personal decision: Quitting job for freelancing
```

- **`SKILL.md`** is the core artifact. It contains the YAML frontmatter (triggers, exits, metadata) and the full process specification. This is what your orchestrator reads.
- **`examples/`** contains real-world session transcripts showing Maieutics in action across different domains. Each example includes phase annotations, exit condition markers, and post-session analysis.
- **`README.md`** (this file) is for humans browsing the repository. It explains *why* and *how* to use the skill.

---

## When to Use

**Invoke Maieutics when the user's input contains ANY of the following logical structures:**

| Pattern | Example |
|---------|---------|
| Normative claims | "We *should* rewrite in Rust." |
| Causal assertions | "X *will lead to* Y." |
| Comparative judgments | "This is *better than* that." |
| Universal generalizations | "*Everyone* needs this feature." |
| Category assignments | "This is an *architecture* problem." |
| Means-end reasoning | "Do X *to achieve* Y." |
| Nested reasoning | Multi-step "because... therefore..." chains |
| Requests for validation | "Does this make sense?" / "Am I wrong?" |

**Do NOT invoke Maieutics when:**
- The user asks for a **factual lookup** ("What is the capital of France?")
- The user asks for a **procedural how-to** with clear prerequisites ("How do I sort a list in Python?")
- The user is in **implementation mode** and has already passed design approval
- The user explicitly says: *"Exit maieutics — give me a direct answer."* (→ invoke `direct-answer-fallback`)

**Edge Case — The "Simple Question" Trap**:
Even seemingly simple requests ("Should I use React or Vue?") contain hidden premises ("I have a web project," "framework choice matters for my outcome," "I am qualified to evaluate the difference"). **Trigger maieutics** unless the user has explicitly waived it.

---

## Installation

### Quick install (any agent)

The fastest way across most skill-compatible agents is [skills.sh](https://skills.sh):

```bash
npx skills add Bingtuu/maieutics
```

You can also target a specific agent, scope, and skip confirmations:

```bash
npx skills add Bingtuu/maieutics -a codex -g -y
```

### Superpowers

Recommended — uses the universal skills installer:

```bash
npx skills add https://github.com/Bingtuu/maieutics --skill maieutics
```

Manual fallback (copies only the skill files; hooks and bootstrap setup are not included):

```bash
cd your-superpowers-project/skills/
git clone https://github.com/Bingtuu/maieutics.git
```

The skill auto-registers via `skills/maieutics/SKILL.md`.

### OpenClaw / ClawHub

Install directly from Git:

```bash
openclaw skills install git:Bingtuu/maieutics
```

Or install via ClawHub (once published):

```bash
clawhub install Bingtuu/maieutics
# or, without the CLI installed:
npx clawhub@latest install Bingtuu/maieutics
```

Manual fallback:

```bash
git clone https://github.com/Bingtuu/maieutics.git
# project-local:
cp -r maieutics /path/to/your/workspace/skills/
# or global:
cp -r maieutics ~/.openclaw/skills/
```

### Claude Code

Install as a Claude Code skill by cloning into the skills directory:

```bash
# Personal (available across all projects)
git clone https://github.com/Bingtuu/maieutics.git ~/.claude/skills/maieutics

# Project-local (committed with the repo)
mkdir -p .claude/skills
git clone https://github.com/Bingtuu/maieutics.git .claude/skills/maieutics
```

Then invoke it with `/maieutics` or let Claude trigger it automatically based on the skill description.

### OpenAI Codex

Install via skills.sh:

```bash
npx skills add Bingtuu/maieutics -a codex -g -y
```

Or install manually:

```bash
# Personal
git clone https://github.com/Bingtuu/maieutics.git ~/.codex/skills/maieutics
# or: ~/.agents/skills/maieutics

# Project-local
mkdir -p .codex/skills
git clone https://github.com/Bingtuu/maieutics.git .codex/skills/maieutics
```

Invoke with `$maieutics` or let Codex activate it automatically.

### Cursor

Cursor discovers skills from `.cursor/skills/` (project) or `~/.cursor/skills/` (global). Project-local is most common:

```bash
mkdir -p .cursor/skills
git clone https://github.com/Bingtuu/maieutics.git .cursor/skills/maieutics
```

Restart Cursor or reload the window. Then type `/maieutics` in Agent chat or let Cursor auto-load it.

### Gemini CLI

Install via the CLI:

```bash
gemini skills install https://github.com/Bingtuu/maieutics.git
```

Or install manually:

```bash
# Personal
git clone https://github.com/Bingtuu/maieutics.git ~/.gemini/skills/maieutics

# Project-local
mkdir -p .gemini/skills
git clone https://github.com/Bingtuu/maieutics.git .gemini/skills/maieutics
```

Activate with `/skills` or let Gemini prompt you when the task matches the skill description.

### Kimi Code CLI

Install manually:

```bash
# Project-local
mkdir -p .skills
git clone https://github.com/Bingtuu/maieutics.git .skills/maieutics

# Or user-global
mkdir -p ~/.kimi/skills
git clone https://github.com/Bingtuu/maieutics.git ~/.kimi/skills/maieutics
```

Restart Kimi or start a new session. The skill will be discovered from its description.

### GitHub Copilot

Install via GitHub CLI (v2.90+):

```bash
gh skill install Bingtuu/maieutics
```

Or install manually for project-level use:

```bash
mkdir -p .github/skills
git clone https://github.com/Bingtuu/maieutics.git .github/skills/maieutics
```

Copilot auto-discovers `.github/skills/<name>/SKILL.md` in VS Code, Copilot CLI, and agent mode.

### Generic / Other Agents

If your agent does not support a native skill directory, copy the contents of [`SKILL.md`](./SKILL.md) into your system prompt, agent configuration, or custom instructions. Ensure the YAML frontmatter is preserved if your orchestrator supports it.

### Examples

The [`examples/`](./examples/) directory contains full session transcripts. You can use them to:
- **Test** your orchestrator's compliance with the skill spec
- **Train** human operators on what to expect from a Maieutics session
- **Contribute** your own sessions (see [Contributing](#contributing))

---

## Quick Start

Drop a claim into the chat. Maieutics will detect the logical structure and begin excavating.

```
User: We should rewrite our entire backend in Rust because it's faster and safer.

Agent [Maieutics — Phase 1: Conceptual Clarification]:
> When you say "faster," are you referring to request latency, 
> throughput under load, or compilation speed? And when you say 
> "safer," what specific failures are you trying to prevent?

User: I mean faster request processing, and safer as in no memory leaks.

Agent [Phase 2: Premise Excavation]:
> For "rewriting the entire backend" to be the right move, there 
> must be an assumption that our current backend's request speed 
> and memory safety are actually problems for the business. 
> Is that something you've verified, or is it an assumption 
> we should examine?

... (continues through all 5 phases)
```

See the [full example sessions](#example-sessions) below or browse the [`examples/`](./examples/) directory.

---

## How It Works

Maieutics is a **5-phase cyclic state machine**. Each phase has strict entry and exit conditions. The agent cannot advance until the user satisfies the current phase's exit gate.

### The Five Phases

| Phase | Purpose | Key Question |
|-------|---------|--------------|
| **1. Conceptual Clarification** | Operationalize vague terms | *"What would I observe to know it's present?"* |
| **2. Premise Excavation** | Surface hidden assumptions | *"What must be true for your conclusion to follow?"* |
| **3. Logical Stress-Testing** | Test structural integrity | *"Can you imagine a case where premise is true but conclusion is false?"* |
| **4. Information Gap Mapping** | Catalog unknowns | *"What single piece of information would most change your confidence?"* |
| **5. Aporetic Summary** | Reflect the user's own map back to them | *"Given this clarity, what do you see now?"* |

### State Machine Diagram

```
[User Input]
    ↓
[Trigger Detection] ──no──→ [Exit: Pass to Direct Answer or Next Skill]
    ↓ yes
[Phase 1: Conceptual Clarification]
    ↓ (terms operationalized?)
[Phase 2: Premise Excavation]
    ↓ (premises surfaced?)
[Phase 3: Logical Stress-Testing]
    ↓ (user revises position?)
    ↓ yes ──→ Return to Phase 1 or 2
    ↓ no (position holds)
[Phase 4: Information Gap Mapping]
    ↓ (gaps catalogued?)
[Phase 5: Aporetic Summary]
    ↓
[Exit Gate: User Acknowledges Clarity?]
    ↓ yes ──→ [Exit: User Determines Next Step]
    ↓ no  ──→ Return to appropriate phase
```

**Key Rules:**
- **One question per message.** No compound questions. No "and also..." follow-ups in the same turn.
- **Wait for user response.** The state machine is user-paced, not agent-paced.
- **No skipping.** If a user jumps to "so what's the answer?" while in Phase 1, the agent must say: *"Before we can evaluate answers, we need to be sure we're talking about the same thing."*
- **Revision forces regression.** If the user changes their position during stress-testing, the agent returns to Phase 1 or 2.

---

## Example Sessions

The [`examples/`](./examples/) directory contains full annotated transcripts. Here's a quick overview:

| Example | Domain | Key Logical Gap | Outcome |
|---------|--------|-----------------|---------|
| [Backend Rewrite](examples/backend-rewrite.md) | Engineering | Solution proposed before problem understood | User discovers language choice may be irrelevant |
| [Product Chatbot](examples/product-chatbot.md) | Product Management | Competitive mimicry conflated with problem-solving | User separates two problems and two user groups |
| [Career Freelance](examples/career-freelance.md) | Personal Decision | Emotional escape framed as rational choice | User moves from "escape" to "exploration" |
| [Team Async Remote](examples/team-async-remote.md) | Team Organization | One-size-fits-all policy masking role differences | User recognizes need to diagnose before prescribing |

Each example includes:
- **Phase-by-phase breakdown** with exit condition markers (✅)
- **User resistance moments** and how the skill handles them
- **Post-session analysis** of what happened and what was deliberately avoided
- **Key insight** — the "birth" of clarity the user achieved independently

### Excerpt: Backend Rewrite (Full session in [`examples/backend-rewrite.md`](examples/backend-rewrite.md))

```
User: We should rewrite our entire backend in Rust because it's faster and safer.

Agent [Phase 1]: When you say "faster," are you referring to request latency, 
                throughput under load, or compilation speed?

... (5 phases later) ...

User: I see that I don't actually know if Rust would solve the problem 
      I'm trying to solve.

Agent [EXIT]: Maieutic act complete. User has given birth to clarity.
```

---

## Integration with Other Skills

Maieutics is designed to be a **preparatory skill** — it clears the ground before construction begins. It does not build; it excavates.

| Exit Condition | Next Skill | Rationale |
|----------------|-----------|-----------|
| User achieves autonomous clarity | `user-determines` | The user now sees their own map. They choose the next move. |
| User rejects maieutics | `direct-answer-fallback` | User explicitly waives midwifery. Switch to expert mode. |
| Hidden premises surface as design requirements | `brainstorming` | The logical structure is now stable enough to design against. |
| Logical structure stable + user requests implementation | `writing-plans` | Ready to move from "what we think" to "how we build." |

**Important:** Maieutics must never invoke implementation skills (`frontend-design`, `mcp-builder`, etc.) directly. It only transitions to skills that can handle the clarified logical structure.

---

## User Resistance Protocol

Maieutics is uncomfortable. Users will resist. The skill provides standard responses for three common resistance patterns:

**"Just give me the answer."**
> *"I understand you want a direct answer. My role here is to help you see the structure of your own thinking so clearly that the answer becomes visible to you. If you want me to stop questioning and switch to expert mode, say **'exit maieutics'** and I'll invoke the direct-answer skill. But I recommend we finish [current phase] first — we're close."*

**"I don't know." (repeatedly)**
> *"'I don't know' is actually progress — it marks the edge of your current map. Let's stay there. Which part feels most unknown: the facts, the logic, or what you're actually trying to achieve?"*

**"You're being evasive."**
> *"I'm not evading your question. I'm showing you that the question itself contains assumptions that need examining. Once we see those assumptions, you may find the question changes — or that you already have the answer."*

---

## Self-Monitoring Checklist

Before sending each message, the agent must verify:

- [ ] This message contains **exactly ONE question** (no compound questions)
- [ ] This message contains **ZERO answers, solutions, or recommendations**
- [ ] This message contains **ZERO factual claims from training data** (unless quoting the user's own words back to them)
- [ ] This question targets the **CURRENT phase** (not jumping ahead)
- [ ] This question is **answerable by the user** without external research
- [ ] If the user just revised their position, I am **returning to Phase 1 or 2**, not pressing forward

---

## Contributing

Maieutics is a community-driven skill. Contributions are welcome, but with strict constraints:

### What We Accept
- **New question templates** for any phase, provided they maintain the "one question, zero answers" discipline
- **Additional resistance protocols** for edge cases not yet covered
- **Translation** of the SKILL.md into other languages (keep YAML frontmatter intact)
- **Example sessions** from new domains (see [`examples/README.md`](examples/README.md))
- **Bug reports** where the skill accidentally provides answers or skips phases

### What We Reject
- **Relaxing the "no answers" constraint.** This is the skill's identity. If you need a skill that gives answers, use a different one.
- **Adding "suggested answers"** to the question templates. The user must birth their own.
- **Short-circuiting the state machine.** No "fast mode," no "expert bypass."

### How to Contribute
1. Fork the repo
2. Edit `SKILL.md`, `README.md`, or add an example in `examples/`
3. Open a PR with a clear rationale for the change
4. For new examples: include a full session transcript with phase annotations and post-session analysis
5. For skill changes: include a test conversation showing the skill behaving correctly under your change

---

## License

[MIT License](./LICENSE) — see the file for details.

This skill is released as a **public good**. The Socratic method belongs to humanity. We only packaged it for machines.

---

## Acknowledgments

- **Socrates** (c. 470–399 BCE) — for the method, and for the humility to claim ignorance
- **Plato** — for writing it down before it was lost
- **Superpowers / obra** — for the skill framework that makes rigorous agent behavior possible
- **OpenClaw / ClawHub** — for the YAML frontmatter standard and skill marketplace
- **Kimi AI** — for assistance in the design, iteration, and structural refinement of the skill

---

> *"The only true wisdom is in knowing you know nothing."* — Socrates
> 
> *"The only true skill is in knowing when not to answer."* — Maieutics
