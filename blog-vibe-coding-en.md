# My Vibe Coding Workflow: A Complete Guide from Terminal to AI Programming

> This article will guide you through setting up a complete Vibe Coding environment from scratch, including terminal configuration, shell customization, AI programming tools, and advanced techniques.

## Table of Contents

1. [Introduction](#1-introduction)
2. [Terminal Configuration](#2-terminal-configuration)
3. [Oh-My-Zsh Configuration](#3-oh-my-zsh-configuration)
4. [Factory Droid - The Core Vibe Coding Tool](#4-factory-droid---the-core-vibe-coding-tool)
5. [BYOK - Model Selection Guide](#5-byok---model-selection-guide)
6. [Skills System](#6-skills-system)
7. [Custom Droids](#7-custom-droids)
8. [MCP (Model Context Protocol)](#8-mcp-model-context-protocol)
9. [Workflow Example](#9-workflow-example)
10. [Summary and Resources](#10-summary-and-resources)

---

## 1. Introduction

### What is Vibe Coding?

Vibe Coding is a new programming paradigm where you interact with AI assistants through natural language conversations to complete programming tasks. Simply describe what you want to achieve, and the AI will help you write, debug, and optimize code. This approach makes programming more intuitive and efficient.

### Why This Toolchain?

- **Modern Terminal Experience**: Warp and Kitty provide smooth, beautiful terminal interfaces
- **Efficient Shell Environment**: Oh-My-Zsh + Powerlevel10k brings powerful command-line enhancements
- **Intelligent AI Programming**: Factory Droid provides professional-grade AI programming assistance
- **Flexible Model Selection**: BYOK lets you use any LLM model
- **Extensible Skills System**: Skills and Custom Droids make AI better understand your workflow

### Target Audience

This tutorial is for all developers interested in AI programming, whether you're a beginner or an experienced professional. Each step includes detailed instructions - just follow along to complete the setup.

---

## 2. Terminal Configuration

A good terminal is the foundation of Vibe Coding. Here we introduce two excellent modern terminals.

### 2.1 Warp Terminal

Warp is a modern terminal with built-in AI features, designed for developers.

![Warp Terminal Interface](<!-- IMAGE: Warp terminal main interface screenshot -->)

#### Features

- 🚀 Built-in AI command suggestions
- 📝 Block-based command output for easy copying and sharing
- 🎨 Modern UI design
- ⚡ Ultra-fast startup and response

#### Installation Steps

**Linux (Debian/Ubuntu):**

```bash
# Download and install
wget https://releases.warp.dev/stable/v0.2024.11.12.08.02.stable_01/warp-terminal_0.2024.11.12.08.02.stable.01_amd64.deb
sudo dpkg -i warp-terminal_0.2024.11.12.08.02.stable.01_amd64.deb
```

**macOS:**

```bash
brew install --cask warp
```

![Warp Installation Complete](<!-- IMAGE: Warp welcome screen after installation -->)

### 2.2 Kitty Terminal (Alternative)

Kitty is a GPU-accelerated terminal emulator that is highly customizable with excellent performance.

![Kitty Terminal Interface](<!-- IMAGE: Kitty terminal main interface screenshot -->)

#### Features

- 🖥️ GPU rendering for ultra-fast speed
- ⚙️ Highly configurable
- 🖼️ Image display support
- 📑 Built-in tabs and splits

#### Installation Steps

**Linux (Debian/Ubuntu):**

```bash
sudo apt install kitty
```

**macOS:**

```bash
brew install --cask kitty
```

#### Basic Configuration

Create or edit the configuration file `~/.config/kitty/kitty.conf`:

```conf
# Font configuration
font_family      FiraCode Nerd Font
bold_font        auto
italic_font      auto
bold_italic_font auto
font_size        14.0

# Window configuration
window_padding_width 10
hide_window_decorations yes
background_opacity 0.95

# Color theme - Catppuccin Mocha
foreground              #CDD6F4
background              #1E1E2E
selection_foreground    #1E1E2E
selection_background    #F5E0DC

# Tab bar
tab_bar_edge bottom
tab_bar_style powerline
tab_powerline_style slanted

# Shortcuts
map ctrl+shift+t new_tab
map ctrl+shift+q close_tab
map ctrl+shift+right next_tab
map ctrl+shift+left previous_tab

# Scrolling
scrollback_lines 10000
wheel_scroll_multiplier 5.0

# Cursor
cursor_shape beam
cursor_blink_interval 0.5
```

![Kitty Configuration Result](<!-- IMAGE: Kitty after configuration screenshot -->)

---

## 3. Oh-My-Zsh Configuration

Oh-My-Zsh is an open-source Zsh configuration management framework that provides numerous themes and plugins.

### 3.1 Installing Oh-My-Zsh

First, ensure Zsh is installed:

```bash
# Check if installed
zsh --version

# If not installed, on Ubuntu/Debian
sudo apt install zsh

# Set Zsh as default shell
chsh -s $(which zsh)
```

Install Oh-My-Zsh:

```bash
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

![Oh-My-Zsh Installation](<!-- IMAGE: Oh-My-Zsh installation process screenshot -->)

### 3.2 Powerlevel10k Theme

Powerlevel10k is one of the most popular Zsh themes, offering rich information display and extremely fast rendering.

#### Installing Nerd Font

First, install a Nerd Font to display icons correctly:

```bash
# Download FiraCode Nerd Font
mkdir -p ~/.local/share/fonts
cd ~/.local/share/fonts
curl -fLo "FiraCode Nerd Font Regular.ttf" \
  https://github.com/ryanoasis/nerd-fonts/raw/master/patched-fonts/FiraCode/Regular/FiraCodeNerdFont-Regular.ttf

# Refresh font cache
fc-cache -fv
```

#### Installing Powerlevel10k

```bash
git clone --depth=1 https://github.com/romkatv/powerlevel10k.git \
  ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k
```

Edit `~/.zshrc` and set the theme:

```bash
ZSH_THEME="powerlevel10k/powerlevel10k"
```

After reopening the terminal, the configuration wizard will start automatically:

```bash
# Manually start the configuration wizard
p10k configure
```

![Powerlevel10k Configuration Wizard](<!-- IMAGE: Powerlevel10k configuration wizard screenshot -->)

### 3.3 Plugin Configuration

Here are my recommended plugins, each significantly enhancing your command-line experience.

#### Installing Third-party Plugins

```bash
# zsh-autosuggestions - Command auto-completion suggestions
git clone https://github.com/zsh-users/zsh-autosuggestions \
  ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions

# zsh-syntax-highlighting - Command syntax highlighting
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git \
  ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting

# zsh-completions - Additional command completions
git clone https://github.com/zsh-users/zsh-completions \
  ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-completions
```

#### Configuring Plugins

Edit `~/.zshrc` and configure the plugin list:

```bash
plugins=(
    git                      # Git command aliases and status prompts
    sudo                     # Double-tap ESC to add sudo before command
    history                  # Enhanced history command search
    extract                  # Universal extraction command for various formats
    z                        # Smart directory jumping
    zsh-autosuggestions      # Auto-suggest based on command history
    zsh-syntax-highlighting  # Command syntax highlighting
    zsh-completions          # Additional command completions
)
```

Apply the configuration:

```bash
source ~/.zshrc
```

#### Plugin Function Description

| Plugin                  | Function             | Usage Example                                                     |
| ----------------------- | -------------------- | ----------------------------------------------------------------- |
| `git`                     | Git command aliases  | `gst` = `git status`, `gco` = `git checkout`                              |
| `sudo`                    | Quick sudo addition  | Double-tap `ESC` to add sudo before current command                 |
| `history`                 | History search       | `Ctrl+R` to search command history                                  |
| `extract`                 | Universal extraction | `extract file.tar.gz` auto-detects format                           |
| `z`                       | Smart jumping        | `z project` jumps to frequently used directory containing "project" |
| `zsh-autosuggestions`     | Command suggestions  | Shows gray suggestions while typing, press `→` to accept            |
| `zsh-syntax-highlighting` | Syntax highlighting  | Correct commands in green, errors in red                          |
| `zsh-completions`         | Extra completions    | More Tab completion support for commands                          |

![Plugin Effects Demo](<!-- IMAGE: Plugin effects comparison screenshot -->)

---

## 4. Factory Droid - The Core Vibe Coding Tool

Factory Droid is a professional AI programming assistant that runs in the terminal, allowing you to interact with code through natural language.

### 4.1 What is Factory Droid

Factory Droid is a command-line AI programming tool from Factory AI with the following features:

- 🤖 Powerful code understanding and generation capabilities
- 📁 Direct file system read/write
- 🔧 Shell command execution
- 🌐 Support for multiple LLM models
- 🎯 Extensible Skills system
- 🔗 MCP protocol support

![Factory Droid Interface](<!-- IMAGE: Factory Droid running interface screenshot -->)

### 4.2 Installation and Configuration

#### Installation

```bash
# macOS/Linux
curl -fsSL https://app.factory.ai/cli | sh
```

**Linux users:** Ensure `xdg-utils` is installed for full functionality: `sudo apt-get install xdg-utils`

#### Getting Started

```bash
# Navigate to your project
cd /path/to/your/project

# Start interactive session
droid
```

On first run, you'll be guided to sign in via your browser to connect to Factory.

#### Configuration File

Configuration file is located at `~/.factory/settings.json`. You can modify settings interactively using the `/settings` command.

#### Session Default Settings

Configure default behavior in `settings.json`:

```json
{
  "sessionDefaultSettings": {
    "model": "claude-opus-4-5-20251101",
    "reasoningEffort": "high",
    "autonomyMode": "spec",
    "specModeReasoningEffort": "off"
  }
}
```

| Setting                 | Options                                        | Description         |
| ----------------------- | ---------------------------------------------- | ------------------- |
| `model`                   | opus, sonnet, gpt-5.1, gpt-5.2, haiku, etc.    | Default AI model    |
| `reasoningEffort`         | off, none, low, medium, high                   | Reasoning depth     |
| `autonomyMode`            | normal, spec, auto-low, auto-medium, auto-high | Autonomy mode       |
| `specModeReasoningEffort` | off, none, low, medium, high                   | Spec mode reasoning |

### 4.3 Hooks Configuration

Hooks allow you to automatically execute operations when specific events occur, greatly enhancing workflows.

Edit `~/.factory/settings.json`:

```json
{
  "hooks": {
    "SessionStart": [
      {
        "matcher": "startup|resume",
        "hooks": [
          {
            "type": "command",
            "command": "echo '[planning-with-files] Ready. For complex tasks, create task_plan.md, findings.md, and progress.md in your project directory.'"
          }
        ]
      }
    ],
    "PreToolUse": [
      {
        "matcher": "Write|Edit|Bash",
        "hooks": [
          {
            "type": "command",
            "command": "if [ -f \"$FACTORY_PROJECT_DIR/task_plan.md\" ]; then head -30 \"$FACTORY_PROJECT_DIR/task_plan.md\"; fi"
          }
        ]
      }
    ],
    "PostToolUse": [
      {
        "matcher": "Write|Edit",
        "hooks": [
          {
            "type": "command",
            "command": "echo '[planning-with-files] File updated. If this completes a phase, update task_plan.md status.'"
          },
          {
            "type": "command",
            "command": "~/.factory/skills/md-table-formatter/scripts/format-tables.py",
            "timeout": 10
          }
        ]
      }
    ],
    "Stop": [
      {
        "hooks": [
          {
            "type": "command",
            "command": "~/.factory/skills/planning-with-files/scripts/check-complete.sh 2>/dev/null || true"
          }
        ]
      }
    ]
  }
}
```

#### Hook Types Description

| Hook Type    | Trigger Time        | Purpose                              |
| ------------ | ------------------- | ------------------------------------ |
| `SessionStart` | When session starts | Initialization prompts, load context |
| `PreToolUse`   | Before using tools  | Check status, read plans             |
| `PostToolUse`  | After using tools   | Update status, format files          |
| `Stop`         | When session ends   | Cleanup, summary                     |

### 4.4 Basic Operations

#### Keyboard Shortcuts

| Shortcut    | Function                               |
| ----------- | -------------------------------------- |
| `Enter`       | Send message                           |
| `Shift+Enter` | New line (multi-line input)            |
| `Shift+Tab`   | Switch mode (Normal/Spec/Auto)         |
| `!`           | Toggle Bash mode (when input is empty) |
| `Esc`         | Exit Bash mode / Interrupt operation   |
| `?`           | View all shortcuts                     |
| `Ctrl+C`      | Exit Droid                             |

#### Basic Interaction Flow

1. Enter your task description
2. Droid analyzes the codebase and creates a plan
3. Review the changes Droid proposes
4. Accept or reject modifications
5. Continue iterating until task is complete

### 4.5 Slash Commands

Type `/` commands in Droid to execute specific operations:

| Command   | Description                   |
| --------- | ----------------------------- |
| `/settings` | Configure Droid settings      |
| `/model`    | Switch AI model               |
| `/review`   | Start AI code review workflow |
| `/mcp`      | Manage MCP servers            |
| `/sessions` | List and select past sessions |
| `/droids`   | Manage custom Droids          |
| `/skills`   | Manage and invoke Skills      |
| `/hooks`    | Manage lifecycle Hooks        |
| `/cost`     | View token usage statistics   |
| `/new`      | Start new session             |
| `/help`     | View all available commands   |

### 4.6 Specification Mode

Specification Mode is a core Droid feature that follows the "plan first, execute later" principle.

#### How to Activate

Press **Shift+Tab** to switch to Spec mode.

#### Workflow

1. **Describe the feature** - Describe what you want in 4-6 sentences
2. **Droid generates spec** - Automatically analyzes codebase, generates detailed implementation plan
3. **Review and approve** - You can modify or approve the plan
4. **Implementation** - After approval, Droid executes and shows each change for review

#### Safety Guarantees

- Analysis phase is read-only, no files are modified
- All changes execute only after approval
- Complete visibility into the implementation plan

#### Approval Options

| Option                  | Description                                      |
| ----------------------- | ------------------------------------------------ |
| Proceed (manual)        | Approve plan, manually confirm each operation    |
| Proceed + Auto (Low)    | Approve plan, auto-execute file edits and reads  |
| Proceed + Auto (Medium) | + Auto-execute reversible commands (npm install) |
| Proceed + Auto (High)   | + Auto-execute high-risk commands (git push)     |
| Keep iterating          | Continue refining the spec                       |

### 4.7 Auto-Run Mode

Auto-Run mode lets you control Droid's autonomous execution level.

| Level         | Auto-executed Operations             | Examples                        |
| ------------- | ------------------------------------ | ------------------------------- |
| Auto (Low)    | File edits, read-only commands       | ls, git status, rg              |
| Auto (Medium) | + Reversible workspace modifications | npm install, git commit, mv, cp |
| Auto (High)   | + High-risk commands (not blocked)   | git push, docker, db migrations |

#### How to Switch

- Press **Shift+Tab** to cycle: Normal → Spec → Auto (Low) → Auto (Medium) → Auto (High)
- Or set the default level in `/settings`

#### Safety Mechanisms

Even in Auto (High) mode, these still require confirmation:
- Dangerous commands (e.g., `rm -rf /`)
- Command substitution (`$(...)` or backticks)
- Operations flagged by CLI security checks

### 4.8 Bash Mode

Bash mode lets you execute shell commands directly in Droid without AI interpretation.

#### How to Use

1. Press `!` when input is empty to enter Bash mode
2. Prompt changes from `>` to `$`
3. Type any shell command and press Enter to execute
4. Press `Esc` to return to AI chat mode

#### Use Cases

- Quick `git status` checks
- Run `npm test` or `make build`
- View file contents or directory structure

### 4.9 Pricing Plans

Factory measures usage through Standard Tokens. Cached tokens are billed at 1/10 (10 cached tokens = 1 Standard Token).

#### Subscription Plans

| Plan  | Standard Tokens / Month   | Price / Month |
| ----- | ------------------------- | ------------- |
| **Free**  | BYOK (Bring Your Own Key) | $0            |
| **Pro**   | 10 million (+10M bonus)   | $20           |
| **Max**   | 100 million (+100M bonus) | $200          |
| **Ultra** | 1 billion (+1B bonus)     | $2,000        |

Overage is billed at **$2.70 per million Standard Tokens**.

#### Model Pricing Multipliers

Different models have different multipliers for Standard Token calculation:

| Model             | Model ID                   | Multiplier |
| ----------------- | -------------------------- | ---------- |
| Gemini 3 Flash    | `gemini-3-flash-preview`     | 0.2×       |
| Droid Core        | `glm-4.6`                    | 0.25×      |
| Claude Haiku 4.5  | `claude-haiku-4-5-20251001`  | 0.4×       |
| GPT-5.1           | `gpt-5.1`                    | 0.5×       |
| GPT-5.1-Codex     | `gpt-5.1-codex`              | 0.5×       |
| GPT-5.1-Codex-Max | `gpt-5.1-codex-max`          | 0.5×       |
| GPT-5.2           | `gpt-5.2`                    | 0.7×       |
| Gemini 3 Pro      | `gemini-3-pro-preview`       | 0.8×       |
| Claude Sonnet 4.5 | `claude-sonnet-4-5-20250929` | 1.2×       |
| Claude Opus 4.5   | `claude-opus-4-5-20251101`   | 2×         |

#### Recommendations

- **Free Plan**: Ideal for users with existing API keys, no monthly fee
- **Pro Plan**: Great for individual developers, excellent value
- **Caching Advantage**: Factory's caching mechanism significantly reduces actual token consumption, typically achieving 4-8x cache hit ratio

---

## 5. BYOK - Model Selection Guide

BYOK (Bring Your Own Key) lets you use your own API Key to access various LLM models.

### 5.1 What is BYOK

BYOK allows you to:
- Use your own API Key to access models
- Choose the model that best fits your needs
- Control costs and usage
- Use locally deployed models

### 5.2 How to Choose Models - SWE-Rebench Leaderboard

[SWE-Rebench](https://swe-rebench.com/) is a continuously updated benchmark leaderboard for software engineering LLMs, helping you understand how various models perform on real programming tasks.

![SWE-Rebench Leaderboard](<!-- IMAGE: SWE-Rebench website screenshot -->)

#### Key Metrics Explained

| Metric             | Meaning                                    | Importance                                |
| ------------------ | ------------------------------------------ | ----------------------------------------- |
| **Resolved Rate**      | Percentage of problems successfully solved | Most important, reflects model capability |
| **Pass@5**             | Success rate within 5 attempts             | Reflects model stability                  |
| **Cost per Problem**   | Average cost per problem                   | Affects usage costs                       |
| **Tokens per Problem** | Tokens consumed per problem                | Reflects efficiency                       |

### 5.3 Recommended Models (January 2026 Data)

Based on the latest SWE-Rebench data, here are model recommendations for different scenarios:

#### Top Performance

| Model                  | Resolved Rate | Pass@5 | Cost/Problem | Features                                    |
| ---------------------- | ------------- | ------ | ------------ | ------------------------------------------- |
| **Claude Opus 4.5**        | 63.3%         | 79.2%  | $1.22        | Highest performance, best for complex tasks |
| **GPT-5.2 xhigh**          | 61.5%         | 70.8%  | $1.46        | OpenAI's strongest, excellent reasoning     |
| **Gemini 3 Flash Preview** | 60.0%         | 72.9%  | $0.29        | Extremely cost-effective                    |

#### Best Value

| Model                  | Resolved Rate | Pass@5 | Cost/Problem | Features                      |
| ---------------------- | ------------- | ------ | ------------ | ----------------------------- |
| **Gemini 3 Flash Preview** | 60.0%         | 72.9%  | $0.29        | 🏆 Best value for money        |
| **GPT-5.2 medium**         | 59.4%         | 70.8%  | $0.86        | Balanced performance and cost |
| **Claude Sonnet 4.5**      | 57.5%         | 75.0%  | $0.98        | Best for daily tasks          |

#### Open Source Models

| Model            | Resolved Rate | Pass@5 | Cost/Problem | Features                |
| ---------------- | ------------- | ------ | ------------ | ----------------------- |
| **GLM-4.7**          | 51.3%         | 66.7%  | $0.40        | 🏆 Best open source      |
| **DeepSeek-V3.2**    | 48.5%         | 68.8%  | $0.25        | Can be locally deployed |
| **Kimi K2 Thinking** | 40.5%         | 60.4%  | $0.48        | Excellent Chinese model |

#### Budget Friendly

| Model            | Resolved Rate | Pass@5 | Cost/Problem | Features                   |
| ---------------- | ------------- | ------ | ------------ | -------------------------- |
| **Grok Code Fast 1** | 35.9%         | 54.2%  | $0.08        | Cheapest                   |
| **Devstral-2-123B**  | 36.6%         | 59.6%  | $0.09        | Open source, self-hostable |
| **MiniMax M2.1**     | 37.3%         | 58.3%  | $0.10        | Cache-friendly             |

### 5.4 Custom Model Configuration

Configure custom models in `~/.factory/settings.json`:

```json
{
  "customModels": [
    {
      "model": "gpt-5.2",
      "id": "custom:my-gpt-5.2",
      "displayName": "My GPT-5.2",
      "baseUrl": "https://api.openai.com/v1",
      "apiKey": "sk-your-api-key-here",
      "provider": "openai"
    },
    {
      "model": "claude-opus-4-5",
      "id": "custom:my-opus",
      "displayName": "My Claude Opus",
      "baseUrl": "https://api.anthropic.com/v1",
      "apiKey": "sk-ant-your-key-here",
      "provider": "anthropic"
    },
    {
      "model": "deepseek-v3.2",
      "id": "custom:local-deepseek",
      "displayName": "Local DeepSeek",
      "baseUrl": "http://localhost:8080/v1",
      "apiKey": "not-needed",
      "provider": "openai"
    }
  ],
  "sessionDefaultSettings": {
    "model": "custom:my-gpt-5.2"
  }
}
```

#### Using Local Proxy

If you use a proxy service (like LiteLLM, OneAPI, etc.), configure as follows:

```json
{
  "customModels": [
    {
      "model": "claude-opus-4-5",
      "id": "custom:proxy-opus",
      "displayName": "[Proxy] Claude Opus 4.5",
      "baseUrl": "http://your-proxy-server:8000/v1",
      "apiKey": "your-proxy-key",
      "provider": "openai",
      "noImageSupport": false
    }
  ]
}
```

---

## 6. Skills System

Skills are Factory Droid's extension system, providing AI with specialized domain knowledge and workflows.

### 6.1 What are Skills

Skills are predefined instruction sets and workflows that help AI perform better in specific scenarios:

- 📋 Provide domain-specific best practices
- 🔄 Define standardized workflows
- 📝 Include templates and checklists
- 🎯 Ensure output quality and consistency

### 6.2 Recommended Skills

#### planning-with-files - Complex Task Planning

For complex tasks requiring multiple steps, using Manus-style file-based planning.

**Core Philosophy:**
```
Context Window = RAM (volatile, limited)
File System = Disk (persistent, unlimited)
→ Everything important gets written to disk
```

**Usage:**
```bash
# Create three planning files in project directory
task_plan.md   # Task plan and progress
findings.md    # Research findings
progress.md    # Session log
```

**task_plan.md Example:**
```markdown
# Task Plan: Implement User Authentication

## Goal
Implement complete user authentication system including registration, login, logout.

## Phases
- [x] Phase 1: Database model design
- [ ] Phase 2: API endpoint implementation
- [ ] Phase 3: Frontend forms
- [ ] Phase 4: Testing

## Current Status
Working on Phase 2

## Issues Encountered
| Issue               | Attempt | Solution            |
| ------------------- | ------- | ------------------- |
| JWT expiry handling | 1       | Added refresh token |
```

#### brainstorming - Creative Brainstorming

Use before any creative work to clarify requirements and design.

**Workflow:**
1. Understand current project context
2. Ask one question at a time to refine ideas
3. Propose 2-3 different approaches with trade-offs
4. Present design in sections, confirm before continuing

#### test-driven-development - TDD Development

Enforces test-driven development workflow.

**Core Principle:**
```
No production code without a failing test first
```

**Red-Green-Refactor Cycle:**
1. **RED** - Write a failing test
2. **Verify RED** - Confirm test fails for the right reason
3. **GREEN** - Write minimal code to pass the test
4. **Verify GREEN** - Confirm test passes
5. **REFACTOR** - Refactor code, keep tests green

#### verification-before-completion - Pre-completion Verification

Prevents claiming work is complete without verification.

**Core Principle:**
```
No completion claims without fresh verification evidence
```

**Verification Checklist:**
- [ ] Run test command, confirm 0 failures
- [ ] Run lint command, confirm 0 errors
- [ ] Run build command, confirm success
- [ ] Check each requirement is met

#### code-simplifier - Code Simplification

Automatically applied after writing or modifying code to simplify and optimize.

**Optimization Areas:**
- Reduce unnecessary complexity and nesting
- Eliminate redundant code
- Improve naming
- Follow project coding standards

### 6.3 Skills Installation and Configuration

Skills are stored in the `~/.factory/skills/` directory:

```bash
# View installed skills
ls ~/.factory/skills/

# Each skill is a directory containing a SKILL.md definition file
~/.factory/skills/
├── brainstorming/
│   └── SKILL.md
├── planning-with-files/
│   ├── SKILL.md
│   ├── scripts/
│   └── templates/
├── test-driven-development/
│   └── SKILL.md
└── verification-before-completion/
    └── SKILL.md
```

#### Creating Custom Skills

Create `~/.factory/skills/my-skill/SKILL.md`:

```markdown
---
name: my-skill
description: This is my custom skill description
---

# My Skill

## Overview
Describe the purpose of this skill...

## When to Use
When to use this skill...

## Process
Specific workflow...
```

---

## 7. Custom Droids

Custom Droids are specialized AI agents optimized for specific tasks.

### 7.1 What are Custom Droids

Difference between Custom Droids and Skills:
- **Skills**: Knowledge and guidance provided to the main AI
- **Custom Droids**: Independent specialized AI agents

Custom Droids can:
- Autonomously handle specific types of tasks
- Have specialized system prompts
- Use different model configurations

### 7.2 Creating Custom Droids

Droids are stored in the `~/.factory/droids/` directory:

#### Example: code-simplifier Droid

Create `~/.factory/droids/code-simplifier.md`:

```markdown
---
name: code-simplifier
description: "Simplifies and refines code for clarity, consistency, and maintainability while preserving all functionality. Use after writing or modifying code."
---

# Code Simplifier

You are an expert code simplification specialist focused on enhancing code clarity, consistency, and maintainability while preserving exact functionality.

## 1. Preserve Functionality
Never change what the code does - only how it does it.

## 2. Apply Project Standards
Follow the established coding standards from project configuration.

## 3. Enhance Clarity
Simplify code structure by:
- Reducing unnecessary complexity and nesting
- Eliminating redundant code
- Improving readability through clear naming
- Avoiding nested ternary operators

## 4. Maintain Balance
Avoid over-simplification that could:
- Reduce code clarity
- Create overly clever solutions
- Make the code harder to debug

## Usage
Operate autonomously after code is written or modified.
```

#### Using Custom Droids

In Factory Droid, you can invoke custom Droids through the Task tool:

```
Please use the code-simplifier droid to simplify this code
```

---

## 8. MCP (Model Context Protocol)

MCP is a standard protocol that allows AI assistants to interact with external tools and data sources.

### 8.1 MCP Concept Introduction

MCP allows you to:
- Connect to databases and query data
- Access API services
- Operate external tools
- Extend AI capabilities

### 8.2 MCP Configuration

Configuration file is located at `~/.factory/mcp.json`:

```json
{
  "mcpServers": {
    "filesystem": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-filesystem", "/path/to/allowed/directory"]
    },
    "github": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-github"],
      "env": {
        "GITHUB_PERSONAL_ACCESS_TOKEN": "your-token-here"
      }
    },
    "postgres": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-postgres"],
      "env": {
        "DATABASE_URL": "postgresql://user:password@localhost:5432/mydb"
      }
    }
  }
}
```

#### Common MCP Servers

| Server            | Purpose             | Package                                 |
| ----------------- | ------------------- | --------------------------------------- |
| `server-filesystem` | File system access  | `@modelcontextprotocol/server-filesystem` |
| `server-github`     | GitHub operations   | `@modelcontextprotocol/server-github`     |
| `server-postgres`   | PostgreSQL database | `@modelcontextprotocol/server-postgres`   |
| `server-sqlite`     | SQLite database     | `@modelcontextprotocol/server-sqlite`     |
| `server-fetch`      | HTTP requests       | `@modelcontextprotocol/server-fetch`      |

---

## 9. Workflow Example

Let's demonstrate the complete Vibe Coding workflow through a practical example.

### Scenario: Creating a REST API Endpoint

#### Step 1: Open Terminal

```bash
# Open project directory in Warp or Kitty
cd ~/projects/my-api
```

#### Step 2: Start Factory Droid

```bash
droid
```

![Start Droid](<!-- IMAGE: Droid startup interface screenshot -->)

#### Step 3: Describe the Task

```
I need to create a user registration REST API endpoint:
- POST /api/users/register
- Accept email and password
- Validate input
- Store password encrypted
- Return JWT token

Please develop using TDD approach.
```

#### Step 4: AI Execution

Droid will:
1. Create `task_plan.md` to plan the task
2. Write test code first
3. Run tests to confirm failure (RED)
4. Write implementation code
5. Run tests to confirm passing (GREEN)
6. Refactor code (REFACTOR)
7. Run verification to confirm completion

#### Step 5: Review Results

```bash
# View generated files
git status

# Run tests
npm test

# View coverage
npm run test:coverage
```

![Workflow Complete](<!-- IMAGE: Complete workflow execution result screenshot -->)

---

## 10. Summary and Resources

### Summary

Through this tutorial, you have learned:

1. ✅ Configure modern terminals (Warp/Kitty)
2. ✅ Beautify shell environment (Oh-My-Zsh + Powerlevel10k)
3. ✅ Install and configure Factory Droid
4. ✅ Choose appropriate LLM models (BYOK)
5. ✅ Use Skills to enhance AI capabilities
6. ✅ Create Custom Droids
7. ✅ Configure MCP extensions

### Related Resources

- **Warp Terminal**: https://www.warp.dev/
- **Kitty Terminal**: https://sw.kovidgoyal.net/kitty/
- **Oh-My-Zsh**: https://ohmyz.sh/
- **Powerlevel10k**: https://github.com/romkatv/powerlevel10k
- **Factory Droid**: https://docs.factory.ai/
- **SWE-Rebench**: https://swe-rebench.com/
- **MCP Protocol**: https://modelcontextprotocol.io/

### Next Steps

- Explore more Skills and Custom Droids
- Try different models based on SWE-Rebench data
- Create custom configurations for your specific workflow
- Join the community to share your experience

---

> 🎉 Congratulations on completing your Vibe Coding environment setup! Start enjoying the fun of AI-assisted programming!

*Last updated: January 2026*
