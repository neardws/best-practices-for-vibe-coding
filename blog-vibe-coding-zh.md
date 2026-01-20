# 我的 Vibe Coding 工作流：从终端到 AI 编程的完整指南

> 本文将带你从零开始搭建一套完整的 Vibe Coding 工作环境，包括终端配置、Shell 美化、AI 编程工具以及进阶技巧。

## 目录

1. [引言](#1-引言)
2. [终端配置](#2-终端配置)
3. [Oh-My-Zsh 配置](#3-oh-my-zsh-配置)
4. [Factory Droid - Vibe Coding 核心工具](#4-factory-droid---vibe-coding-核心工具)
5. [BYOK - 模型选择指南](#5-byok---模型选择指南)
6. [Skills 系统](#6-skills-系统)
7. [Custom Droids](#7-custom-droids)
8. [MCP (Model Context Protocol)](#8-mcp-model-context-protocol)
9. [工作流示例](#9-工作流示例)
10. [总结与资源](#10-总结与资源)

---

## 1. 引言

### 什么是 Vibe Coding？

Vibe Coding 是一种全新的编程方式，通过与 AI 助手进行自然语言对话来完成编程任务。你只需要描述你想要实现的功能，AI 就会帮你编写、调试和优化代码。这种方式让编程变得更加直观和高效。

### 为什么选择这套工具链？

- **现代化终端体验**：Warp 和 Kitty 提供流畅、美观的终端界面
- **高效的 Shell 环境**：Oh-My-Zsh + Powerlevel10k 带来强大的命令行增强
- **智能 AI 编程**：Factory Droid 提供专业级的 AI 编程辅助
- **灵活的模型选择**：BYOK 让你可以使用任何 LLM 模型
- **可扩展的技能系统**：Skills 和 Custom Droids 让 AI 更懂你的工作流

### 目标读者

本教程面向所有对 AI 编程感兴趣的开发者，无论你是刚入门的新手还是经验丰富的老手。每个步骤都有详细说明，跟着做就能完成配置。

---

## 2. 终端配置

一个好的终端是 Vibe Coding 的基础。这里介绍两款优秀的现代终端。

### 2.1 Warp 终端

Warp 是一款现代化的终端，内置 AI 功能，专为开发者设计。

![Warp 终端界面](<!-- IMAGE: Warp 终端主界面截图 -->)

#### 特点

- 🚀 内置 AI 命令建议
- 📝 块状命令输出，便于复制和分享
- 🎨 现代化 UI 设计
- ⚡ 极速启动和响应

#### 安装步骤

**Linux (Debian/Ubuntu):**

```bash
# 下载并安装
wget https://releases.warp.dev/stable/v0.2024.11.12.08.02.stable_01/warp-terminal_0.2024.11.12.08.02.stable.01_amd64.deb
sudo dpkg -i warp-terminal_0.2024.11.12.08.02.stable.01_amd64.deb
```

**macOS:**

```bash
brew install --cask warp
```

![Warp 安装完成](<!-- IMAGE: Warp 安装成功后的欢迎界面 -->)

### 2.2 Kitty 终端（备选方案）

Kitty 是一款基于 GPU 加速的终端模拟器，高度可定制且性能优异。

![Kitty 终端界面](<!-- IMAGE: Kitty 终端主界面截图 -->)

#### 特点

- 🖥️ GPU 渲染，超快速度
- ⚙️ 高度可配置
- 🖼️ 支持图片显示
- 📑 内置多标签和分屏

#### 安装步骤

**Linux (Debian/Ubuntu):**

```bash
sudo apt install kitty
```

**macOS:**

```bash
brew install --cask kitty
```

#### 基础配置

创建或编辑配置文件 `~/.config/kitty/kitty.conf`：

```conf
# 字体配置
font_family      FiraCode Nerd Font
bold_font        auto
italic_font      auto
bold_italic_font auto
font_size        14.0

# 窗口配置
window_padding_width 10
hide_window_decorations yes
background_opacity 0.95

# 颜色主题 - Catppuccin Mocha
foreground              #CDD6F4
background              #1E1E2E
selection_foreground    #1E1E2E
selection_background    #F5E0DC

# 标签栏
tab_bar_edge bottom
tab_bar_style powerline
tab_powerline_style slanted

# 快捷键
map ctrl+shift+t new_tab
map ctrl+shift+q close_tab
map ctrl+shift+right next_tab
map ctrl+shift+left previous_tab

# 滚动
scrollback_lines 10000
wheel_scroll_multiplier 5.0

# 光标
cursor_shape beam
cursor_blink_interval 0.5
```

![Kitty 配置效果](<!-- IMAGE: Kitty 配置完成后的效果截图 -->)

---

## 3. Oh-My-Zsh 配置

Oh-My-Zsh 是一个开源的 Zsh 配置管理框架，提供大量主题和插件。

### 3.1 安装 Oh-My-Zsh

首先确保已安装 Zsh：

```bash
# 检查是否安装
zsh --version

# 如果未安装，在 Ubuntu/Debian 上安装
sudo apt install zsh

# 设置 Zsh 为默认 Shell
chsh -s $(which zsh)
```

安装 Oh-My-Zsh：

```bash
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

![Oh-My-Zsh 安装](<!-- IMAGE: Oh-My-Zsh 安装过程截图 -->)

### 3.2 Powerlevel10k 主题

Powerlevel10k 是最受欢迎的 Zsh 主题之一，提供丰富的信息展示和极快的渲染速度。

#### 安装 Nerd Font

首先需要安装 Nerd Font 以正确显示图标：

```bash
# 下载 FiraCode Nerd Font
mkdir -p ~/.local/share/fonts
cd ~/.local/share/fonts
curl -fLo "FiraCode Nerd Font Regular.ttf" \
  https://github.com/ryanoasis/nerd-fonts/raw/master/patched-fonts/FiraCode/Regular/FiraCodeNerdFont-Regular.ttf

# 刷新字体缓存
fc-cache -fv
```

#### 安装 Powerlevel10k

```bash
git clone --depth=1 https://github.com/romkatv/powerlevel10k.git \
  ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k
```

编辑 `~/.zshrc`，设置主题：

```bash
ZSH_THEME="powerlevel10k/powerlevel10k"
```

重新打开终端后，会自动启动配置向导：

```bash
# 手动启动配置向导
p10k configure
```

![Powerlevel10k 配置向导](<!-- IMAGE: Powerlevel10k 配置向导截图 -->)

### 3.3 插件配置

以下是我推荐的插件配置，每个插件都能显著提升你的命令行体验。

#### 安装第三方插件

```bash
# zsh-autosuggestions - 命令自动补全建议
git clone https://github.com/zsh-users/zsh-autosuggestions \
  ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions

# zsh-syntax-highlighting - 命令语法高亮
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git \
  ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting

# zsh-completions - 额外的命令补全
git clone https://github.com/zsh-users/zsh-completions \
  ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-completions
```

#### 配置插件

编辑 `~/.zshrc`，配置插件列表：

```bash
plugins=(
    git                      # Git 命令别名和状态提示
    sudo                     # 双击 ESC 在命令前添加 sudo
    history                  # 历史命令搜索增强
    extract                  # 通用解压命令，支持各种格式
    z                        # 智能目录跳转
    zsh-autosuggestions      # 根据历史命令自动建议
    zsh-syntax-highlighting  # 命令语法高亮
    zsh-completions          # 额外的命令补全
)
```

应用配置：

```bash
source ~/.zshrc
```

#### 插件功能说明

| 插件                      | 功能        | 使用示例                                 |
| ----------------------- | --------- | ------------------------------------ |
| `git`                     | Git 命令别名  | `gst` = `git status`, `gco` = `git checkout` |
| `sudo`                    | 快速添加 sudo | 双击 `ESC` 在当前命令前添加 sudo                 |
| `history`                 | 历史搜索      | `Ctrl+R` 搜索历史命令                        |
| `extract`                 | 通用解压      | `extract file.tar.gz` 自动识别格式           |
| `z`                       | 智能跳转      | `z project` 跳转到包含 "project" 的常用目录      |
| `zsh-autosuggestions`     | 命令建议      | 输入时显示灰色建议，按 `→` 接受                     |
| `zsh-syntax-highlighting` | 语法高亮      | 正确命令绿色，错误命令红色                        |
| `zsh-completions`         | 额外补全      | 更多命令的 Tab 补全支持                       |

![插件效果展示](<!-- IMAGE: 各插件效果对比截图 -->)

---

## 4. Factory Droid - Vibe Coding 核心工具

Factory Droid 是一款专业的 AI 编程助手，运行在终端中，让你通过自然语言与代码交互。

### 4.1 什么是 Factory Droid

Factory Droid 是 Factory AI 推出的命令行 AI 编程工具，具有以下特点：

- 🤖 强大的代码理解和生成能力
- 📁 直接读写文件系统
- 🔧 执行 Shell 命令
- 🌐 支持多种 LLM 模型
- 🎯 可扩展的 Skills 系统
- 🔗 MCP 协议支持

![Factory Droid 界面](<!-- IMAGE: Factory Droid 运行界面截图 -->)

### 4.2 安装与配置

#### 安装

```bash
# macOS/Linux
curl -fsSL https://app.factory.ai/cli | sh
```

**Linux 用户注意**：确保已安装 `xdg-utils` 以获得完整功能：`sudo apt-get install xdg-utils`

#### 启动

```bash
# 进入项目目录
cd /path/to/your/project

# 启动交互式会话
droid
```

首次运行时会引导你通过浏览器登录 Factory 账户。

#### 配置文件

配置文件位于 `~/.factory/settings.json`，可通过 `/settings` 命令交互式修改。

#### 会话默认设置

在 `settings.json` 中配置默认行为：

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

| 配置项                     | 可选值                                            | 说明       |
| ----------------------- | ---------------------------------------------- | -------- |
| `model`                   | opus, sonnet, gpt-5.1, gpt-5.2, haiku 等        | 默认 AI 模型 |
| `reasoningEffort`         | off, none, low, medium, high                   | 推理深度     |
| `autonomyMode`            | normal, spec, auto-low, auto-medium, auto-high | 自主模式     |
| `specModeReasoningEffort` | off, none, low, medium, high                   | 规范模式推理   |

### 4.3 Hooks 配置

Hooks 允许你在特定事件发生时自动执行操作，极大增强工作流。

编辑 `~/.factory/settings.json`：

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

#### Hooks 类型说明

| Hook 类型      | 触发时机  | 用途          |
| ------------ | ----- | ----------- |
| `SessionStart` | 会话开始时 | 初始化提示、加载上下文 |
| `PreToolUse`   | 使用工具前 | 检查状态、读取计划   |
| `PostToolUse`  | 使用工具后 | 更新状态、格式化文件  |
| `Stop`         | 会话结束时 | 清理、总结       |

### 4.4 基础操作

#### 快捷键

| 快捷键         | 功能                     |
| ----------- | ---------------------- |
| `Enter`       | 发送消息                   |
| `Shift+Enter` | 换行（多行输入）               |
| `Shift+Tab`   | 切换模式（Normal/Spec/Auto） |
| `!`           | 切换 Bash 模式（输入框为空时）     |
| `Esc`         | 退出 Bash 模式 / 中断操作      |
| `?`           | 查看所有快捷键                |
| `Ctrl+C`      | 退出 Droid               |

#### 基本交互流程

1. 输入你的任务描述
2. Droid 分析代码库并制定计划
3. 审查 Droid 提出的更改
4. 接受或拒绝修改
5. 继续迭代直到任务完成

### 4.5 Slash 命令

在 Droid 中输入 `/` 开头的命令来执行特定操作：

| 命令        | 说明            |
| --------- | ------------- |
| `/settings` | 配置 Droid 设置   |
| `/model`    | 切换 AI 模型      |
| `/review`   | 启动 AI 代码审查工作流 |
| `/mcp`      | 管理 MCP 服务器    |
| `/sessions` | 列出和选择历史会话     |
| `/droids`   | 管理自定义 Droids  |
| `/skills`   | 管理和调用 Skills  |
| `/hooks`    | 管理生命周期 Hooks  |
| `/cost`     | 查看 Token 使用统计 |
| `/new`      | 开始新会话         |
| `/help`     | 查看所有可用命令      |

### 4.6 Specification Mode（规范模式）

规范模式是 Droid 的核心功能之一，遵循「先规划、后执行」的原则。

#### 激活方式

按 **Shift+Tab** 切换到 Spec 模式。

#### 工作流程

1. **描述功能** - 用 4-6 句话描述你想要实现的功能
2. **Droid 生成规范** - 自动分析代码库，生成详细的实现计划
3. **审查和批准** - 你可以修改或批准计划
4. **实现** - 批准后 Droid 开始执行，每个修改都会展示给你审查

#### 安全保证

- 分析阶段只读，不会修改任何文件
- 所有更改在批准后才会执行
- 完整可见的实现计划

#### 批准选项

| 选项                      | 说明                        |
| ----------------------- | ------------------------- |
| Proceed (手动)            | 批准计划，保持手动确认每个操作           |
| Proceed + Auto (Low)    | 批准计划，自动执行文件编辑和只读命令        |
| Proceed + Auto (Medium) | + 自动执行可逆命令（npm install 等） |
| Proceed + Auto (High)   | + 自动执行高风险命令（git push 等）   |
| Keep iterating          | 继续修改规范                    |

### 4.7 Auto-Run Mode（自动运行模式）

Auto-Run 模式让你可以控制 Droid 的自主执行级别。

| 级别            | 自动执行的操作         | 示例                              |
| ------------- | --------------- | ------------------------------- |
| Auto (Low)    | 文件编辑、只读命令       | ls, git status, rg              |
| Auto (Medium) | + 可逆的工作区修改      | npm install, git commit, mv, cp |
| Auto (High)   | + 高风险命令（未明确禁止的） | git push, docker, 数据库迁移         |

#### 切换方式

- 按 **Shift+Tab** 循环切换：Normal → Spec → Auto (Low) → Auto (Medium) → Auto (High)
- 或在 `/settings` 中设置默认级别

#### 安全机制

即使在 Auto (High) 模式下，以下操作仍需确认：
- 危险命令（如 `rm -rf /`）
- 命令替换（`$(...)` 或反引号）
- CLI 安全检查标记的操作

### 4.8 Bash Mode

Bash 模式让你可以直接在 Droid 中执行 Shell 命令，无需 AI 解释。

#### 使用方法

1. 在输入框为空时按 `!` 进入 Bash 模式
2. 提示符从 `>` 变为 `$`
3. 输入任何 Shell 命令并按 Enter 执行
4. 按 `Esc` 返回 AI 对话模式

#### 适用场景

- 快速检查 `git status`
- 运行 `npm test` 或 `make build`
- 查看文件内容或目录结构

### 4.9 定价方案

Factory 通过标准 Token（Standard Tokens）计量使用量。缓存 Token 按 1/10 计费（10 个缓存 Token = 1 个标准 Token）。

#### 订阅方案

| 方案    | 标准 Token / 月             | 价格 / 月 |
| ----- | ------------------------ | ------ |
| **Free**  | BYOK（自带 API Key）         | $0     |
| **Pro**   | 1000 万 (+1000 万奖励 Token) | $20    |
| **Max**   | 1 亿 (+1 亿奖励 Token)       | $200   |
| **Ultra** | 10 亿 (+10 亿奖励 Token)     | $2,000 |

超额使用按 **$2.70 / 百万标准 Token** 计费。

#### 模型计费乘数

不同模型有不同的乘数来计算标准 Token 使用量：

| 模型                | Model ID                   | 乘数    |
| ----------------- | -------------------------- | ----- |
| Gemini 3 Flash    | `gemini-3-flash-preview`     | 0.2×  |
| Droid Core        | `glm-4.6`                    | 0.25× |
| Claude Haiku 4.5  | `claude-haiku-4-5-20251001`  | 0.4×  |
| GPT-5.1           | `gpt-5.1`                    | 0.5×  |
| GPT-5.1-Codex     | `gpt-5.1-codex`              | 0.5×  |
| GPT-5.1-Codex-Max | `gpt-5.1-codex-max`          | 0.5×  |
| GPT-5.2           | `gpt-5.2`                    | 0.7×  |
| Gemini 3 Pro      | `gemini-3-pro-preview`       | 0.8×  |
| Claude Sonnet 4.5 | `claude-sonnet-4-5-20250929` | 1.2×  |
| Claude Opus 4.5   | `claude-opus-4-5-20251101`   | 2×    |

#### 使用建议

- **Free 方案**：适合已有 API Key 的用户，无月费
- **Pro 方案**：适合个人开发者日常使用，性价比高
- **缓存优势**：Factory 的缓存机制可显著降低实际 Token 消耗，通常有 4-8 倍的缓存命中率

---

## 5. BYOK - 模型选择指南

BYOK（Bring Your Own Key）让你可以使用自己的 API Key 来访问各种 LLM 模型。

### 5.1 什么是 BYOK

BYOK 允许你：
- 使用自己的 API Key 访问模型
- 选择最适合你需求的模型
- 控制成本和使用量
- 使用本地部署的模型

### 5.2 如何选择模型 - SWE-Rebench 排行榜

[SWE-Rebench](https://swe-rebench.com/) 是一个持续更新的软件工程 LLM 基准测试排行榜，帮助你了解各模型在实际编程任务中的表现。

![SWE-Rebench 排行榜](<!-- IMAGE: SWE-Rebench 网站截图 -->)

#### 关键指标解读

| 指标                 | 含义                | 重要性        |
| ------------------ | ----------------- | ---------- |
| **Resolved Rate**      | 成功解决问题的比例         | 最重要，反映模型能力 |
| **Pass@5**             | 5 次尝试中至少成功 1 次的比例 | 反映模型稳定性    |
| **Cost per Problem**   | 每个问题的平均成本         | 影响使用成本     |
| **Tokens per Problem** | 每个问题消耗的 token 数   | 反映效率       |

### 5.3 推荐模型（2026年1月数据）

根据最新的 SWE-Rebench 数据，以下是不同场景的模型推荐：

#### 顶级性能

| 模型                     | Resolved Rate | Pass@5 | Cost/Problem | 特点              |
| ---------------------- | ------------- | ------ | ------------ | --------------- |
| **Claude Opus 4.5**        | 63.3%         | 79.2%  | $1.22        | 最高性能，复杂任务首选     |
| **GPT-5.2 xhigh**          | 61.5%         | 70.8%  | $1.46        | OpenAI 最强，推理能力强 |
| **Gemini 3 Flash Preview** | 60.0%         | 72.9%  | $0.29        | 性价比极高           |

#### 性价比之选

| 模型                     | Resolved Rate | Pass@5 | Cost/Problem | 特点      |
| ---------------------- | ------------- | ------ | ------------ | ------- |
| **Gemini 3 Flash Preview** | 60.0%         | 72.9%  | $0.29        | 🏆 性价比之王 |
| **GPT-5.2 medium**         | 59.4%         | 70.8%  | $0.86        | 平衡性能与成本 |
| **Claude Sonnet 4.5**      | 57.5%         | 75.0%  | $0.98        | 日常任务首选  |

#### 开源模型

| 模型               | Resolved Rate | Pass@5 | Cost/Problem | 特点     |
| ---------------- | ------------- | ------ | ------------ | ------ |
| **GLM-4.7**          | 51.3%         | 66.7%  | $0.40        | 🏆 开源最强 |
| **DeepSeek-V3.2**    | 48.5%         | 68.8%  | $0.25        | 可本地部署  |
| **Kimi K2 Thinking** | 40.5%         | 60.4%  | $0.48        | 国产优秀选择 |

#### 预算友好

| 模型               | Resolved Rate | Pass@5 | Cost/Problem | 特点     |
| ---------------- | ------------- | ------ | ------------ | ------ |
| **Grok Code Fast 1** | 35.9%         | 54.2%  | $0.08        | 最便宜    |
| **Devstral-2-123B**  | 36.6%         | 59.6%  | $0.09        | 开源可自托管 |
| **MiniMax M2.1**     | 37.3%         | 58.3%  | $0.10        | 缓存友好   |

### 5.4 自定义模型配置

在 `~/.factory/settings.json` 中配置自定义模型：

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

#### 配置参数说明

| 参数              | 必填  | 说明                                                 |
| --------------- | --- | -------------------------------------------------- |
| `model`           | 是   | 模型名称，发送给 API 的 model 参数                            |
| `id`              | 否   | 唯一标识符，格式为 `custom:名称`，用于在 Droid 中选择模型                |
| `displayName`     | 否   | 在 UI 中显示的名称，便于识别                                   |
| `baseUrl`         | 是   | API 端点地址，不同服务有不同地址                                 |
| `apiKey`          | 是   | API 密钥，本地服务可填 `not-needed`                           |
| `provider`        | 是   | 提供商类型：`openai`、`anthropic`、`generic-chat-completion-api` |
| `noImageSupport`  | 否   | 是否禁用图片支持，默认 `false`                                  |
| `maxOutputTokens` | 否   | 最大输出 Token 数，本地模型建议设置                              |

#### 常用 baseUrl 参考

**海外服务：**

| 服务            | baseUrl                                           | 说明               |
| ------------- | ------------------------------------------------- | ---------------- |
| OpenAI        | `https://api.openai.com/v1`                         | OpenAI 官方 API    |
| Anthropic     | `https://api.anthropic.com/v1`                      | Anthropic 官方 API |
| Google Gemini | `https://generativelanguage.googleapis.com/v1beta/` | Google AI Studio |
| OpenRouter    | `https://openrouter.ai/api/v1`                      | 多模型聚合平台          |
| Groq          | `https://api.groq.com/openai/v1`                    | 超快推理（LPU）        |
| Fireworks AI  | `https://api.fireworks.ai/inference/v1`             | 高性能开源模型推理        |
| DeepInfra     | `https://api.deepinfra.com/v1/openai`               | 经济型开源模型推理        |
| Baseten       | `https://inference.baseten.co/v1`                   | 企业级模型部署          |
| Hugging Face  | `https://router.huggingface.co/v1`                  | HF 推理路由          |

**国内服务：**

| 服务              | baseUrl                                           | 说明              |
| --------------- | ------------------------------------------------- | --------------- |
| DeepSeek        | `https://api.deepseek.com/v1`                       | DeepSeek 官方 API |
| 智谱 AI (GLM)     | `https://open.bigmodel.cn/api/paas/v4`              | GLM 系列模型        |
| 阿里通义千问          | `https://dashscope.aliyuncs.com/compatible-mode/v1` | Qwen 系列模型       |
| Moonshot (Kimi) | `https://api.moonshot.cn/v1`                        | Kimi 系列模型       |
| 百度千帆            | `https://aip.baidubce.com`                          | 文心一言            |
| 字节豆包            | `https://ark.cn-beijing.volces.com/api/v3`          | 豆包大模型           |
| SiliconFlow     | `https://api.siliconflow.cn/v1`                     | 国内模型聚合平台        |

**本地部署：**

| 服务         | baseUrl                    | 说明       |
| ---------- | -------------------------- | -------- |
| Ollama 本地  | `http://localhost:11434/v1`  | 本地模型部署   |
| vLLM       | `http://localhost:8000/v1`   | 高性能本地推理  |
| LM Studio  | `http://localhost:1234/v1`   | 桌面端本地模型  |
| LiteLLM 代理 | `http://your-proxy:8000/v1`  | API 代理聚合 |
| OneAPI     | `http://your-oneapi:3000/v1` | 国内常用代理聚合 |

#### 使用本地代理

如果你使用代理服务（如 LiteLLM、OneAPI 等），配置如下：

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

## 6. Skills 系统

Skills 是 Anthropic 于 2025 年 10 月推出的 Claude Agent Skills 系统，Factory Droid 完整支持该系统。Skills 是可组合、可移植的指令集，为 AI 提供特定领域的专业知识和工作流。

### 6.1 什么是 Skills

Skills 是 Anthropic 为 Claude 设计的一套可扩展能力系统。本质上，Skill 是一个包含指令、脚本和资源的文件夹，Claude 可以在执行相关任务时自动加载和使用。

#### 核心特性

| 特性  | 说明                                          |
| --- | ------------------------------------------- |
| 可组合 | 多个 Skills 可以堆叠使用，Claude 自动识别和协调             |
| 可移植 | 一次构建，可在 Claude Code、Factory Droid、API 等多处使用 |
| 高效  | Claude 仅加载当前任务所需的信息，保持响应速度                  |
| 强大  | Skills 可包含可执行代码，处理需要高可靠性的任务                 |

#### Skills 的作用

- 📋 提供特定领域的最佳实践
- 🔄 定义标准化的工作流程
- 📝 包含模板和检查清单
- 🎯 确保输出质量和一致性

### 6.2 推荐 Skills

#### planning-with-files - 复杂任务规划

适用于需要多步骤完成的复杂任务，采用 Manus 风格的文件化规划。

**核心理念：**
```
上下文窗口 = 内存（易失、有限）
文件系统 = 磁盘（持久、无限）
→ 重要的东西都写到文件里
```

**使用方法：**
```bash
# 在项目目录创建三个规划文件
task_plan.md   # 任务计划和进度
findings.md    # 研究发现
progress.md    # 会话日志
```

**task_plan.md 示例：**
```markdown
# 任务计划：实现用户认证功能

## 目标
实现完整的用户认证系统，包括注册、登录、注销功能。

## 阶段
- [x] Phase 1: 数据库模型设计
- [ ] Phase 2: API 端点实现
- [ ] Phase 3: 前端表单
- [ ] Phase 4: 测试

## 当前状态
正在进行 Phase 2

## 遇到的问题
| 问题       | 尝试  | 解决方案             |
| -------- | --- | ---------------- |
| JWT 过期处理 | 1   | 添加 refresh token |
```

#### brainstorming - 创意头脑风暴

在开始任何创造性工作之前使用，帮助明确需求和设计。

**工作流程：**
1. 了解当前项目上下文
2. 一次问一个问题来细化想法
3. 提出 2-3 个不同方案及其权衡
4. 分段展示设计，每段确认后继续

#### test-driven-development - TDD 开发

强制执行测试驱动开发流程。

**核心原则：**
```
没有失败的测试，就没有生产代码
```

**Red-Green-Refactor 循环：**
1. **RED** - 编写一个失败的测试
2. **验证 RED** - 确认测试失败且原因正确
3. **GREEN** - 编写最少代码使测试通过
4. **验证 GREEN** - 确认测试通过
5. **REFACTOR** - 重构代码，保持测试通过

#### verification-before-completion - 完成前验证

防止在没有验证的情况下声称工作完成。

**核心原则：**
```
没有验证证据，不做完成声明
```

**验证检查清单：**
- [ ] 运行测试命令，确认 0 失败
- [ ] 运行 lint 命令，确认 0 错误
- [ ] 运行 build 命令，确认成功
- [ ] 逐条检查需求是否满足

#### code-simplifier - 代码简化

在编写或修改代码后自动应用，简化和优化代码。

**优化方向：**
- 减少不必要的复杂度和嵌套
- 消除冗余代码
- 改进命名
- 遵循项目编码规范

### 6.3 Skills 安装与配置

#### 安装位置

Skills 可以安装在两个位置：

| 位置                    | 作用域       | 说明           |
| --------------------- | --------- | ------------ |
| `~/.factory/skills/`    | 个人 Skills | 跨项目使用，仅对你可见  |
| `<项目>/.factory/skills/` | 项目 Skills | 与团队共享，跟随项目仓库 |

#### 从 droid-skills 仓库安装

推荐从 [droid-skills](https://github.com/neardws/droid-skills) 仓库安装预配置的 Skills：

```bash
# 克隆仓库
git clone https://github.com/neardws/droid-skills.git
cd droid-skills

# 安装为个人 Skill（跨项目使用）
cp -r skills/planning-with-files ~/.factory/skills/
cp -r skills/md-table-formatter ~/.factory/skills/

# 安装 superpowers 套件（14 个 Skills）
cp -r skills/superpowers/* ~/.factory/skills/

# 或安装为项目 Skill（与团队共享）
cp -r skills/planning-with-files <你的项目>/.factory/skills/
```

重启 `droid` 以加载新安装的 Skills。

#### 可用 Skills 列表

| Skill               | 描述                |
| ------------------- | ----------------- |
| planning-with-files | Manus 风格的文件化任务规划  |
| md-table-formatter  | 自动格式化 Markdown 表格 |
| superpowers (14 个)  | 完整开发工作流套件         |

**superpowers 套件包含：**
- brainstorming - 交互式设计头脑风暴
- writing-plans - 详细实现计划编写
- executing-plans - 带检查点的批量执行
- test-driven-development - RED-GREEN-REFACTOR 循环
- systematic-debugging - 四阶段根因分析
- verification-before-completion - 完成前验证
- requesting-code-review - 代码审查请求
- receiving-code-review - 响应审查反馈
- 等等...

#### 创建自定义 Skill

创建 `~/.factory/skills/my-skill/SKILL.md`：

```markdown
---
name: my-skill
description: 这是我的自定义 skill 描述
---

# My Skill

## Overview
描述这个 skill 的用途...

## When to Use
什么时候使用这个 skill...

## Process
具体的工作流程...
```

#### Skills 相关资源

| 资源                      | 说明                    | 链接                                                    |
| ----------------------- | --------------------- | ----------------------------------------------------- |
| Skills Manager Client   | Skills 管理客户端工具        | https://github.com/buzhangsan/skills-manager-client   |
| Superpowers             | 完整开发工作流 Skills 套件     | https://github.com/obra/superpowers                   |
| Planning With Files     | Manus 风格文件化规划 Skill   | https://github.com/OthmanAdi/planning-with-files      |
| Agent Skills            | 社区 Skills 集合          | https://github.com/agentskills/agentskills            |
| Awesome Claude Skills   | Claude Skills 精选列表    | https://github.com/travisvn/awesome-claude-skills     |
| Claude Plugins Official | Anthropic 官方插件/Skills | https://github.com/anthropics/claude-plugins-official |

---

## 7. 高级定制功能

Factory Droid 提供多种定制功能，让你可以根据团队和项目需求扩展 AI 的能力。

### 7.1 AGENTS.md - AI 代理的说明书

AGENTS.md 是一个 Markdown 文件，作为 AI 编程代理的「简报包」，告诉 AI 如何构建、测试和运行你的项目。

#### 为什么需要 AGENTS.md

| 文件        | 目的         | 受众      |
| --------- | ---------- | ------- |
| README.md | 快速入门、项目描述  | 人类开发者   |
| AGENTS.md | 构建步骤、测试、约定 | AI 编程代理 |

#### 文件位置与发现

代理按以下顺序查找 AGENTS.md（首个匹配生效）：

1. 当前工作目录的 `./AGENTS.md`
2. 向上查找到仓库根目录
3. 子文件夹中的 `AGENTS.md`
4. 个人覆盖：`~/.factory/AGENTS.md`

#### 常用章节

| 章节            | 内容                  |
| ------------- | ------------------- |
| Build & Test  | 编译和运行测试套件的确切命令      |
| Architecture  | 主要模块和数据流的一段话总结      |
| Security      | API 密钥、端点、认证流程、敏感数据 |
| Git Workflows | 分支策略、提交约定、PR 要求     |
| Conventions   | 文件夹结构、命名模式、代码风格     |

#### 示例

```markdown
# MyProject

## Core Commands

• Type-check and lint: `pnpm check`
• Run full test suite: `pnpm test --run --no-color`
• Start dev servers: `pnpm dev`
• Build for production: `pnpm build`

## Project Layout

├─ client/ → React + Vite frontend
├─ server/ → Express backend

## Development Patterns

• TypeScript strict mode, single quotes, trailing commas
• Tests first when fixing logic bugs
• Never introduce new runtime deps without PR description

## Git Workflow

1. Branch from `main`: `feature/<slug>` or `bugfix/<slug>`
2. Run `pnpm check` locally before committing
3. Keep commits atomic: `feat: …`, `test: …`
```

#### 最佳实践

- **保持简短** - 目标 ≤150 行，过长会拖慢代理
- **使用具体命令** - 用反引号包裹命令，代理可直接复制
- **随代码更新** - 构建步骤变更时同步更新 AGENTS.md
- **单一信息源** - 链接到 README 或设计文档，而不是复制粘贴

#### 跨代理兼容

AGENTS.md 兼容多种 AI 编程工具：
- Factory Droid
- Cursor
- Aider
- Gemini CLI
- Codex
- Zed
- 等等...

---

### 7.2 Custom Slash Commands - 自定义斜杠命令

Custom Slash Commands 将可重复的提示或设置步骤转换为 `/快捷命令`。Droid 扫描 `.factory/commands` 文件夹，将每个文件转换为命令。

#### 命令发现与命名

| 作用域 | 位置                     | 说明           |
| --- | ---------------------- | ------------ |
| 工作区 | `<项目>/.factory/commands` | 项目特定命令，与团队共享 |
| 个人  | `~/.factory/commands`    | 私有或跨项目快捷命令   |

- 仅注册 Markdown (`*.md`) 文件和带 shebang (`#!`) 的文件
- 文件名自动转换为 slug：`Code Review.md` → `/code-review`
- 使用 `/commands` 打开命令管理 UI

#### Markdown 命令

Markdown 文件渲染为系统通知，作为 Droid 下一轮对话的种子。

```markdown
---
description: 请求代码审查
argument-hint: <分支名>
---

请审查 `$ARGUMENTS` 并总结任何合并阻塞、测试缺口和风险区域。

- 突出安全或性能问题
- 建议后续任务和负责人
- 列出需要关注的文件
```

| 前置配置          | 用途                       |
| ------------- | ------------------------ |
| `description`   | 覆盖斜杠建议中显示的摘要             |
| `argument-hint` | 添加内联用法提示，如 `/review <分支名>` |

`$ARGUMENTS` 扩展为命令名后输入的所有内容。

#### 可执行命令

可执行文件必须以有效的 shebang 开头：

```bash
#!/usr/bin/env bash
set -euo pipefail

echo "Preparing $1"
npm install
npm run lint
echo "Ready to deploy $1"
```

保存为 `deploy.sh` 后，显示为 `/deploy`。使用 `/deploy feature/login` 传递参数。

#### 示例命令

**每日站会助手：**

```markdown
---
description: 为站会总结进度
---

使用以下格式草拟站会更新：

- **昨天：** 主要成果、合并的 PR、清除的阻塞
- **今天：** 计划的工作项和目标
- **风险：** 任何可能延迟的事项、需要的支持、跨团队依赖

保持三个简短的要点部分。
```

**回归冒烟测试：**

```bash
#!/usr/bin/env bash
set -euo pipefail

target=${1:-"src"}

echo "Running lint + unit tests for $target"
npm run lint -- "$target"
npm test -- --runTestsByPath "$target"

echo "Done"
```

---

### 7.3 Custom Droids - 自定义子代理

Custom Droids 是可复用的子代理（Subagent），每个 Droid 携带自己的系统提示、模型偏好和工具策略，可以处理特定任务如代码审查、安全检查或研究，无需重复输入指令。

#### 什么是 Custom Droids

Custom Droids 以 `.md` 文件形式存放在 `.factory/droids/` 或 `~/.factory/droids/` 目录下。CLI 扫描这些文件夹，验证每个定义，并作为 **Task** 工具的 `subagent_type` 目标公开，让主助手可以在会话中启动专用辅助程序。

#### Custom Droids 与 Skills 的区别

| 特性   | Skills     | Custom Droids |
| ---- | ---------- | ------------- |
| 本质   | 知识和指导      | 独立的专门化 AI 代理  |
| 运行方式 | 增强主 AI 的能力 | 作为子代理独立运行     |
| 上下文  | 共享主会话上下文   | 独立的上下文窗口      |
| 工具访问 | 使用主 AI 的工具 | 可限制特定工具集      |
| 模型选择 | 使用主 AI 的模型 | 可指定不同模型       |

#### 存储位置

| 位置                    | 作用域       | 说明           |
| --------------------- | --------- | ------------ |
| `<项目>/.factory/droids/` | 项目 Droids | 与团队共享，可版本控制  |
| `~/.factory/droids/`    | 个人 Droids | 跨工作区使用，仅对你可见 |

**注意**：当名称相同时，项目定义会覆盖个人定义。

#### 为什么使用 Custom Droids

- **更快的任务委派** - 将复杂检查清单编码一次，通过单个工具调用复用
- **更严格的安全性** - 将代理限制为只读、仅编辑或特定工具集
- **上下文隔离** - 每个子代理使用新的上下文窗口，避免提示膨胀
- **可重复的流程** - 将团队特定的审查、测试或发布检查编码为可版本控制的代码

#### 创建自定义 Droid

**方法一：使用 UI 向导**

1. 运行 `/droids` 打开 Droids 菜单
2. 选择 **Create a new Droid**
3. 选择存储位置（项目或个人）
4. 描述 Droid 应该做什么
5. 生成或手动编辑系统提示
6. 确认标识符、模型和工具

**方法二：手动创建文件**

创建 `~/.factory/droids/code-reviewer.md`：

```markdown
---
name: code-reviewer
description: 检查 diff 的正确性风险的专注审查者
model: inherit
tools: ["Read", "LS", "Grep", "Glob"]
---

你是团队的高级审查者。检查父代理分享的 diff：

- 标记正确性、安全性和迁移风险
- 如果需要更改，列出有针对性的后续任务
- 确认合并前需要的测试或手动验证

回复格式：
Summary: <一行总结>
Findings:
- <要点>
- <要点>
```

#### 配置字段说明

| 字段              | 说明                                                    |
| --------------- | ----------------------------------------------------- |
| `name`            | 必填。小写字母、数字、`-`、`_`。决定 `subagent_type` 值和文件名                 |
| `description`     | 可选。在 UI 列表中显示，≤500 字符                                 |
| `model`           | `inherit`（使用父会话模型）或指定模型 ID，如 `claude-sonnet-4-5-20250929` |
| `reasoningEffort` | 可选。设置推理深度：`low`、`medium`、`high`                             |
| `tools`           | 省略表示所有工具；使用类别字符串或工具 ID 数组                             |

#### 工具类别

| 类别        | 工具 ID                    | 用途         |
| --------- | ------------------------ | ---------- |
| `read-only` | `Read`, `LS`, `Grep`, `Glob`     | 安全分析和文件探索  |
| `edit`      | `Create`, `Edit`, `ApplyPatch` | 代码生成和修改    |
| `execute`   | `Execute`                  | Shell 命令执行 |
| `web`       | `WebSearch`, `FetchUrl`      | 网络研究和内容    |
| `mcp`       | 动态填充                     | MCP 工具     |

#### 使用 Custom Droids

**通过自然语言调用：**

```
请使用 code-reviewer subagent 审查这个 diff
```

```
运行 security-sweeper droid 检查最近编辑的文件
```

**通过 Task 工具调用：**

Droid 可以自主调用自定义 Droids，或者你可以直接请求。

#### 从 Claude Code 导入代理

如果你已经在 Claude Code 中创建了代理，可以直接导入：

1. 运行 `/droids` 打开 Droids 菜单
2. 按 **I** 启动导入流程
3. CLI 扫描 Claude Code 代理目录：
   - 项目范围：`<项目>/.claude/agents/`
   - 个人范围：`~/.claude/agents/`
4. 使用 **Space** 切换选择，**A** 全选
5. 按 **Enter** 导入

导入时会自动进行模型映射：
- `sonnet` → 第一个可用的 Sonnet 模型
- `haiku` → 第一个可用的 Haiku 模型
- `opus` → 第一个可用的 Opus 模型

#### 示例 Droids

**安全扫描器：**

```markdown
---
name: security-sweeper
description: 在最近编辑的文件中查找不安全模式
model: inherit
tools: ["Read", "Grep", "WebSearch"]
---

调查提示中引用的文件的安全问题：

- 识别注入、不安全传输、权限提升或密钥暴露
- 建议具体的缓解措施
- 在有帮助时链接到相关 CWE 或内部标准

回复格式：
Summary: <标题>
Findings:
- <文件>: <问题>
Mitigations:
- <建议>
```

**任务协调器：**

```markdown
---
name: task-coordinator
description: 协调多步骤任务并实时更新进度
model: inherit
tools: ["Read", "Edit", "Execute"]
---

你是任务协调器。将目标分解为可操作的步骤：

1. 使用 TodoWrite 创建和更新任务列表
2. 对于每个任务，读取相关文件并根据需要执行命令
3. 使用 TodoWrite 更新实时报告进度

保持任务列表状态更新（pending、in_progress、completed）。
```

#### 最佳实践

| 实践      | 说明                                 |
| ------- | ---------------------------------- |
| 策略性选择模型 | 简单任务用小模型降低成本，复杂推理用大模型              |
| 限制工具访问  | 使用显式工具列表防止意外的 shell 命令或危险操作        |
| 结构化输出   | 组织提示以输出 `Summary:` 和 `Findings:` 等部分   |
| 版本控制共享  | 将 `.factory/droids/*.md` 提交到仓库，与团队共享 |
| 利用实时更新  | Task 工具现在流式传输实时进度，显示工具调用和结果        |

---

## 8. MCP (Model Context Protocol)

MCP（Model Context Protocol）是由 Anthropic 开源的标准协议，用于连接 AI 应用与外部系统。可以把 MCP 想象成 AI 应用的 USB-C 接口——就像 USB-C 为电子设备提供标准化连接方式一样，MCP 为 AI 应用提供了连接外部系统的标准化方式。

### 8.1 MCP 概念介绍

#### MCP 能做什么

- 🗓️ AI 助手可以访问你的 Google Calendar 和 Notion，提供更个性化的服务
- 🎨 Claude Code 可以根据 Figma 设计稿生成完整的 Web 应用
- 🏢 企业聊天机器人可以连接多个数据库，让用户通过对话分析数据
- 🖨️ AI 模型可以在 Blender 中创建 3D 设计并用 3D 打印机打印

#### MCP 的核心组件

| 组件        | 说明                    |
| --------- | --------------------- |
| Tools     | 可执行的函数，如搜索、计算、API 调用等 |
| Resources | 数据源，如文件、数据库记录等        |
| Prompts   | 预定义的提示模板，用于特定工作流      |

### 8.2 MCP 配置

配置文件位于 `~/.factory/mcp.json`：

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

### 8.3 使用 Smithery 安装 MCP Servers

[Smithery](https://smithery.ai/) 是目前最大的 MCP Server 市场，提供 3700+ 个 MCP 应用。推荐使用 Smithery 来发现和安装 MCP Servers。

#### Smithery 的优势

| 特性   | 说明                           |
| ---- | ---------------------------- |
| 认证   | 内置 OAuth，无需自己实现认证流程          |
| 可观测  | 查看工具使用情况，优化 AI 体验            |
| 分发   | 发布到 Smithery，可从任何 AI 客户端连接   |
| 协议网关 | Smithery 保持与 MCP 规范同步，无需自己维护 |

#### 热门 MCP Servers

| Server          | 用途         | 连接数    |
| --------------- | ---------- | ------ |
| Gmail           | 邮件管理       | 10.13k |
| Linkup          | 网络搜索       | 9.53k  |
| Google Super    | Google 全家桶 | 6.73k  |
| GitHub          | 代码仓库管理     | 5.98k  |
| Google Calendar | 日程管理       | 5.63k  |

### 8.4 常用 MCP Servers

#### 官方 Servers

| Server              | 用途             | 安装                                        |
| ------------------- | -------------- | ----------------------------------------- |
| `server-filesystem`   | 文件系统访问         | `@modelcontextprotocol/server-filesystem`   |
| `server-github`       | GitHub 操作      | `@modelcontextprotocol/server-github`       |
| `server-postgres`     | PostgreSQL 数据库 | `@modelcontextprotocol/server-postgres`     |
| `server-sqlite`       | SQLite 数据库     | `@modelcontextprotocol/server-sqlite`       |
| `server-fetch`        | HTTP 请求        | `@modelcontextprotocol/server-fetch`        |
| `server-puppeteer`    | 浏览器自动化         | `@modelcontextprotocol/server-puppeteer`    |
| `server-brave-search` | Brave 搜索       | `@modelcontextprotocol/server-brave-search` |

#### 社区 Servers

| Server  | 用途        | 来源       |
| ------- | --------- | -------- |
| Notion  | 知识库管理     | Smithery |
| Slack   | 团队通讯      | Smithery |
| Linear  | 项目管理      | Smithery |
| Figma   | 设计协作      | Smithery |
| MongoDB | NoSQL 数据库 | Smithery |

### 8.5 MCP 相关资源

| 资源                  | 说明                   | 链接                                              |
| ------------------- | -------------------- | ----------------------------------------------- |
| MCP 官方文档            | 协议规范和开发指南            | https://modelcontextprotocol.io/                |
| Smithery            | MCP Server 市场（推荐）    | https://smithery.ai/                            |
| MCP 官方注册表           | 官方 MCP Server 注册表    | https://registry.modelcontextprotocol.io/       |
| Awesome MCP Servers | MCP Servers 精选列表     | https://github.com/punkpeye/awesome-mcp-servers |
| MCP Servers 官方仓库    | Anthropic 官方 Servers | https://github.com/modelcontextprotocol/servers |

---

## 9. 工作流示例

让我们通过一个完整的例子来展示 Vibe Coding 工作流。

### 场景：创建一个 REST API 端点

#### 步骤 1：打开终端

```bash
# 在 Warp 或 Kitty 中打开项目目录
cd ~/projects/my-api
```

#### 步骤 2：启动 Factory Droid

```bash
droid
```

![启动 Droid](<!-- IMAGE: Droid 启动界面截图 -->)

#### 步骤 3：描述任务

```
我需要创建一个用户注册的 REST API 端点：
- POST /api/users/register
- 接收 email 和 password
- 验证输入
- 密码加密存储
- 返回 JWT token

请使用 TDD 方式开发。
```

#### 步骤 4：AI 执行

Droid 会：
1. 创建 `task_plan.md` 规划任务
2. 先编写测试代码
3. 运行测试确认失败（RED）
4. 编写实现代码
5. 运行测试确认通过（GREEN）
6. 重构代码（REFACTOR）
7. 运行验证确认完成

#### 步骤 5：审查结果

```bash
# 查看生成的文件
git status

# 运行测试
npm test

# 查看覆盖率
npm run test:coverage
```

![工作流完成](<!-- IMAGE: 完整工作流执行结果截图 -->)

---

## 10. 总结与资源

### 总结

通过本教程，你已经学会了：

1. ✅ 配置现代化终端（Warp/Kitty）
2. ✅ 美化 Shell 环境（Oh-My-Zsh + Powerlevel10k）
3. ✅ 安装和配置 Factory Droid
4. ✅ 选择合适的 LLM 模型（BYOK）
5. ✅ 使用 Skills 增强 AI 能力
6. ✅ 创建 Custom Droids
7. ✅ 配置 MCP 扩展功能

### 相关资源

- **Warp 终端**: https://www.warp.dev/
- **Kitty 终端**: https://sw.kovidgoyal.net/kitty/
- **Oh-My-Zsh**: https://ohmyz.sh/
- **Powerlevel10k**: https://github.com/romkatv/powerlevel10k
- **Factory Droid**: https://docs.factory.ai/
- **SWE-Rebench**: https://swe-rebench.com/
- **MCP 协议**: https://modelcontextprotocol.io/
- **Anthropic Agent Skills**: https://www.anthropic.com/news/skills
- **Droid Skills 仓库**: https://github.com/neardws/droid-skills

### 下一步

- 探索更多 Skills 和 Custom Droids
- 根据 SWE-Rebench 数据尝试不同模型
- 为你的特定工作流创建自定义配置
- 加入社区分享你的经验

---

> 🎉 恭喜你完成了 Vibe Coding 环境的配置！开始享受 AI 辅助编程的乐趣吧！

*最后更新：2026年1月*
