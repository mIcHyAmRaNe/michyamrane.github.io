---
title: Implementing oh-my-opencode-slim in Opencode
date: 2026-09-03
categories:
  - opencode
  - ai
  - agents
---

[oh-my-opencode-slim](https://github.com/alvinunreal/oh-my-opencode-slim) turns [Opencode](https://opencode.ai) into a multi-agent suite: one orchestrator plans the work, then auto-delegates to specialists. Mix any models from any providers, balance quality / speed / cost.

My setup runs entirely on free-tier models — no usage cost.

<!-- more -->

## What you get

- **Orchestrator** — master delegator, plans and reconciles work
- **Explorer** — fast codebase reconnaissance
- **Oracle** — architecture, hard debugging, code review
- **Librarian** — external docs / web research
- **Designer** — UI/UX implementation and polish
- **Fixer** — fast bounded implementation
- **Observer** — visual analysis (screenshots, PDFs, diagrams)

> **Opencode Multi Agent Suite · Mix any models · Auto delegate tasks**

## 1. Install Opencode

Follow the official install: [opencode.ai](https://opencode.ai).

```bash
# quick check
opencode --version
```

## 2. Install oh-my-opencode-slim

```bash
bunx oh-my-opencode-slim@latest install
```

No Bun? `npx` works too since the CLI is a Node-compatible bundle:

```bash
npx oh-my-opencode-slim@latest install
```

This registers the plugin in `~/.config/opencode/opencode.json` and creates `~/.config/opencode/oh-my-opencode-slim.json`.

Docs: [Installation Guide](https://github.com/alvinunreal/oh-my-opencode-slim/blob/master/docs/installation.md) · [Configuration](https://github.com/alvinunreal/oh-my-opencode-slim/blob/master/docs/configuration.md).

## 3. Get API keys from providers

My preset below mixes free models from a few providers. Grab keys from each one you want to use:

- Opencode Zen (`opencode/*`) — from your Opencode account
- OpenRouter (`openrouter/*`) — [openrouter.ai](https://openrouter.ai)
- Bai (`bai/*`) — Bai API console
- Pollination (`pollination/*`) — [pollination.ai](https://pollination.ai)

You don't need all of them on day one — start with one or two, add the rest later. Each agent has a fallback list, so if the first model fails / rate-limits, the next one is tried.

## 4. Connect providers in Opencode

Inside Opencode:

```text
/connect
```

Find the provider in the list and paste your key. If your provider isn't listed, add it as a custom provider — see [Opencode providers docs](https://opencode.ai/docs/providers/).

Repeat for every provider you collected keys for in step 3.

## 5. Refresh models

Once providers are connected:

```bash
opencode models --refresh
```

Then list to confirm Opencode sees them:

```bash
opencode models --list
```

If a model is missing here, it will be missing in the slim config too. Fix auth first, then continue.

## 6. Edit the slim config

Open the config file:

```bash
nano ~/.config/opencode/oh-my-opencode-slim.json
```

Here is my working `opencode-zen-free` preset — every agent on a free model:

```json
{
  "$schema": "https://unpkg.com/oh-my-opencode-slim@latest/oh-my-opencode-slim.schema.json",
  "preset": "opencode-zen-free",
  "fallback": {
    "enabled": true
  },
  "disabled_agents": [],
  "presets": {
    "opencode-zen-free": {
      "orchestrator": {
        "model": [
          "opencode/muse-spark-1.3-contributor-free",
          "openrouter/thinkingmachines/inkling:free"
        ],
        "variant": "xhigh",
        "temperature": 0.4,
        "color": "#CBA6F7",
        "skills": ["*"],
        "mcps": ["*", "!context7"]
      },
      "oracle": {
        "model": [
          "bai/qwen3.8-flash",
          "opencode/muse-spark-1.3-contributor-free"
        ],
        "variant": "xhigh",
        "temperature": 0.3,
        "color": "#F38BA8",
        "skills": ["simplify"],
        "mcps": []
      },
      "explorer": {
        "model": [
          "bai/qwen3.8-flash",
          "openrouter/thinkingmachines/inkling-small:free"
        ],
        "temperature": 0.2,
        "color": "#89B4FA",
        "skills": [],
        "mcps": []
      },
      "librarian": {
        "model": [
          "openrouter/thinkingmachines/inkling-small:free",
          "openrouter/nvidia/nemotron-3-ultra-550b-a55b:free"
        ],
        "temperature": 0.2,
        "color": "#A6E3A1",
        "skills": [],
        "mcps": ["context7", "gh_grep"]
      },
      "designer": {
        "model": [
          "bai/glm-5.3-flash",
          "pollination/morriszdweck/glm-fast"
        ],
        "temperature": 0.3,
        "color": "#F5C2E7",
        "skills": [],
        "mcps": []
      },
      "fixer": {
        "model": [
          "opencode/muse-spark-1.3-contributor-free",
          "bai/glm-5.3-flash"
        ],
        "variant": "xhigh",
        "temperature": 0.3,
        "color": "#FAB387",
        "skills": [],
        "mcps": []
      },
      "observer": {
        "model": [
          "openrouter/thinkingmachines/inkling-small:free",
          "openrouter/nvidia/nemotron-3-ultra-550b-a55b:free"
        ],
        "variant": "low",
        "temperature": 0.2,
        "color": "#94E2D5",
        "skills": [],
        "mcps": []
      }
    }
  }
}
```

What matters in this file:

- `preset` — which preset is active. Must match a key under `presets`.
- `fallback.enabled: true` — if the first model in an agent's list fails, try the next.
- `model` as an array — priority order. First = primary, rest = fallbacks.
- `disabled_agents: []` — empty means Observer stays enabled (needed for images/PDFs since some orchestrator models aren't multimodal).
- `skills` / `mcps` per agent — permission grants. Orchestrator gets `["*"]`, specialists get only what they need. Librarian gets `context7` + `gh_grep` because that's its job.

Save, then restart Opencode.

## 7. Verify

```bash
opencode
```

Then in the TUI:

```text
ping all agents
```

You should see every agent reply. If one fails, check its provider auth (step 4) and that `opencode models --list` contains its model (step 5).

## 8. Run it

Just describe the task — the orchestrator builds the work graph and dispatches specialists in the background:

```text
Add dark mode to the settings page, check the Tailwind docs for the current way, and keep it responsive
```

That one sentence fans out to Librarian (docs) + Explorer (codebase) + Designer (UI) + Fixer (implementation), reconciled back into one result.

Manual control when you want it:

```text
@explorer where is auth handled?
@librarian how does Opencode custom provider auth work?
@oracle review this refactor plan
@designer polish this landing page
@fixer rename getCwd to getCurrentWorkingDirectory across src/
```

Other useful bits:

- `/preset` — switch the whole team's models at runtime
- `run codemap` — hierarchical map for unfamiliar repos
- Bundled skills: `deepwork`, `verification-planning`, `simplify`, `worktrees`, `clonedeps`, `reflect` — see [Skills docs](https://github.com/alvinunreal/oh-my-opencode-slim/blob/master/docs/skills.md)

## Troubleshooting

- **Agent model not found** → you skipped step 5. `opencode models --refresh`, confirm with `--list`.
- **Auth error on one agent** → `/connect` again for that provider, then refresh.
- **Want latest plugin code** → run from master per the [README](https://github.com/alvinunreal/oh-my-opencode-slim#run-from-master), or pin a version in the `plugin` array.
- **Full reference** → [Configuration](https://github.com/alvinunreal/oh-my-opencode-slim/blob/master/docs/configuration.md) · [Background orchestration](https://github.com/alvinunreal/oh-my-opencode-slim/blob/master/docs/background-orchestration.md).

That's it — install Opencode, install the slim plugin, connect providers, refresh models, paste the config, and you have a free multi-agent coding team.
