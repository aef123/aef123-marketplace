---
name: install-marketplace
description: Install and manage plugin marketplaces for Claude Code CLI and GitHub Copilot CLI. Supports the Anthropic official marketplace, GitHub Copilot official marketplace, and popular community marketplaces.
---

## Overview

This skill helps you install and manage plugin marketplaces for Claude Code CLI and GitHub Copilot CLI. It handles detection of which CLI tools are available, registers the requested marketplace(s), and verifies the installation.

## Supported Marketplaces

The following marketplaces are available to install:

| Name | Identifier | Description |
|------|-----------|-------------|
| Anthropic Official | `anthropics/claude-code` | Official Anthropic plugins for Claude Code CLI, including frontend design, security checks, and more |
| GitHub Copilot Plugins | `github/copilot-plugins` | GitHub's official curated plugin collection for Copilot CLI |
| Awesome Copilot | `github/awesome-copilot` | Community-curated collection of high-quality Copilot CLI plugins |
| This marketplace | `aef123/aef123-marketplace` | This private marketplace (already registered if you're using this skill) |

## Usage

When asked to install a marketplace, use the appropriate commands below based on which CLI tools are available on the system.

### Detect Available CLI Tools

First, check which CLI tools are installed:

```bash
# Check for GitHub Copilot CLI
which copilot 2>/dev/null && copilot --version || echo "Copilot CLI not found"

# Check for Claude Code CLI
which claude 2>/dev/null && claude --version || echo "Claude Code CLI not found"
```

### Install Marketplace — GitHub Copilot CLI

Use `copilot plugin marketplace add` to register a marketplace. After adding, list available plugins with `copilot plugin marketplace browse`.

**Anthropic Official Marketplace:**
```bash
copilot plugin marketplace add anthropics/claude-code
copilot plugin marketplace browse anthropics/claude-code
```

**GitHub Copilot Plugins (Official):**
```bash
copilot plugin marketplace add github/copilot-plugins
copilot plugin marketplace browse github/copilot-plugins
```

**Awesome Copilot (Community):**
```bash
copilot plugin marketplace add github/awesome-copilot
copilot plugin marketplace browse github/awesome-copilot
```

**This private marketplace:**
```bash
copilot plugin marketplace add aef123/aef123-marketplace
copilot plugin marketplace browse aef123-marketplace
```

**Custom marketplace from any Git URL:**
```bash
copilot plugin marketplace add https://github.com/OWNER/REPO.git
```

**Verify all registered marketplaces:**
```bash
copilot plugin marketplace list
```

### Install Marketplace — Claude Code CLI (Interactive Session)

Within a Claude Code interactive session, use `/plugin marketplace add` commands:

**Anthropic Official Marketplace:**
```
/plugin marketplace add anthropics/claude-code
```

**GitHub Copilot Plugins (Official):**
```
/plugin marketplace add github/copilot-plugins
```

**Awesome Copilot (Community):**
```
/plugin marketplace add github/awesome-copilot
```

**This private marketplace:**
```
/plugin marketplace add aef123/aef123-marketplace
```

**Verify all registered marketplaces:**
```
/plugin marketplace list
```

### Install All Popular Marketplaces at Once

To install all supported marketplaces in a single step using Copilot CLI:

```bash
copilot plugin marketplace add anthropics/claude-code && \
copilot plugin marketplace add github/copilot-plugins && \
copilot plugin marketplace add github/awesome-copilot && \
copilot plugin marketplace list
```

## Installing Plugins from a Marketplace

After registering a marketplace, install plugins from it:

```bash
# List what's available in a marketplace
copilot plugin marketplace browse MARKETPLACE-NAME

# Install a specific plugin
copilot plugin install PLUGIN-NAME@MARKETPLACE-NAME

# Examples
copilot plugin install frontend-design@anthropics/claude-code
copilot plugin install database-data-management@github/awesome-copilot
```

Or install a plugin directly from a GitHub repository without registering a marketplace:

```bash
copilot plugin install OWNER/REPO
copilot plugin install OWNER/REPO:PATH/TO/PLUGIN
```

## Removing a Marketplace

```bash
copilot plugin marketplace remove MARKETPLACE-NAME
# Use --force to also uninstall all plugins from that marketplace
copilot plugin marketplace remove MARKETPLACE-NAME --force
```

## Instructions for the AI Agent

When the user asks to install a marketplace:

1. **Determine intent**: Ask the user which marketplace(s) they want to install if they have not specified. Present the supported list above.

2. **Detect available CLIs**: Run the detection commands above to determine which CLI tools are available.

3. **Run the install commands**: Execute the appropriate `copilot plugin marketplace add` commands for the Copilot CLI. For Claude Code CLI, provide the equivalent `/plugin marketplace add` commands for the user to run in their interactive session (the agent cannot run these directly since they are interactive session commands).

4. **Verify**: After installation, run `copilot plugin marketplace list` to confirm the marketplace was registered.

5. **Browse**: Optionally browse the newly added marketplace to show the user what plugins are available.
