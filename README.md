# devpost-curriculum

Devpost's plugin marketplace for Claude Code. A collection of agent-powered tools for hackathon participants and organizers.

Currently ships one plugin — more coming soon.

## Plugins

### hackathon-in-a-plugin

A hackathon curriculum that guides you from idea spark to working app in 3–4 hours, delivered as eight agent commands.

**Commands:** `/onboard` → `/scope` → `/prd` → `/spec` → `/checklist` → `/build` → `/iterate` → `/reflect`

#### Install

```
/plugin marketplace add challengepost/devpost-curriculum
/plugin install hackathon-in-a-plugin@devpost-curriculum
```

Then run `/onboard` to start. Requires [Claude Code](https://claude.ai/code).

#### About

A complete hackathon curriculum built as a set of agent skills. Each command produces artifacts that downstream commands consume — scope doc, PRD, technical spec, build checklist, and reflection.

The curriculum teaches spec-driven development: the planning documents aren't busywork, they're the submission itself. The agent acts as a hackathon coach — brisk, sharp, encouraging — interviewing you through each phase.

**Skills:**

| Command | What it does |
|---|---|
| `/onboard` | Welcome, introductions, and learner profile |
| `/scope` | Brainstorm and refine your idea into a focused project scope |
| `/prd` | Turn scope into detailed product requirements |
| `/spec` | Translate PRD into a technical blueprint |
| `/checklist` | Break the spec into a concrete build checklist |
| `/build` | Build the app — autonomous (single run) or step-by-step (one item per session) |
| `/iterate` | Optional polish pass after the build is done |
| `/reflect` | Wrap up with a quiz, qualitative feedback, and reflection |

---

## Other Platforms

The curriculum also works with OpenAI Codex and Cursor.

### OpenAI Codex

Codex uses the same `SKILL.md` format natively. Clone and symlink the skills into your project:

```bash
git clone https://github.com/challengepost/devpost-curriculum.git ~/.devpost-curriculum

# Copy skills into your project
cp -r ~/.devpost-curriculum/plugins/hackathon-in-a-plugin/skills .agents/skills/hackathon
```

Or copy the whole plugin into your home skills directory for global access:

```bash
mkdir -p ~/.agents/skills
cp -r ~/.devpost-curriculum/plugins/hackathon-in-a-plugin/skills/* ~/.agents/skills/
```

The `AGENTS.md` at the plugin root also works as a drop-in — copy it to your project root:

```bash
cp ~/.devpost-curriculum/plugins/hackathon-in-a-plugin/AGENTS.md ./AGENTS.md
```

Then run `/onboard` to start.

### Cursor

Cursor uses `.cursor/rules/*.mdc` files. This repo includes a pre-built adapter:

```bash
git clone https://github.com/challengepost/devpost-curriculum.git ~/.devpost-curriculum

# Copy the Cursor rules into your project
mkdir -p .cursor/rules
cp ~/.devpost-curriculum/cursor-rules/*.mdc .cursor/rules/
```

Then tell the agent: "Let's run /onboard" to start the hackathon curriculum.

---

## License

MIT
