# BioLib plugins

Plugins for using [BioLib](https://biolib.com) from AI coding agents such as Claude Code and Codex.

## Install

Claude Code:

```
/plugin marketplace add biolib/plugins
/plugin install biolib@biolib
```

Codex:

```
codex plugin marketplace add biolib/plugins
```

Then install the `biolib` plugin from `/plugins`.

Other agents that support Agent Skills:

```
npx skills add biolib/plugins
```

## Layout

- `.claude-plugin/marketplace.json`: marketplace for Claude Code
- `.agents/plugins/marketplace.json`: marketplace for Codex
- `plugins/biolib/`: the `biolib` plugin, with manifests for Claude Code (`.claude-plugin/plugin.json`) and Codex (`plugin.json`)
- `plugins/biolib/skills/biolib/SKILL.md`: the skill, shared by all agents
