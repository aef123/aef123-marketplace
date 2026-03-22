# aef123-marketplace

A private plugin marketplace for [Claude Code CLI](https://docs.anthropic.com/en/docs/claude-code) and [GitHub Copilot CLI](https://docs.github.com/en/copilot/how-tos/copilot-cli). This marketplace is for personal use — saving and sharing plugins across agents and machines.

## Quick Start

### Add this marketplace to GitHub Copilot CLI

```bash
copilot plugin marketplace add aef123/aef123-marketplace
```

### Add this marketplace to Claude Code CLI (interactive session)

```
/plugin marketplace add aef123/aef123-marketplace
```

### Install a plugin from this marketplace

```bash
# List available plugins
copilot plugin marketplace browse aef123-marketplace

# Install the install-marketplace skill
copilot plugin install install-marketplace@aef123-marketplace
```

---

## Available Plugins

### `install-marketplace`

A skill that discovers and installs popular plugin marketplaces for both Claude Code CLI and GitHub Copilot CLI.

**What it does:**

- Detects which CLI tools (Claude Code CLI, Copilot CLI) are available on the system
- Installs any of the popular marketplaces listed below with a single command
- Verifies successful installation and browses available plugins

**Supported marketplaces it can install:**

| Marketplace | Identifier | Description |
|-------------|-----------|-------------|
| Anthropic Official | `anthropics/claude-code` | Official Anthropic plugins for Claude Code CLI |
| GitHub Copilot Plugins | `github/copilot-plugins` | GitHub's official curated plugin collection |
| Awesome Copilot | `github/awesome-copilot` | Community-curated high-quality Copilot plugins |
| This marketplace | `aef123/aef123-marketplace` | This private marketplace |

---

## Supported Marketplaces

This marketplace provides a skill to install any of the following popular marketplaces:

### Anthropic Official — `anthropics/claude-code`

The official plugin marketplace from Anthropic. Contains plugins built and maintained by the Anthropic team for Claude Code CLI.

```bash
copilot plugin marketplace add anthropics/claude-code
```

### GitHub Copilot Plugins — `github/copilot-plugins`

GitHub's official curated plugin collection for Copilot CLI. Registered by default in Copilot CLI installations.

```bash
copilot plugin marketplace add github/copilot-plugins
```

### Awesome Copilot — `github/awesome-copilot`

A community-curated collection of high-quality plugins for Copilot CLI. Registered by default in Copilot CLI installations.

```bash
copilot plugin marketplace add github/awesome-copilot
```

---

## How Plugin Marketplaces Work

### Copilot CLI

Copilot CLI comes with two default marketplaces (`copilot-plugins` and `awesome-copilot`). You can add more with:

```bash
copilot plugin marketplace add OWNER/REPO          # GitHub repository
copilot plugin marketplace add https://git.url.git # Any Git URL
copilot plugin marketplace add /local/path          # Local path

copilot plugin marketplace list                     # List all registered
copilot plugin marketplace browse MARKETPLACE-NAME  # Browse plugins
copilot plugin marketplace remove MARKETPLACE-NAME  # Unregister
```

### Claude Code CLI

In an interactive Claude Code CLI session:

```
/plugin marketplace add OWNER/REPO
/plugin marketplace list
/plugin marketplace browse MARKETPLACE-NAME
```

### Installing Plugins

```bash
copilot plugin install PLUGIN-NAME@MARKETPLACE-NAME  # From marketplace
copilot plugin install OWNER/REPO                    # Directly from GitHub
copilot plugin install OWNER/REPO:PATH/TO/PLUGIN     # From subdirectory
copilot plugin install ./local/path                  # From local path

copilot plugin list                                  # View installed plugins
copilot plugin update PLUGIN-NAME                    # Update a plugin
copilot plugin uninstall PLUGIN-NAME                 # Remove a plugin
```

---

## Repository Structure

```
aef123-marketplace/
├── .github/
│   └── plugin/
│       └── marketplace.json         # Copilot CLI marketplace manifest
├── .claude-plugin/
│   └── marketplace.json             # Claude Code CLI marketplace manifest
├── plugins/
│   └── install-marketplace/
│       ├── plugin.json              # Plugin manifest
│       └── skills/
│           └── install-marketplace/
│               └── SKILL.md         # Skill definition
├── .gitignore
└── README.md
```

---

## Adding a New Plugin

To add a new plugin to this marketplace:

1. Create a new directory under `plugins/PLUGIN-NAME/`
2. Add a `plugin.json` manifest at the root of that directory
3. Add skill, agent, hook, or MCP server files as needed
4. Add the plugin entry to both `marketplace.json` files

**Minimum plugin structure:**

```
plugins/my-plugin/
├── plugin.json        # Required
├── skills/
│   └── my-skill/
│       └── SKILL.md
└── agents/
    └── my-agent.agent.md
```

**`plugin.json` example:**

```json
{
  "name": "my-plugin",
  "description": "Description of what this plugin does",
  "version": "1.0.0",
  "author": { "name": "aef123" },
  "skills": "skills/",
  "agents": "agents/"
}
```

---

## References

- [Claude Code CLI documentation](https://docs.anthropic.com/en/docs/claude-code)
- [Creating plugins for GitHub Copilot CLI](https://docs.github.com/en/copilot/how-tos/copilot-cli/customize-copilot/plugins-creating)
- [Creating a plugin marketplace for Copilot CLI](https://docs.github.com/en/copilot/how-tos/copilot-cli/customize-copilot/plugins-marketplace)
- [Finding and installing Copilot CLI plugins](https://docs.github.com/en/copilot/how-tos/copilot-cli/customize-copilot/plugins-finding-installing)
- [GitHub Copilot CLI plugin reference](https://docs.github.com/en/copilot/reference/copilot-cli-reference/cli-plugin-reference)
- [Anthropic official plugins](https://github.com/anthropics/claude-code)
- [Awesome Copilot community plugins](https://github.com/github/awesome-copilot)