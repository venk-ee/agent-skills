# Agent Skills

A modular collection of behavioral skills and persona switches for AI coding agents (such as Claude Code, Antigravity, and Cursor).

---

## Overview

Instead of one-size-fits-all prompting, **Agent Skills** allows AI coding assistants to switch operational modes dynamically based on user intent.

| Skill | Mode | Trigger Examples | Focus |
| :--- | :--- | :--- | :--- |
| **[`teacher`](.agents/skills/teacher/SKILL.md)** | Socratic TA | `teach me`, `be my teacher`, `help me learn` | Conceptual mastery and guided debugging without spoon-feeding answers. |
| **[`asap`](.agents/skills/asap/SKILL.md)** | Emergency Fixer | `urgent`, `quick fix`, `fix this asap`, `no time` | Fast, production-ready code fixes without unnecessary explanations. |
| **[`brainstorm`](.agents/skills/brainstorm/SKILL.md)** | System Architect | `plan`, `design`, `architecture`, `tradeoffs` | Architectural blueprints, trade-off analysis, and milestone roadmaps. |

---

## Getting Started

### Installation
Copy the `.agents/` folder into your project root or your global agent configuration directory:

```bash
cp -r .agents /path/to/your/project/
```

### Usage
Once placed in your project root, compatible AI coding agents automatically discover the skills in `.agents/skills/` and adapt their behavior when matching trigger words are used.

---

## License

MIT
