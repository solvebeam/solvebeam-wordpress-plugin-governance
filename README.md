# SolveBeam WordPress Plugin Governance

Opinionated governance and AI-driven standards for modern WordPress plugin development. Enforces strict architecture, tooling, auditing, refactoring, and clean distribution practices while supporting the latest three major releases of PHP and WordPress.

## Installation

```bash
npx skills add https://github.com/solvebeam/solvebeam-wordpress-plugin-governance --skill solvebeam-wordpress-plugin-governance
```

This clones the skill into `.agents/skills/solvebeam-wordpress-plugin-governance/` in your project.

## Usage

The skill is automatically discovered by VS Code Copilot (and other compatible agents) based on its `SKILL.md` description. There are two ways to invoke it:

### Slash command

Type `/` in Copilot Chat and select **solvebeam-wordpress-plugin-governance** from the list. Then type your request.

### Natural language

Simply describe what you need in Copilot Chat. The agent will detect that this skill is relevant and load it automatically. For example:

> _"Audit my plugin for SolveBeam compliance"_

## Modes

The skill supports four modes. Mention the mode by name in your chat message to activate it.

### `audit`

Produces a structured compliance report — no code changes.

```
Audit my-plugin against SolveBeam standards
```

### `config`

Safe, non-breaking modernization: adds missing tooling config, `declare(strict_types=1)`, dist hygiene files, and documentation.

```
Run config mode on my-plugin
```

### `refactor`

Everything in **config**, plus namespace flattening, `psr-4/` migration, singleton enforcement, and full hook rewrite. May introduce breaking changes.

```
Refactor my-plugin to SolveBeam standards
```

### `scaffold`

Generates a brand-new, fully compliant plugin from the canonical boilerplate.

```
Scaffold a new plugin called "My Awesome Feature"
```

## Links

- https://skills.sh/
- https://skills.sh/docs
- https://skills.sh/jeffallan/claude-skills/wordpress-pro
- https://github.com/vercel-labs/agent-skills/blob/main/skills/web-design-guidelines/SKILL.md
- https://github.com/Jeffallan/claude-skills/tree/main/skills/wordpress-pro
- https://developers.openai.com/codex/skills/
- https://github.com/openai/skills
- https://agentskills.io/specification
- https://www.solvebeam.com/
- https://code.visualstudio.com/docs/copilot/customization/agent-skills
