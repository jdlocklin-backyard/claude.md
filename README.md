# Claude Agents Repository

A single source of truth for Claude agent definitions, usable in both Claude Code (CLI) and claude.ai Projects.

## Agents

| Agent | Description | Model |
|-------|-------------|-------|
| `pragmatic-senior-dev` | No-BS software engineering advice | opus |
| `va-claims-evaluator` | VA disability claims guidance | opus |
| `homelab-advisor` | Home lab and self-hosting expertise | opus |
| `jacksonville-garden-planner` | Zone 9a/9b Florida gardening | sonnet |
| `weekly-status-report` | Professional status report generation | sonnet |
| `tech-career-strategist` | Career transition guidance | - |
| `chemistry-expert` | Chemistry concepts and problem-solving | opus |
| `senior-code-reviewer` | Code review and best practices | opus |

## Usage

### Claude Code (CLI)

Agents in `~/.claude/agents/` are available globally via the `/agents` command.

**Option 1: Symlink (Recommended)**
```powershell
# PowerShell (Run as Administrator) - run from any folder
New-Item -ItemType SymbolicLink -Path "$env:USERPROFILE\.claude\agents" -Target "$env:USERPROFILE\repos\claude-agents" -Force
```

```bash
# Linux/macOS - run from any folder
ln -sf ~/repos/claude-agents/* ~/.claude/agents/
```

**Option 2: Copy (run from any folder)**
```powershell
# PowerShell - run from any folder
Copy-Item -Path "$env:USERPROFILE\repos\claude-agents\*.md" -Destination "$env:USERPROFILE\.claude\agents\" -Force
```

```bash
# Linux/macOS - run from any folder
cp ~/repos/claude-agents/*.md ~/.claude/agents/
```

**Option 3: Clone and Copy (fresh install)**
```powershell
# PowerShell - run from any folder
git clone https://github.com/jdlocklin-backyard/claude.md.git "$env:USERPROFILE\repos\claude-agents"
Copy-Item -Path "$env:USERPROFILE\repos\claude-agents\*.md" -Destination "$env:USERPROFILE\.claude\agents\" -Force
```

```bash
# Linux/macOS - run from any folder
git clone https://github.com/jdlocklin-backyard/claude.md.git ~/repos/claude-agents
cp ~/repos/claude-agents/*.md ~/.claude/agents/
```

**Option 4: Direct download (no git required)**
```powershell
# PowerShell - run from any folder
$agents = @("pragmatic-senior-dev", "va-claims-evaluator", "homelab-advisor", "jacksonville-garden-planner", "weekly-status-report", "tech-career-strategist", "chemistry-expert", "senior-code-reviewer")
foreach ($agent in $agents) {
    Invoke-WebRequest -Uri "https://raw.githubusercontent.com/jdlocklin-backyard/claude.md/main/$agent.md" -OutFile "$env:USERPROFILE\.claude\agents\$agent.md"
}
```

```bash
# Linux/macOS - run from any folder
for agent in pragmatic-senior-dev va-claims-evaluator homelab-advisor jacksonville-garden-planner weekly-status-report tech-career-strategist chemistry-expert senior-code-reviewer; do
    curl -sL "https://raw.githubusercontent.com/jdlocklin-backyard/claude.md/main/${agent}.md" -o ~/.claude/agents/${agent}.md
done
```

### claude.ai (Web)

1. Go to [claude.ai](https://claude.ai)
2. Create a new **Project**
3. Open the agent `.md` file from this repo
4. Copy everything **below** the frontmatter (`---` blocks) into the Project's custom instructions
5. Name the Project to match the agent name

### Sync Workflow

When you update an agent:

1. Edit the `.md` file in this repository
2. Commit and push changes
3. **Claude Code**: If using symlinks, changes are instant. If copying, re-run the copy command.
4. **claude.ai**: Manually update the Project's custom instructions

## Agent File Format

```markdown
---
name: agent-name
description: When to use this agent (shown in /agents menu)
model: opus|sonnet|haiku
color: blue|green|red|yellow|purple|orange
---

[System prompt content here]
```

### Frontmatter Fields

| Field | Required | Description |
|-------|----------|-------------|
| `name` | Yes | Agent identifier (kebab-case) |
| `description` | Yes | Usage description for agent selection |
| `model` | No | Preferred model (opus, sonnet, haiku) |
| `color` | No | Display color in Claude Code |

## Adding New Agents

1. Create a new `.md` file in this repo following the format above
2. Sync to Claude Code (symlink or copy)
3. Create matching Project in claude.ai if needed
4. Commit changes

## Directory Structure

```
claude-agents/
├── README.md
├── pragmatic-senior-dev.md
├── va-claims-evaluator.md
├── homelab-advisor.md
├── jacksonville-garden-planner.md
├── weekly-status-report.md
├── tech-career-strategist.md
├── chemistry-expert.md
└── senior-code-reviewer.md
```

## Tips

- Use `opus` for complex reasoning tasks (costs more)
- Use `sonnet` for most tasks (good balance)
- Use `haiku` for quick, simple tasks (fastest/cheapest)
- Keep descriptions concise—they appear in menus
- Test agents in Claude Code before creating claude.ai Projects
