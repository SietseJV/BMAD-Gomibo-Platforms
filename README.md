## Introduction

This repository is a Gomibo Platforms adaptation of the [BMAD repository](https://github.com/bmad-code-org/BMAD-METHOD). This repository provides a set of agents and workflows that guide you through the complete product lifecycle, from brainstorming to deployment. Some highlights:

* AI Intelligent Help — Invoke the bmad-help skill anytime for guidance on what's next
* Scale-Domain-Adaptive — Automatically adjusts planning depth based on project complexity
* Structured Workflows — Grounded in agile best practices across analysis, planning, architecture, and implementation
* Specialized Agents — 12+ domain experts (PM, Architect, Developer, UX, and more)
* Party Mode — Bring multiple agent personas into one session to collaborate and discuss

Learn more at [docs.bmad-method.org](https://docs.bmad-method.org/).

## Quick Start

**Prerequisites**: [Node.js](https://nodejs.org) v20+ · [Python](https://www.python.org) 3.10+ · [uv](https://docs.astral.sh/uv/)

```bash
npx bmad-method install
```

> Want the newest prerelease build? Use `npx bmad-method@next install`. Expect higher churn than the default install.

Follow the installer prompts, then open your AI IDE (Claude Code, Cursor, etc.) in your project folder.

**Non-Interactive Installation** (for CI/CD):

```bash
npx bmad-method install --directory /path/to/project --modules bmm --tools claude-code --yes
```

Override any module config option with `--set <module>.<key>=<value>` (repeatable). Run `--list-options [module]` to see locally-known official keys (built-in modules plus any external officials cached on this machine):

```bash
npx bmad-method install --yes \
  --modules bmm --tools claude-code \
  --set bmm.project_knowledge=research \
  --set bmm.user_skill_level=expert
```

[See all installation options](https://docs.bmad-method.org/how-to/non-interactive-installation/)

> **Not sure what to do?** Ask `bmad-help` — it tells you exactly what's next and what's optional. You can also ask questions like `bmad-help I just finished the architecture, what do I do next?`

## Documentation

[BMad Method Docs Site](https://docs.bmad-method.org) — Tutorials, guides, concepts, and reference

**Quick links:**
- [Getting Started Tutorial](https://docs.bmad-method.org/tutorials/getting-started/)
- [Upgrading from Previous Versions](https://docs.bmad-method.org/how-to/upgrade-to-v6/)
- [Test Architect Documentation](https://bmad-code-org.github.io/bmad-method-test-architecture-enterprise/)