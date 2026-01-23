# Vibe Coding 最佳实践

> 本文将带你从零开始搭建一套完整的 Vibe Coding 工作环境，包括终端配置、Shell 美化、AI 编程工具以及进阶技巧。

## 目录

0. 引言
1. 终端配置
2. Oh-My-Zsh 配置
3. Vibe Coding CLI 工具
4. BYOK - 模型选择指南
5. Agent Skills
6. MCP (Model Context Protocol)
7. 高级定制功能
8. 工作流示例
9. 总结与资源

---

## 0. 引言

### 什么是 Vibe Coding

**Vibe Coding** 这个概念由 AI 领域传奇人物 **[Andrej Karpathy](https://x.com/karpathy)**（前 Tesla AI 总监、OpenAI 创始成员）于 2025 年 2 月在 X (Twitter) 上首次提出。

![The X Post about Vibe Coding ](https://neardws.com/images/posts/vibe-coding/Generated Image January 20, 2026 - 1_20PM.jpeg)
*The X Post about Vibe Coding *

简单来说，Vibe Coding 是一种"氛围驱动"的编程方式：

- 🗣️ 用自然语言描述你想要的功能
- 🤖 AI 负责生成代码，你负责验证效果
- 🔄 快速迭代，不纠结于代码细节
- ✨ 专注创意和问题本身，而非语法和调试

这个词在提出后迅速走红，甚至被 **Merriam-Webster 词典**收录为 2025 年度流行词汇。

> 📚 延伸阅读：
> - Vibe Coding - Wikipedia
> - Simon Willison: Not all AI-assisted programming is vibe coding

### 为什么选择这套工具链

- 现代化终端体验：Kitty 和 Warp 提供流畅、美观的终端界面
- 高效的 Shell 环境：Oh-My-Zsh + Powerlevel10k 带来强大的命令行增强
- 智能 AI 编程：Factory Droid 提供专业级的 AI 编程辅助
- 灵活的模型选择：BYOK 让你可以使用任何 LLM 模型
- 可扩展的技能系统：Skills 和 Custom Droids 让 AI 更懂你的工作流

### 目标读者

本教程面向所有对 AI 编程感兴趣的开发者，无论你是刚入门的新手还是经验丰富的老手。每个步骤都有详细说明，跟着做就能完成配置。

### Quick Start

根据你的偏好，选择以下任一配置方式：

| 方式 | 说明 |
| --- | --- |
| 🤖 AI Agent 配置 | 下载 [LLM 配置指南](/scripts/vibe-coding-llm-guide.md)，复制给 Warp AI 或 Factory Droid，让 AI 自动完成配置 |
| ⚡ 一键脚本 | 运行 `curl -fsSL https://neardws.com/scripts/vibe-setup.sh | bash` |
| 📖 手动配置 | 继续阅读下文，按步骤手动配置每个组件 |

---

## 1. 终端配置

一个好的终端是 Vibe Coding 的基础。这里介绍两款优秀的现代终端。

### 1.1 Kitty 终端

[Kitty](https://sw.kovidgoyal.net/kitty/) 是一款基于 GPU 加速的终端模拟器，高度可定制且性能优异。

![Kitty Terminal: https://sw.kovidgoyal.net/kitty/](https://neardws.com/images/posts/vibe-coding/CleanShot 2026-01-20 at 13.37.37@2x.png)
*Kitty Terminal: https://sw.kovidgoyal.net/kitty/*

#### 特点

- 🖥️ GPU 渲染，超快速度
- ⚙️ 高度可配置
- 🖼️ 支持图片显示
- 📑 内置多标签和分屏

#### 安装步骤

**Linux / macOS（推荐方式）：**

```bash
curl -L https://sw.kovidgoyal.net/kitty/installer.sh | sh /dev/stdin
```

**macOS （Homebrew）:**

```bash
brew install --cask kitty
```

安装位置：

- macOS: /Applications/kitty.app
- Linux: ~/.local/kitty.app

> ⚠️ 注意：Kitty 不支持 Windows 原生运行，但可在 WSL2 + WSLg 环境下使用。
> 💡 更新 Kitty：只需重新运行安装脚本即可。

**Linux 桌面集成（可选，如果希望在桌面菜单和任务栏显示 Kitty 图标）：**

```bash
# 创建符号链接（确保 \~/.local/bin 在 PATH 中）
ln -sf \~/.local/kitty.app/bin/kitty \~/.local/kitty.app/bin/kitten \~/.local/bin/
```

```bash
# 复制桌面文件
cp \~/.local/kitty.app/share/applications/kitty.desktop \~/.local/share/applications/
```

```bash
# 更新图标和路径
sed -i "s|Icon=kitty|Icon=$(readlink -f \~)/.local/kitty.app/share/icons/hicolor/256x256/apps/kitty.png|g"
\~/.local/share/applications/kitty\*.desktop
sed -i "s|Exec=kitty|Exec=$(readlink -f \~)/.local/kitty.app/bin/kitty|g" \~/.local/share/applications/kitty\*.desktop
```

---

#### 基础配置

创建或编辑配置文件 `~/.config/kitty/kitty.conf`：

```bash
# ===== 主题引入 =====
include ./theme.conf

# ===== 远程控制（支持实时预览主题）=====
allow_remote_control yes

# ===== 字体设置 =====
# 主字体 - 英文
font_family      Berkeley Mono
bold_font        Berkeley Mono Bold
italic_font      Berkeley Mono Italic
font_size 14.0

# 中文字体回退 - CJK 字符范围
symbol_map U+4E00-U+9FFF,U+3400-U+4DBF Maple Mono CN

# Nerd Font 图标 - Private Use Area
symbol_map U+E000-U+F8FF,U+F0000-U+FFFFF Hack Nerd Font

# ===== 窗口设置 =====
window_padding_width 4
hide_window_decorations no
mouse_hide_wait 3.0
term xterm-kitty

# ===== 布局 =====
enabled_layouts splits,stack

# ===== Tab Bar 设置 =====
tab_bar_edge bottom
tab_bar_style custom
tab_bar_min_tabs 1
tab_bar_margin_height 5.0 0.0
tab_bar_background #1e1e2e

# Tab 颜色 (Soft Pastel 风格)
active_tab_foreground   #1e1e2e
active_tab_background   #cdd6f4
active_tab_font_style   bold
inactive_tab_foreground #cdd6f4
inactive_tab_background #313244

# ===== 快捷键 (macOS) =====
# 分屏
map cmd+d launch --location=hsplit    # 水平分屏
map cmd+r launch --location=vsplit    # 垂直分屏

# Tab 管理
map cmd+t new_tab
map cmd+w close_window
map cmd+shift+w close_tab
map cmd+1 goto_tab 1
map cmd+2 goto_tab 2
# ... cmd+3-9 类似

# 焦点切换
map cmd+j neighboring_window left
map cmd+k neighboring_window right
map cmd+i neighboring_window up
map cmd+m neighboring_window down

# 其他
map cmd+c copy_to_clipboard
map cmd+v paste_from_clipboard
map cmd+equal change_font_size all +1.0
map cmd+minus change_font_size all -1.0
map cmd+enter toggle_fullscreen
```

#### 安装主题

![Kitty Themes：https://github.com/dexpota/kitty-themes](https://neardws.com/images/posts/vibe-coding/CleanShot 2026-01-20 at 14.36.59@2x.png)
*Kitty Themes：https://github.com/dexpota/kitty-themes*

```bash
# 克隆主题仓库
git clone --depth 1 https://github.com/dexpota/kitty-themes.git \~/.config/kitty/kitty-themes
```

```bash
# 选择主题（以 Dracula 为例）
ln -sf ./kitty-themes/themes/Dracula.conf \~/.config/kitty/theme.conf
```

```bash
# 或使用内置主题切换器
kitty +kitten themes
```

#### 自定义 Tab Bar

从 [neardws/kitty-config](https://github.com/neardws/kitty-config) 获取完整配置：

```bash
# 克隆配置仓库
git clone https://github.com/neardws/kitty-config.git \~/kitty-config
```

```bash
# 复制配置文件
cp \~/kitty-config/kitty.conf \~/.config/kitty/
cp \~/kitty-config/tab\_bar.py \~/.config/kitty/
```

功能特性：

- 10 色循环色板（Catppuccin 风格）
- 左侧：用户名、当前目录、Git 分支
- 中间：Tab 列表（序号 + 程序名）
- 右侧：Session 名、时间（15秒刷新）
- SSH 模式自动显示服务器信息

Tab Bar 布局：

![Kitty 自定义Tab Bar](https://neardws.com/images/posts/vibe-coding/CleanShot 2026-01-20 at 14.49.26@2x.png)
*Kitty 自定义Tab Bar*

[👤 用户] [📁 目录] [Git] [1 zsh] [2 vim] [3 python] [💻 Session] [🕐 时间]

> ⚠️ 注意：自定义Tab Bar需要Nerd Font，详见安装Nerd Font。

#### Zsh 配置

```bash
# ===== Kitty SSH + Tmux 配置 =====
# kitten ssh 基础别名
alias s="kitten ssh"
```

```bash
# 服务器 1 - local (局域网)
alias ssh-local="kitten ssh user@local-server"
alias st-local="kitten ssh user@local-server -t 'tmux new -As main'"

# 服务器 2 - remote （远程)
alias ssh-remote="kitten ssh user@remote-server"
alias st-remote="kitten ssh user@remote-server -t 'tmux new -As main'"
```

> ⚠️ 注意：user 填写实际用户名，local-server/remote-server 填写实际局域网或远程服务器IP地址。

在 `~/.zshrc ` 添加以下函数，连接服务器时自动设置 Tab 标题：

```bash
# ===== Kitty Tab 自动命名 =====
# 检测是否在 Kitty 终端中运行
if [[ "$TERM" == "xterm-kitty" ]]; then
# 设置 tab 名为当前目录名
function _kitty_set_tab_title() {
printf "\033]1;%s\007" "${PWD##*/}"
}

# 目录切换时触发
autoload -Uz add-zsh-hook
add-zsh-hook chpwd _kitty_set_tab_title

# 初始化时也设置一次
_kitty_set_tab_title
fi

# SSH + tmux 并自动设置 Tab 标题
st-server-s() {
local session="$\{1:-main}"
kitty @ set-tab-title "#server:$session" # #前缀触发自定义标题
kitten ssh user@your-server -t "tmux new -As $session"
}

# 示例：多服务器配置
st-dev-s() {
local session="${1:-main}"
kitty @ set-tab-title "#dev:$session"
kitten ssh user@dev-server -t "tmux new -As $session"
}

st-prod-s() {
local session="${1:-main}"
kitty @ set-tab-title "#prod:$session"
kitten ssh user@prod-server -t "tmux new -As $session"
}
```

使用方式：

| 命令 | 效果 | Tab 标题 |
| --- | --- | --- |
| `st-dev-s` | 连接 dev + main 会话 | `dev:main` |
| `st-dev-s work` | 连接 dev + work 会话 | `dev:work` |
| `st-prod-s train` | 连接 prod + train 会话 | `prod:train` |

> 📚 完整配置参考：neardws/kitty-config

---

#### 推荐字体

终端字体需要满足三个需求：英文显示、中文显示、图标支持。以下是我推荐的三款字体：

| 字体 | 用途 | 特点 |
| --- | --- | --- |
| [Berkeley Mono](https://berkeleygraphics.com/typefaces/berkeley-mono/) | 英文等宽 | 优雅、清晰，专为编程设计 |
| [Maple Mono CN](https://github.com/subframe7536/maple-font) | 中文显示 | 开源、美观，中英文等宽对齐 |
| [Hack Nerd Font](https://www.nerdfonts.com/) | 图标支持 | Tab Bar 必需，包含 3000+ 图标 |

![Berkeley Mono Font: https://usgraphics.com/products/berkeley-mono](https://neardws.com/images/posts/vibe-coding/CleanShot 2026-01-20 at 14.23.33@2x.png)
*Berkeley Mono Font: https://usgraphics.com/products/berkeley-mono*

#### 安装 Nerd Font（图标支持必需）

**macOS:**

```bash
# macOS
brew tap homebrew/cask-fonts
brew install --cask font-hack-nerd-font
```

**Linux:**

```bash
# Linux
mkdir -p ~/.local/share/fonts
cd ~/.local/share/fonts
curl -fLO https://github.com/ryanoasis/nerd-fonts/releases/download/v3.1.1/Hack.zip
unzip Hack.zip && rm Hack.zip
fc-cache -fv
```

> 💡 Berkeley Mono 为付费字体，可从 官网 购买。
> Maple Mono CN 开源免费，从 GitHub 下载。
> 当然，也可以选择你自己喜欢的字体。

---

### 1.2 Warp 终端

[Warp](https://app.warp.dev/referral/28JVZ3) 是一款现代化的终端，内置 AI 功能，专为开发者设计。

![Warp Terminal: https://www.warp.dev/](https://neardws.com/images/posts/vibe-coding/CleanShot 2026-01-20 at 16.29.10@2x.png)
*Warp Terminal: https://www.warp.dev/*

#### 特点

- 🚀 内置 AI 命令建议
- 📝 块状命令输出，便于复制和分享
- 🎨 现代化 UI 设计
- ⚡ 极速启动和响应

#### 安装步骤

> 📌 平台支持：macOS (Intel/Apple Silicon)、Windows (x64/ARM64)、Linux (x64/ARM64)

**macOS:**

```bash
brew install --cask warp
```

**Windows:**

```bash
winget install Warp.Warp
```

**Linux (Debian/Ubuntu):**

```bash
# 下载 .deb 包安装（推荐）
# 从 https://www.warp.dev/download 下载后：
sudo apt install ./.deb
```

```bash
# 或使用 apt 仓库
sudo apt-get install wget gpg
wget -qO- https://releases.warp.dev/linux/keys/warp.asc | gpg --dearmor > warpdotdev.gpg
sudo install -D -o root -g root -m 644 warpdotdev.gpg /etc/apt/keyrings/warpdotdev.gpg
sudo sh -c 'echo "deb \[arch=amd64 signed-by=/etc/apt/keyrings/warpdotdev.gpg] https://releases.warp.dev/linux/deb stable main" > /etc/apt/sources.list.d/warpdotdev.list'
rm warpdotdev.gpg
sudo apt update && sudo apt install warp-terminal
```

![Warp 主界面](https://neardws.com/images/posts/vibe-coding/CleanShot 2026-01-20 at 16.43.06@2x.png)
*Warp 主界面*

---

## 2. Oh-My-Zsh 配置

Oh-My-Zsh 是一个开源的 Zsh 配置管理框架，提供大量主题和插件。

### 什么是 Zsh

Zsh（Z Shell）是一款功能强大的 Unix shell，是 Bash 的增强替代品。相比 Bash，Zsh 提供了：

- 更强大的自动补全：智能补全命令、参数、文件路径，甚至支持 Git 分支补全
- 更好的历史记录管理：跨会话共享历史，支持子字符串搜索
- 丰富的主题和提示符自定义：可高度定制的提示符显示
- 拼写纠正：自动纠正拼写错误的命令
- 通配符扩展增强：更强大的文件匹配模式

macOS Catalina (10.15) 及以后版本已将 Zsh 设为默认 shell。

### 什么是 Oh-My-Zsh

[Oh-My-Zsh](https://ohmyz.sh/) 是一个社区驱动的 Zsh 配置管理框架，让 Zsh 的配置和使用变得简单：

- 300+ 插件：Git、Docker、npm、kubectl 等常用工具的增强支持
- 150+ 主题：开箱即用的美观提示符主题
- 简单的插件管理：只需在配置文件中添加插件名即可启用
- 活跃的社区：持续更新和维护

简而言之：**Zsh 是 shell 本身，Oh-My-Zsh 是让 Zsh 更易用、更强大的配置框架。**

![Oh My Zsh: https://ohmyz.sh/](https://neardws.com/images/posts/vibe-coding/CleanShot 2026-01-20 at 16.52.33@2x.png)
*Oh My Zsh: https://ohmyz.sh/*

---

### 2.1 安装 Zsh

**首先检查并安装 Zsh：**

```bash
# 首先检查是否安装
zsh --version
```

如果未安装，根据你的操作系统选择对应的安装命令：

**macOS:**

```bash
# macOS 10.15+ 已预装 Zsh，如需更新可使用 Homebrew
brew install zsh
```

** Ubuntu/Debian:**

```bash
sudo apt install zsh
```

**Windows:**

Windows 用户可以通过以下方式使用 Zsh：

*方式一：WSL（推荐）*

- Step 1: 安装WSL

```powershell
wsl --install
```

- Step 2: 重启系统后，在 WSL 的 Ubuntu 中安装 Zsh

```bash
sudo apt install zsh
```

*方式二：Git Bash + Zsh*

- Step 1: 先安装 Git for Windows
- Step 2: 下载 Zsh for Windows
- Step 3: 解压到 Git 安装目录（如 C:\Program Files\Git）
- Step 4: 在 /.bashrc 中添加以下内容自动启动 Zsh

```bash
if \[ -t 1 ]; then
exec zsh
fi
```

**最后，安装完成后，将 Zsh 设为默认 Shell：**

```bash
# 设置 Zsh 为默认 Shell
chsh -s $(which zsh)
```

### 2.2 安装 Oh-My-Zsh

```bash
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

![Oh-My-Zsh 安装过程](https://neardws.com/images/posts/vibe-coding/CleanShot 2026-01-20 at 17.40.27@2x.png)
*Oh-My-Zsh 安装过程*

---

### 2.3 Powerlevel10k 主题

[Powerlevel10k](https://github.com/romkatv/powerlevel10k) 是最受欢迎的 Zsh 主题之一，提供丰富的信息展示和极快的渲染速度。

#### 安装 Nerd Font

首先需要[安装 Nerd Font](#安装-nerd-font图标支持必需) 以正确显示图标。

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

![Powerlevel10k 主题设置](https://neardws.com/images/posts/vibe-coding/CleanShot 2026-01-20 at 17.50.11@2x.png)
*Powerlevel10k 主题设置*

![Powerlevel10k 主题最终效果](https://neardws.com/images/posts/vibe-coding/CleanShot 2026-01-20 at 17.53.00@2x.png)
*Powerlevel10k 主题最终效果*

### 2.3 插件配置

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

| 插件 | 功能 | 使用示例 |
| --- | --- | --- |
| `git` | Git 命令别名 | `gst` = `git status`, `gco` = `git checkout` |
| `sudo` | 快速添加 sudo | 双击 `ESC` 在当前命令前添加 sudo |
| `history` | 历史搜索 | `Ctrl+R` 搜索历史命令 |
| `extract` | 通用解压 | `extract file.tar.gz` 自动识别格式 |
| `z` | 智能跳转 | `z project` 跳转到包含 "project" 的常用目录 |
| `zsh-autosuggestions` | 命令建议 | 输入时显示灰色建议，按 `→` 接受 |
| `zsh-syntax-highlighting` | 语法高亮 | 正确命令绿色，错误命令红色 |
| `zsh-completions` | 额外补全 | 更多命令的 Tab 补全支持 |

---

## 3. Vibe Coding CLI 工具

### 为什么选择 CLI 而非 IDE

说实话，Cursor 这类 IDE 工具确实好用，开箱即用，界面友好，写代码的时候 inline completion 配合 visual diff，心流体验拉满。但用久了，或者项目复杂起来，你会发现几个问题。

- 上下文是个黑盒。 Cursor 号称 200K token 上下文，实际跑起来经常只有 70K-120K，而且不会告诉你原因。有人做过测试：同样搭一个 Next.js项目，Claude Code CLI 用了 33K tokens 零错误完成，Cursor 用了 188K tokens 还出 bug，因为你不知道它往 context 里塞了什么。
- 资源占用感人。 Cursor 启动要 15-30 秒，内存占用 2-4 GB。CLI 工具秒开，100MB 以内。对于终端党来说，开个 IDE 只为了让 AI 改几行代码，属实有点重。
- 没法自动化。 在 CI/CD 里跑 AI code review、批量处理多个仓库，这些场景 CLI 一行命令就能搞定，IDE 很难做到。
- 绑定编辑器。 用了 Cursor 就得接受 VS Code 那套。如果你习惯 Neovim、Emacs 或者其他编辑器，CLI 工具不挑，终端开着就能用。

当然，如果是新手入门，或者偏好图形界面写小功能，IDE 完全没问题。但如果你是终端党，或者需要处理复杂任务、追求透明可控、有自动化需求，CLI更合适。

| 维度 | CLI工具 | IDE 工具 |
| --- | --- | --- |
| 资源占用 | 轻量，仅终端 | 重，需运行完整 IDE |
| 灵活性 | 可与任何编辑器配合 | 绑定特定 IDE |
| 自动化 | 易于脚本化、CI/CD 集成 | 难以自动化 |
| 透明度 | 所有操作可见可控 | 部分操作在后台 |
| 上下文控制 | 精确控制输入内容 | IDE 自动收集（有时过多） |

---

### 3.1 主流 Vibe Coding CLI 工具

| 工具 | 开源 | 特点 | 适用场景 |
| --- | --- | --- | --- |
| [Claude Code](https://claude.com/product/claude-code) | 否 | Anthropic 官方，200K 上下文，深度推理能力强 | Claude 用户、复杂任务 |
| [Codex CLI](https://developers.openai.com/codex/cli/) | [是](https://github.com/openai/codex) | OpenAI 官方，轻量级，支持 ChatGPT Pro/Plus | OpenAI 生态用户 |
| [Gemini CLI](https://geminicli.com) | [是](https://github.com/google-gemini/gemini-cli) | Google 官方，免费用 Gemini 2.5 Pro | 预算有限、Google 生态 |
| [OpenCode](https://opencode.ai) | [是](https://github.com/anomalyco/opencode) | 支持 75+ 模型，可切换 Claude/GPT/Gemini | 多模型切换用户 |
| [Factory Droid](https://factory.ai) | 否 | 全平台无缝切换，CI/CD 可大规模并行，企业级安全 | 专业开发者 ⭐推荐 |

### 3.2 Factory Droid 安装

#### 什么是Factory Droid ？

Factory Droid 是 Factory AI 推出的命令行 AI 编程工具，具有以下特点：

- 🤖 强大的代码理解和生成能力
- 📁 直接读写文件系统
- 🔧 执行 Shell 命令
- 🌐 支持多种 LLM 模型
- 🎯 可扩展的 Skills 系统
- 🔗 MCP 协议支持

![Factory Droid: https://factory.ai/](https://neardws.com/images/posts/vibe-coding/CleanShot 2026-01-20 at 18.44.50@2x.png)
*Factory Droid: https://factory.ai/*

#### 安装Factory Droid

**macOS/Linux:**

```bash
curl -fsSL https://app.factory.ai/cli | sh
```

**Windows:**

```bash
irm https://app.factory.ai/cli/windows | iex
```

> ⚠️ Linux 用户注意：确保已安装 xdg-utils 以获得完整功能：sudo apt-get install xdg-utils

#### 启动Factory Droid

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

| 配置项 | 可选值 | 说明 |
| --- | --- | --- |
| `model` | opus, sonnet, gpt-5.1, gpt-5.2, haiku 等 | 默认 AI 模型 |
| `reasoningEffort` | off, none, low, medium, high | 推理深度 |
| `autonomyMode` | normal, spec, auto-low, auto-medium, auto-high | 自主模式 |
| `specModeReasoningEffort` | off, none, low, medium, high | 规范模式推理 |

### 3.3 Hooks 配置

> Hooks 允许你在特定事件发生时自动执行操作，极大增强工作流。

编辑 `~/.factory/settings.json`，当前Hooks配置与[planning-with-files](#planning-with-files---复杂任务规划) Skill 相关：

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

| Hook 类型 | 触发时机 | 用途 |
| --- | --- | --- |
| `SessionStart` | 会话开始时 | 初始化提示、加载上下文 |
| `PreToolUse` | 使用工具前 | 检查状态、读取计划 |
| `PostToolUse` | 使用工具后 | 更新状态、格式化文件 |
| `Stop` | 会话结束时 | 清理、总结 |

---

### 3.4 Factory Droid 使用指南

#### 基础操作

**快捷键**

| 快捷键 | 功能 |
| --- | --- |
| `Enter` | 发送消息 |
| `Shift+Enter` | 换行（多行输入） |
| `Shift+Tab` | 切换模式（Normal/Spec/Auto） |
| `!` | 切换 Bash 模式（输入框为空时） |
| `Esc` | 退出 Bash 模式 / 中断操作 |
| `?` | 查看所有快捷键 |
| `Ctrl+C` | 退出 Droid |

**基本交互流程（详细版本可参考[工作流示例](#8-工作流示例)）**

1. 输入你的任务描述
2. Droid 分析代码库并制定计划
3. 审查 Droid 提出的更改
4. 接受或拒绝修改
5. 继续迭代直到任务完成

#### Slash 命令

在 Droid 中输入 `/` 开头的命令来执行特定操作：

| 命令 | 说明 |
| --- | --- |
| `/settings` | 配置 Droid 设置 |
| `/model` | 切换 AI 模型 |
| `/review` | 启动 AI 代码审查工作流 |
| `/mcp` | 管理 MCP 服务器 |
| `/sessions` | 列出和选择历史会话 |
| `/droids` | 管理自定义 Droids |
| `/skills` | 管理和调用 Skills |
| `/hooks` | 管理生命周期 Hooks |
| `/cost` | 查看 Token 使用统计 |
| `/new` | 开始新会话 |
| `/help` | 查看所有可用命令 |

#### Specification Mode（规范模式）

规范模式是 Droid 的核心功能之一，遵循「先规划、后执行」的原则。

- 激活方式

按 **Shift+Tab** 切换到 Spec 模式。

- 工作流程

		
			描述功能 - 用 4-6 句话描述你想要实现的功能
- Droid 生成规范 - 自动分析代码库，生成详细的实现计划
- 审查和批准 - 你可以修改或批准计划
- 实现 - 批准后 Droid 开始执行，每个修改都会展示给你审查
- 安全保证

		
			 分析阶段只读，不会修改任何文件
- 所有更改在批准后才会执行
- 完整可见的实现计划

	批准选项

| 选项 | 说明 |
| --- | --- |
| Proceed (手动) | 批准计划，保持手动确认每个操作 |
| Proceed + Auto (Low) | 批准计划，自动执行文件编辑和只读命令 |
| Proceed + Auto (Medium) | + 自动执行可逆命令（npm install 等） |
| Proceed + Auto (High) | + 自动执行高风险命令（git push 等） |
| Keep iterating | 继续修改规范 |

#### Auto-Run Mode（自动运行模式）

Auto-Run 模式让你可以控制 Droid 的自主执行级别。

| 级别 | 自动执行的操作 | 示例 |
| --- | --- | --- |
| Auto (Low) | 文件编辑、只读命令 | ls, git status, rg |
| Auto (Medium) | + 可逆的工作区修改 | npm install, git commit, mv, cp |
| Auto (High) | + 高风险命令（未明确禁止的） | git push, docker, 数据库迁移 |

- 切换方式

		
			按 Shift+Tab 循环切换：Normal → Spec → Auto (Low) → Auto (Medium) → Auto (High)
- 或在 `/settings` 中设置默认级别

	安全机制（即使在 Auto (High) 模式下，以下操作仍需确认）：

		
- 危险命令（如 `rm -rf /`）
- 命令替换（`$(...)` 或反引号）
- CLI 安全检查标记的操作

#### Bash Mode （命令行模式）

Bash 模式让你可以直接在 Droid 中执行 Shell 命令，无需 AI 解释。

- 使用方法

		
			在输入框为空时按 `!` 进入 Bash 模式
- 提示符从 `>` 变为 `$`
- 输入任何 Shell 命令并按 Enter 执行
- 按 `Esc` 返回 AI 对话模式
- 适用场景

		
			快速检查 `git status`
- 运行 `npm test` 或 `make build`
- 查看文件内容或目录结构

#### 定价方案

Factory 通过标准 Token（Standard Tokens）计量使用量。缓存 Token 按 1/10 计费（10 个缓存 Token = 1 个标准 Token）。

- 订阅方案

| 方案 | 标准 Token / 月 | 价格 / 月 |
| --- | --- | --- |
| Free | BYOK（自带 API Key） | $0 |
| Pro | 1000 万 (+1000 万奖励 Token) | $20 |
| Max | 1 亿 (+1 亿奖励 Token) | $200 |
| Ultra | 10 亿 (+10 亿奖励 Token) | $2,000 |

超额使用按 **$2.70 / 百万标准 Token** 计费。

- 模型计费乘数

不同模型有不同的乘数来计算标准 Token 使用量：

| 模型 | Model ID | 乘数 |
| --- | --- | --- |
| Gemini 3 Flash | `gemini-3-flash-preview` | 0.2× |
| Droid Core | `glm-4.6` | 0.25× |
| Claude Haiku 4.5 | `claude-haiku-4-5-20251001` | 0.4× |
| GPT-5.1 | `gpt-5.1` | 0.5× |
| GPT-5.1-Codex | `gpt-5.1-codex` | 0.5× |
| GPT-5.1-Codex-Max | `gpt-5.1-codex-max` | 0.5× |
| GPT-5.2 | `gpt-5.2` | 0.7× |
| Gemini 3 Pro | `gemini-3-pro-preview` | 0.8× |
| Claude Sonnet 4.5 | `claude-sonnet-4-5-20250929` | 1.2× |
| Claude Opus 4.5 | `claude-opus-4-5-20251101` | 2× |

- 使用建议
- Free 方案：适合已有 API Key 的用户，无月费
- Pro 方案：适合个人开发者日常使用，性价比高
- 缓存优势：Factory 的缓存机制可显著降低实际 Token 消耗，通常有 4-8 倍的缓存命中率

> 📚 延伸阅读：
> - Factory Droid - Docs

---

## 4. BYOK - 模型选择指南

> BYOK（Bring Your Own Key）让你可以使用自己的 API Key 来访问各种 LLM 模型。

BYOK 允许你：

- 使用自己的 API Key 访问模型
- 选择最适合你需求的模型
- 控制成本和使用量
- 使用本地部署的模型

### 4.1 如何选择模型

[SWE-Rebench](https://swe-rebench.com/) 是一个持续更新的软件工程 LLM 基准测试排行榜，帮助你了解各模型在实际编程任务中的表现。

![SWE-reBench: https://swe-rebench.com/](https://neardws.com/images/posts/vibe-coding/CleanShot 2026-01-20 at 20.18.22@2x.png)
*SWE-reBench: https://swe-rebench.com/*

#### 关键指标解读

| 指标 | 含义 | 重要性 |
| --- | --- | --- |
| Resolved Rate | 成功解决问题的比例 | 最重要，反映模型能力 |
| Pass@5 | 5 次尝试中至少成功 1 次的比例 | 反映模型稳定性 |
| Cost per Problem | 每个问题的平均成本 | 影响使用成本 |
| Tokens per Problem | 每个问题消耗的 token 数 | 反映效率 |

### 4.2 推荐模型（2026年1月数据）

根据最新的 SWE-Rebench 数据，以下是不同场景的模型推荐：

#### 顶级性能

| 模型 | Resolved Rate | Pass@5 | Cost/Problem | 特点 |
| --- | --- | --- | --- | --- |
| [Claude Opus 4.5](https://www.anthropic.com/news/claude-opus-4-5) | 63.3% | 79.2% | $1.22 | 最高性能，复杂任务首选 |
| [GPT-5.2 xhigh](https://openai.com/index/introducing-gpt-5-2/) | 61.5% | 70.8% | $1.46 | OpenAI 最强，推理能力强 |
| [Gemini 3 Flash Preview](https://blog.google/products-and-platforms/products/gemini/gemini-3-flash/) | 60.0% | 72.9% | $0.29 | 性价比极高 |

#### 性价比之选

| 模型 | Resolved Rate | Pass@5 | Cost/Problem | 特点 |
| --- | --- | --- | --- | --- |
| [Gemini 3 Flash Preview](https://blog.google/products-and-platforms/products/gemini/gemini-3-flash/) | 60.0% | 72.9% | $0.29 | 🏆 性价比之王 |
| [GPT-5.2 medium](https://openai.com/index/introducing-gpt-5-2/) | 59.4% | 70.8% | $0.86 | 平衡性能与成本 |
| [Claude Sonnet 4.5](https://www.anthropic.com/news/claude-sonnet-4-5) | 57.5% | 75.0% | $0.98 | 日常任务首选 |

#### 开源模型

| 模型 | Resolved Rate | Pass@5 | Cost/Problem | 特点 |
| --- | --- | --- | --- | --- |
| [GLM-4.7](https://docs.z.ai/guides/llm/glm-4.7) | 51.3% | 66.7% | $0.40 | 🏆 开源最强 |
| [DeepSeek-V3.2](https://api-docs.deepseek.com/news/news251201) | 48.5% | 68.8% | $0.25 | 可本地部署 |
| [Kimi K2 Thinking](https://moonshotai.github.io/Kimi-K2/thinking.html) | 40.5% | 60.4% | $0.48 | 国产优秀选择 |

#### 预算友好

| 模型 | Resolved Rate | Pass@5 | Cost/Problem | 特点 |
| --- | --- | --- | --- | --- |
| [Grok Code Fast 1](https://x.ai/news/grok-code-fast-1) | 35.9% | 54.2% | $0.08 | 最便宜 |
| [Devstral-2-123B](https://mistral.ai/news/devstral-2-vibe-cli) | 36.6% | 59.6% | $0.09 | 开源可自托管 |
| [MiniMax M2.1](https://www.minimax.io/news/minimax-m21) | 37.3% | 58.3% | $0.10 | 缓存友好 |

---

### 4.3 BYOK配置

#### 配置自定义模型

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

| 参数 | 必填 | 说明 |
| --- | --- | --- |
| `model` | 是 | 模型名称，发送给 API 的 model 参数 |
| `id` | 否 | 唯一标识符，格式为 `custom:名称`，用于在 Droid 中选择模型 |
| `displayName` | 否 | 在 UI 中显示的名称，便于识别 |
| `baseUrl` | 是 | API 端点地址，不同服务有不同地址 |
| `apiKey` | 是 | API 密钥，本地服务可填 `not-needed` |
| `provider` | 是 | 提供商类型：`openai`、`anthropic`、`generic-chat-completion-api` |
| `noImageSupport` | 否 | 是否禁用图片支持，默认 `false` |
| `maxOutputTokens` | 否 | 最大输出 Token 数，本地模型建议设置 |

#### 常用 baseUrl 参考

**海外服务：**

| 服务 | baseUrl | 说明 |
| --- | --- | --- |
| OpenAI | `https://api.openai.com/v1` | OpenAI 官方 API |
| Anthropic | `https://api.anthropic.com/v1` | Anthropic 官方 API |
| Google Gemini | `https://generativelanguage.googleapis.com/v1beta/` | Google AI Studio |
| OpenRouter | `https://openrouter.ai/api/v1` | 多模型聚合平台 |
| Hugging Face | `https://router.huggingface.co/v1` | HF 推理路由 |

**国内服务：**

| 服务 | baseUrl | 说明 |
| --- | --- | --- |
| DeepSeek | `https://api.deepseek.com/v1` | DeepSeek 官方 API |
| 智谱 AI (GLM) | `https://open.bigmodel.cn/api/paas/v4` | GLM 系列模型 |
| 阿里通义千问 | `https://dashscope.aliyuncs.com/compatible-mode/v1` | Qwen 系列模型 |
| Moonshot (Kimi) | `https://api.moonshot.cn/v1` | Kimi 系列模型 |
| 百度千帆 | `https://aip.baidubce.com` | 文心一言 |
| 字节豆包 | `https://ark.cn-beijing.volces.com/api/v3` | 豆包大模型 |
| SiliconFlow | `https://api.siliconflow.cn/v1` | 国内模型聚合平台 |

**本地部署：**

| 服务 | baseUrl | 说明 |
| --- | --- | --- |
| Ollama 本地 | `http://localhost:11434/v1` | 本地模型部署 |
| vLLM | `http://localhost:8000/v1` | 高性能本地推理 |
| LM Studio | `http://localhost:1234/v1` | 桌面端本地模型 |

#### 使用本地部署LLM

** Ollama（推荐）**

```json
{
"customModels": [
{
"model": "qwen2.5-coder:32b",
"displayName": "Qwen 2.5 Coder 32B [Local]",
"baseUrl": "http://localhost:11434/v1",
"apiKey": "not-needed",
"provider": "generic-chat-completion-api",
"maxOutputTokens": 16000
}
]
}
```

** vLLM**

```json
{
"customModels": [
{
"model": "your-model",
"displayName": "vLLM Model",
"baseUrl": "http://localhost:8000/v1",
"apiKey": "not-needed",
"provider": "openai"
}
]
}
```

**LM Studio**

```
{
"customModels": [
{
"model": "local-model",
"displayName": "LM Studio Model",
"baseUrl": "http://localhost:1234/v1",
"apiKey": "lm-studio",
"provider": "openai"
}
]
}
```

> ⚠️ 注意：配置时要使用实际的model name, baseUrl和apiKey。

---

## 5. Agent Skills

Skills 是 Anthropic 于 2025 年 10 月推出的 Claude Agent Skills 系统，Factory Droid 完整支持该系统。Skills 是可组合、可移植的指令集，为 AI 提供特定领域的专业知识和工作流。

### 什么是 Skills

Skills 是 Anthropic 为 Claude 设计的一套可扩展能力系统。本质上，Skill 是一个包含指令、脚本和资源的文件夹，Claude 可以在执行相关任务时自动加载和使用。

![Agent Skills: https://agentskills.io/home](https://neardws.com/images/posts/vibe-coding/CleanShot 2026-01-20 at 21.25.25@2x.png)
*Agent Skills: https://agentskills.io/home*

#### 核心特性

| 特性 | 说明 |
| --- | --- |
| 可组合 | 多个 Skills 可以堆叠使用，Claude 自动识别和协调 |
| 可移植 | 一次构建，可在 Claude Code、Factory Droid、API 等多处使用 |
| 高效 | Claude 仅加载当前任务所需的信息，保持响应速度 |
| 强大 | Skills 可包含可执行代码，处理需要高可靠性的任务 |

#### Skills 的作用

- 📋 提供特定领域的最佳实践
- 🔄 定义标准化的工作流程
- 📝 包含模板和检查清单
- 🎯 确保输出质量和一致性

### 5.1 推荐 Skills

#### planning-with-files - 复杂任务规划

> 适用于需要多步骤完成的复杂任务，采用 Manus 风格的文件化规划。

- 核心理念：

上下文窗口 = 内存（易失、有限）

文件系统 = 磁盘（持久、无限）

→ 重要的东西都写到文件里

- 使用方法：

```bash
# 在项目目录创建三个规划文件
task_plan.md   # 任务计划和进度
findings.md    # 研究发现
progress.md    # 会话日志

```

- task_plan.md 示例：

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
| 问题 | 尝试 | 解决方案 |
|------|------|----------|
| JWT 过期处理 | 1 | 添加 refresh token |
```

#### brainstorming - 创意头脑风暴

> 在开始任何创造性工作之前使用，帮助明确需求和设计。

- 工作流程：

		
			了解当前项目上下文
- 一次问一个问题来细化想法
- 提出 2-3 个不同方案及其权衡
- 分段展示设计，每段确认后继续

#### test-driven-development - TDD 开发

> 强制执行测试驱动开发流程。

- 核心原则：

没有失败的测试，就没有生产代码

- Red-Green-Refactor 循环：

		
			RED - 编写一个失败的测试
- 验证 RED - 确认测试失败且原因正确
- GREEN - 编写最少代码使测试通过
- 验证 GREEN - 确认测试通过
- REFACTOR - 重构代码，保持测试通过

#### verification-before-completion - 完成前验证

> 防止在没有验证的情况下声称工作完成。

- 核心原则：

没有验证证据，不做完成声明。

- 验证检查清单：

		
			  运行测试命令，确认 0 失败
-   运行 lint 命令，确认 0 错误
-   运行 build 命令，确认成功
-   逐条检查需求是否满足

#### code-simplifier - 代码简化

> 在编写或修改代码后自动应用，简化和优化代码。

- 优化方向：

		
			减少不必要的复杂度和嵌套
- 消除冗余代码
- 改进命名
- 遵循项目编码规范

### 6.3 Skills 安装与配置

#### 安装位置

Skills 可以安装在两个位置：

| 位置 | 作用域 | 说明 |
| --- | --- | --- |
| `~/.factory/skills/` | 个人 Skills | 跨项目使用，仅对你可见 |
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
cp -r skills/planning-with-files /.factory/skills/
```

重启 `droid` 以加载新安装的 Skills。

#### 可用 Skills 列表

| Skill | 描述 |
| --- | --- |
| planning-with-files | Manus 风格的文件化任务规划 |
| md-table-formatter | 自动格式化 Markdown 表格 |
| superpowers (14 个) | 完整开发工作流套件 |

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

| 资源 | 说明 | 链接 |
| --- | --- | --- |
| Skills Manager Client | Skills 管理客户端工具 | [https://github.com/buzhangsan/skills-manager-client](https://github.com/buzhangsan/skills-manager-client) |
| Superpowers | 完整开发工作流 Skills 套件 | [https://github.com/obra/superpowers](https://github.com/obra/superpowers) |
| Planning With Files | Manus 风格文件化规划 Skill | [https://github.com/OthmanAdi/planning-with-files](https://github.com/OthmanAdi/planning-with-files) |
| Agent Skills | 社区 Skills 集合 | [https://github.com/agentskills/agentskills](https://github.com/agentskills/agentskills) |
| Awesome Claude Skills | Claude Skills 精选列表 | [https://github.com/travisvn/awesome-claude-skills](https://github.com/travisvn/awesome-claude-skills%20) |
| Claude Plugins Official | Anthropic 官方插件/Skills | [https://github.com/anthropics/claude-plugins-official](https://github.com/anthropics/claude-plugins-official) |

---

## 6. MCP (Model Context Protocol)

MCP（Model Context Protocol）是由 Anthropic 开源的标准协议，用于连接 AI 应用与外部系统。可以把 MCP 想象成 AI 应用的 USB-C 接口——就像 USB-C 为电子设备提供标准化连接方式一样，MCP 为 AI 应用提供了连接外部系统的标准化方式。

![MCP: https://modelcontextprotocol.io/docs/getting-started/intro](https://neardws.com/images/posts/vibe-coding/CleanShot 2026-01-20 at 21.29.08@2x.png)
*MCP: https://modelcontextprotocol.io/docs/getting-started/intro*

### 6.1 MCP 概念介绍

#### MCP 能做什么

- 🗓️ AI 助手可以访问你的 Google Calendar 和 Notion，提供更个性化的服务
- 🎨 Claude Code 可以根据 Figma 设计稿生成完整的 Web 应用
- 🏢 企业聊天机器人可以连接多个数据库，让用户通过对话分析数据
- 🖨️ AI 模型可以在 Blender 中创建 3D 设计并用 3D 打印机打印

#### MCP 的核心组件

| 组件 | 说明 |
| --- | --- |
| Tools | 可执行的函数，如搜索、计算、API 调用等 |
| Resources | 数据源，如文件、数据库记录等 |
| Prompts | 预定义的提示模板，用于特定工作流 |

### 6.2 MCP 配置

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

### 6.3 使用 Smithery 安装 MCP Servers

[Smithery](https://smithery.ai/) 是目前最大的 MCP Server 市场，提供 3700+ 个 MCP 应用。推荐使用 Smithery 来发现和安装 MCP Servers。

#### Smithery 的优势

| 特性 | 说明 |
| --- | --- |
| 认证 | 内置 OAuth，无需自己实现认证流程 |
| 可观测 | 查看工具使用情况，优化 AI 体验 |
| 分发 | 发布到 Smithery，可从任何 AI 客户端连接 |
| 协议网关 | Smithery 保持与 MCP 规范同步，无需自己维护 |

#### 热门 MCP Servers

| Server | 用途 | 连接数 |
| --- | --- | --- |
| Gmail | 邮件管理 | 10.13k |
| Linkup | 网络搜索 | 9.53k |
| Google Super | Google 全家桶 | 6.73k |
| GitHub | 代码仓库管理 | 5.98k |
| Google Calendar | 日程管理 | 5.63k |

### 6.4 常用 MCP Servers

#### 官方 Servers

| Server | 用途 | 安装 |
| --- | --- | --- |
| `server-filesystem` | 文件系统访问 | `@modelcontextprotocol/server-filesystem` |
| `server-github` | GitHub 操作 | `@modelcontextprotocol/server-github` |
| `server-postgres` | PostgreSQL 数据库 | `@modelcontextprotocol/server-postgres` |
| `server-sqlite` | SQLite 数据库 | `@modelcontextprotocol/server-sqlite` |
| `server-fetch` | HTTP 请求 | `@modelcontextprotocol/server-fetch` |
| `server-puppeteer` | 浏览器自动化 | `@modelcontextprotocol/server-puppeteer` |
| `server-brave-search` | Brave 搜索 | `@modelcontextprotocol/server-brave-search` |

#### 社区 Servers

| Server | 用途 | 来源 |
| --- | --- | --- |
| Notion | 知识库管理 | Smithery |
| Slack | 团队通讯 | Smithery |
| Linear | 项目管理 | Smithery |
| Figma | 设计协作 | Smithery |
| MongoDB | NoSQL 数据库 | Smithery |

### 6.5 MCP 相关资源

| 资源 | 说明 | 链接 |
| --- | --- | --- |
| MCP 官方文档 | 协议规范和开发指南 | https://modelcontextprotocol.io/ |
| Smithery | MCP Server 市场（推荐） | https://smithery.ai/ |
| MCP 官方注册表 | 官方 MCP Server 注册表 | https://registry.modelcontextprotocol.io/ |
| Awesome MCP Servers | MCP Servers 精选列表 | https://github.com/punkpeye/awesome-mcp-servers |
| MCP Servers 官方仓库 | Anthropic 官方 Servers | https://github.com/modelcontextprotocol/servers |

---

## 7. 高级定制功能

Factory Droid 提供多种定制功能，让你可以根据团队和项目需求扩展 AI 的能力。

### 7.1 AGENTS.md - AI 代理的说明书

AGENTS.md 是一个 Markdown 文件，作为 AI 编程代理的「简报包」，告诉 AI 如何构建、测试和运行你的项目。

#### 为什么需要 AGENTS.md

| 文件 | 目的 | 受众 |
| --- | --- | --- |
| README.md | 快速入门、项目描述 | 人类开发者 |
| AGENTS.md | 构建步骤、测试、约定 | AI 编程代理 |

#### 文件位置与发现

代理按以下顺序查找 AGENTS.md（首个匹配生效）：

1. 当前工作目录的 `./AGENTS.md`
2. 向上查找到仓库根目录
3. 子文件夹中的 `AGENTS.md`
4. 个人覆盖：`~/.factory/AGENTS.md`

#### 常用章节

| 章节 | 内容 |
| --- | --- |
| Build & Test | 编译和运行测试套件的确切命令 |
| Architecture | 主要模块和数据流的一段话总结 |
| Security | API 密钥、端点、认证流程、敏感数据 |
| Git Workflows | 分支策略、提交约定、PR 要求 |
| Conventions | 文件夹结构、命名模式、代码风格 |

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

1. Branch from `main`: `feature/` or `bugfix/`
2. Run `pnpm check` locally before committing
3. Keep commits atomic: `feat: …`, `test: …`
```

#### 最佳实践

- 保持简短 - 目标 ≤150 行，过长会拖慢代理
- 使用具体命令 - 用反引号包裹命令，代理可直接复制
- 随代码更新 - 构建步骤变更时同步更新 AGENTS.md
- 单一信息源 - 链接到 README 或设计文档，而不是复制粘贴

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

| 作用域 | 位置 | 说明 |
| --- | --- | --- |
| 工作区 | `<项目>/.factory/commands` | 项目特定命令，与团队共享 |
| 个人 | `~/.factory/commands` | 私有或跨项目快捷命令 |

- 仅注册 Markdown (`*.md`) 文件和带 shebang (`#!`) 的文件
- 文件名自动转换为 slug：`Code Review.md` → `/code-review`
- 使用 `/commands` 打开命令管理 UI

#### Markdown 命令

Markdown 文件渲染为系统通知，作为 Droid 下一轮对话的种子。

```markdown
---
description: 请求代码审查
argument-hint:
---

请审查 `$ARGUMENTS` 并总结任何合并阻塞、测试缺口和风险区域。

- 突出安全或性能问题
- 建议后续任务和负责人
- 列出需要关注的文件
```

| 前置配置 | 用途 |
| --- | --- |
| `description` | 覆盖斜杠建议中显示的摘要 |
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

| 特性 | Skills | Custom Droids |
| --- | --- | --- |
| 本质 | 知识和指导 | 独立的专门化 AI 代理 |
| 运行方式 | 增强主 AI 的能力 | 作为子代理独立运行 |
| 上下文 | 共享主会话上下文 | 独立的上下文窗口 |
| 工具访问 | 使用主 AI 的工具 | 可限制特定工具集 |
| 模型选择 | 使用主 AI 的模型 | 可指定不同模型 |

#### 存储位置

| 位置 | 作用域 | 说明 |
| --- | --- | --- |
| `<项目>/.factory/droids/` | 项目 Droids | 与团队共享，可版本控制 |
| `~/.factory/droids/` | 个人 Droids | 跨工作区使用，仅对你可见 |

**注意**：当名称相同时，项目定义会覆盖个人定义。

#### 为什么使用 Custom Droids

- 更快的任务委派 - 将复杂检查清单编码一次，通过单个工具调用复用
- 更严格的安全性 - 将代理限制为只读、仅编辑或特定工具集
- 上下文隔离 - 每个子代理使用新的上下文窗口，避免提示膨胀
- 可重复的流程 - 将团队特定的审查、测试或发布检查编码为可版本控制的代码

#### 创建自定义 Droid

**方法一：使用 UI 向导**

1. 运行 `/droids` 打开 Droids 菜单
2. 选择 Create a new Droid
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
Summary:
Findings:
-
-
```

#### 配置字段说明

| 字段 | 说明 |
| --- | --- |
| `name` | 必填。小写字母、数字、`-`、`_`。决定 `subagent_type` 值和文件名 |
| `description` | 可选。在 UI 列表中显示，≤500 字符 |
| `model` | `inherit`（使用父会话模型）或指定模型 ID，如 `claude-sonnet-4-5-20250929` |
| `reasoningEffort` | 可选。设置推理深度：`low`、`medium`、`high` |
| `tools` | 省略表示所有工具；使用类别字符串或工具 ID 数组 |

#### 工具类别

| 类别 | 工具 ID | 用途 |
| --- | --- | --- |
| `read-only` | `Read`, `LS`, `Grep`, `Glob` | 安全分析和文件探索 |
| `edit` | `Create`, `Edit`, `ApplyPatch` | 代码生成和修改 |
| `execute` | `Execute` | Shell 命令执行 |
| `web` | `WebSearch`, `FetchUrl` | 网络研究和内容 |
| `mcp` | 动态填充 | MCP 工具 |

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
2. 按 I 启动导入流程
3. CLI 扫描 Claude Code 代理目录：
4. 项目范围：`<项目>/.claude/agents/`
5. 个人范围：`~/.claude/agents/`
6. 使用 Space 切换选择，A 全选
7. 按 Enter 导入

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
Summary:
Findings:
- :
Mitigations:
-
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

| 实践 | 说明 |
| --- | --- |
| 策略性选择模型 | 简单任务用小模型降低成本，复杂推理用大模型 |
| 限制工具访问 | 使用显式工具列表防止意外的 shell 命令或危险操作 |
| 结构化输出 | 组织提示以输出 `Summary:` 和 `Findings:` 等部分 |
| 版本控制共享 | 将 `.factory/droids/*.md` 提交到仓库，与团队共享 |
| 利用实时更新 | Task 工具现在流式传输实时进度，显示工具调用和结果 |

---

## 8. 工作流示例

让我们通过一个完整的例子来展示 Vibe Coding 工作流——实现一个 CartPole（倒立摆）强化学习游戏，包含完整的前后端。

### 场景：CartPole 强化学习游戏

CartPole 是强化学习的经典问题：通过左右移动小车，让杆子保持直立。我们将用 Vibe Coding 完成：

- 后端：Python + FastAPI，实现环境模拟和 DQN 算法
- 前端：React + Canvas，实时可视化训练过程

![CartPole 游戏界面](https://neardws.com/images/posts/vibe-coding/CleanShot 2026-01-20 at 22.32.54@2x.png)
*CartPole 游戏界面*

### 步骤 1：创建项目并启动 Droid

```bash
# 创建项目目录
mkdir cartpole-rl && cd cartpole-rl

# 启动 Droid，进入 Spec Mode
droid
# 按 Shift+Tab 切换到 Spec 模式

```

### 步骤 2：描述需求（Spec Mode）

在 Spec 模式下输入详细需求：

```bash
我想创建一个 CartPole 强化学习可视化项目：

## 后端（Python + FastAPI）
1. CartPole 环境模拟
- 物理参数：小车质量、杆子长度、重力等
- 状态：[位置, 速度, 角度, 角速度]
- 动作：向左(0) 或 向右(1)

2. DQN 算法实现
- 神经网络：2层全连接，输入4维状态，输出2个动作Q值
- 经验回放缓冲区
- 目标网络软更新

3. API 端点
- POST /train/start - 开始训练
- POST /train/stop - 停止训练
- GET /train/status - 获取训练状态
- WebSocket /ws/game - 实时推送游戏状态

## 前端（React + Vite）
1. Canvas 可视化
- 绘制小车、杆子、轨道
- 实时更新位置和角度

2. 控制面板
- 开始/暂停/重置按钮
- 训练回合数显示
- 当前奖励显示

3. 训练曲线图
- 显示每回合的总奖励
- 使用 Chart.js 或 Recharts

请先给我一个实现计划。
```

### 步骤 3：审查并批准计划

Droid 会生成详细的实现计划，包括：

```markdown
Specification for approval

项目结构

cartpole-rl/
├── backend/
│   ├── main.py              # FastAPI 入口
│   ├── cartpole_env.py      # CartPole 环境实现
│   ├── dqn_agent.py         # DQN 算法
│   ├── training_manager.py  # 训练状态管理
│   └── requirements.txt
├── frontend/
│   ├── src/
│   │   ├── App.tsx
│   │   ├── components/
│   │   │   ├── CartPoleCanvas.tsx   # Canvas 可视化
│   │   │   ├── ControlPanel.tsx     # 控制面板
│   │   │   └── TrainingChart.tsx    # 训练曲线
│   │   ├── hooks/
│   │   │   └── useWebSocket.ts      # WebSocket hook
│   │   └── api/
│   │       └── training.ts          # API 调用
│   ├── package.json
│   └── vite.config.ts
└── README.md

后端实现步骤

1. CartPole 环境 (`cartpole_env.py`)
•  自定义实现（不依赖 Gym），便于控制和调试
•  物理参数可配置：重力 9.8，小车质量 1.0，杆子质量 0.1，杆子长度 0.5
•  step(action) 返回 (state, reward, done)
•  reset() 重置环境

2. DQN Agent (`dqn_agent.py`)
•  使用 PyTorch 实现神经网络：4 → 128 → 128 → 2
•  经验回放：deque 缓冲区，容量 10000
•  目标网络：软更新 τ=0.005
•  ε-贪婪策略：ε 从 1.0 衰减到 0.01

3. 训练管理器 (`training_manager.py`)
•  后台线程运行训练循环
•  维护训练状态：episode、reward、running 标志
•  每步通过队列发送状态给 WebSocket

4. FastAPI 端点 (`main.py`)

python
POST /train/start    # 启动训练线程
POST /train/stop     # 停止训练
GET  /train/status   # 返回 {episode, total_reward, epsilon}
WS   /ws/game        # 推送 {cart_x, pole_angle, reward, done}

前端实现步骤

1. 项目初始化
•  npm create vite@latest frontend -- --template react-ts
•  安装依赖：recharts（图表）

2. CartPoleCanvas 组件
•  Canvas 尺寸 600x400
•  绘制：轨道（底部直线）、小车（矩形）、杆子（旋转线段）
•  使用 requestAnimationFrame 平滑动画

3. ControlPanel 组件
•  按钮：开始训练、停止训练、重置
•  显示：当前回合、累计奖励、ε 值

4. TrainingChart 组件
•  使用 Recharts 的 LineChart
•  X轴：回合数，Y轴：总奖励
•  实时更新数据

5. WebSocket 连接
•  自定义 useWebSocket hook
•  自动重连机制
•  解析消息更新 Canvas 状态

依赖

后端：
•  fastapi, uvicorn, websockets
•  torch (PyTorch)
•  numpy

前端：
•  react, typescript
•  recharts
•  vite

运行方式

bash
# 后端
cd backend && pip install -r requirements.txt && uvicorn main:app --reload

# 前端
cd frontend && npm install && npm run dev

预计总代码量约 800-1000 行，可在 1-2 小时内完成。
```

选择 **Proceed + Auto (Medium)** 让 Droid 自动执行。

![审查并批准计划](https://neardws.com/images/posts/vibe-coding/CleanShot 2026-01-20 at 22.25.44@2x.png)
*审查并批准计划*

### 步骤 4：观察 AI 编码

Droid 会自动创建文件，你可以实时观察：

**后端核心代码示例（AI 生成）：**

```python
# backend/env/cartpole.py
import numpy as np

class CartPoleEnv:
def __init__(self):
self.gravity = 9.8
self.cart_mass = 1.0
self.pole_mass = 0.1
self.pole_length = 0.5
self.force_mag = 10.0
self.tau = 0.02  # 时间步长

self.state = None
self.reset()

def reset(self):
# 随机初始化状态 [x, x_dot, theta, theta_dot]
self.state = np.random.uniform(-0.05, 0.05, size=(4,))
return self.state.copy()

def step(self, action):
x, x_dot, theta, theta_dot = self.state
force = self.force_mag if action == 1 else -self.force_mag

# 物理模拟（简化欧拉法）
cos_theta, sin_theta = np.cos(theta), np.sin(theta)
total_mass = self.cart_mass + self.pole_mass

temp = (force + self.pole_mass * self.pole_length * theta_dot**2 * sin_theta) / total_mass
theta_acc = (self.gravity * sin_theta - cos_theta * temp) / (
self.pole_length * (4/3 - self.pole_mass * cos_theta**2 / total_mass)
)
x_acc = temp - self.pole_mass * self.pole_length * theta_acc * cos_theta / total_mass

# 更新状态
x += self.tau * x_dot
x_dot += self.tau * x_acc
theta += self.tau * theta_dot
theta_dot += self.tau * theta_acc

self.state = np.array([x, x_dot, theta, theta_dot])

# 判断是否结束
done = abs(x) > 2.4 or abs(theta) > 0.21  # 约12度
reward = 1.0 if not done else 0.0

return self.state.copy(), reward, done
```

**前端可视化示例（AI 生成）：**

```tsx
// frontend/src/components/CartPoleCanvas.tsx
import { useEffect, useRef } from 'react';

interface GameState {
x: number;
theta: number;
reward: number;
episode: number;
}

export function CartPoleCanvas({ state }: { state: GameState }) {
const canvasRef = useRef(null);

useEffect(() => {
const canvas = canvasRef.current;
if (!canvas) return;

const ctx = canvas.getContext('2d')!;
const width = canvas.width;
const height = canvas.height;

// 清空画布
ctx.fillStyle = '#1a1a2e';
ctx.fillRect(0, 0, width, height);

// 坐标转换
const scale = 100;
const cartX = width / 2 + state.x * scale;
const cartY = height - 50;
const cartWidth = 60;
const cartHeight = 30;
const poleLength = 100;

// 绘制轨道
ctx.strokeStyle = '#4a4a6a';
ctx.lineWidth = 3;
ctx.beginPath();
ctx.moveTo(0, cartY + cartHeight / 2);
ctx.lineTo(width, cartY + cartHeight / 2);
ctx.stroke();

// 绘制小车
ctx.fillStyle = '#00d4ff';
ctx.fillRect(cartX - cartWidth / 2, cartY - cartHeight / 2, cartWidth, cartHeight);

// 绘制杆子
const poleEndX = cartX + Math.sin(state.theta) * poleLength;
const poleEndY = cartY - Math.cos(state.theta) * poleLength;

ctx.strokeStyle = '#ff6b6b';
ctx.lineWidth = 8;
ctx.lineCap = 'round';
ctx.beginPath();
ctx.moveTo(cartX, cartY - cartHeight / 2);
ctx.lineTo(poleEndX, poleEndY);
ctx.stroke();

// 绘制信息
ctx.fillStyle = '#ffffff';
ctx.font = '16px monospace';
ctx.fillText(`Episode: ${state.episode}`, 10, 25);
ctx.fillText(`Reward: ${state.reward.toFixed(1)}`, 10, 50);

}, [state]);

return ;
}
```

### 步骤 5：迭代优化

训练效果不理想？继续与 Droid 对话：

```
训练了 100 回合但杆子还是很快倒下，请帮我：
1. 检查奖励函数设计是否合理
2. 调整神经网络结构或超参数
3. 添加奖励曲线的移动平均线便于观察趋势
```

Droid 会分析问题并提出改进：

```
分析发现几个问题：

1. **奖励稀疏** - 只在存活时给 +1，改为：
- 基础存活奖励 +1
- 角度接近垂直额外奖励
- 位置接近中心额外奖励

2. **学习率过高** - 从 0.001 降到 0.0005

3. **探索不足** - epsilon 衰减太快，调整为 500 回合衰减

正在应用修改...
```

### 步骤 6：运行和验证

```bash
项目已完成！结构如下：

cartpole-rl/
├── backend/
│   ├── main.py              # FastAPI 入口 + WebSocket
│   ├── cartpole_env.py      # CartPole 物理模拟
│   ├── dqn_agent.py         # DQN 神经网络 + 经验回放
│   ├── training_manager.py  # 后台训练线程管理
│   └── requirements.txt
└── frontend/
└── src/
├── App.tsx
├── components/       # Canvas、控制面板、图表
├── hooks/            # WebSocket hook
└── api/              # REST API 调用

运行方式：

bash
# 终端 1 - 后端
cd backend
pip install -r requirements.txt
python main.py

# 终端 2 - 前端
cd frontend
npm run dev

然后访问 http://localhost:5173，点击 "Start Training" 开始 DQN 训练，可视化会实时显示小车平衡杆的状态和训练曲线。
```

打开浏览器访问 `http://localhost:5173`，观看 AI 学习保持杆子直立！

![CartPole DQN Training](https://neardws.com/images/posts/vibe-coding/CleanShot 2026-01-20 at 22.35.01.gif)
*CartPole DQN Training*

### 完整项目结构

```
cartpole-rl/
├── backend/
│   ├── main.py              # FastAPI 入口
│   ├── requirements.txt
│   ├── env/
│   │   └── cartpole.py      # 环境模拟
│   └── agent/
│       ├── dqn.py           # DQN 算法
│       └── replay_buffer.py # 经验回放
├── frontend/
│   ├── package.json
│   ├── src/
│   │   ├── App.tsx
│   │   ├── components/
│   │   │   ├── CartPoleCanvas.tsx
│   │   │   ├── ControlPanel.tsx
│   │   │   └── RewardChart.tsx
│   │   └── hooks/
│   │       └── useWebSocket.ts
│   └── vite.config.ts
└── README.md
```

### 关键收获

通过这个示例，你体验了 Vibe Coding 的完整流程：

| 阶段 | 传统开发 | Vibe Coding |
| --- | --- | --- |
| 需求分析 | 手动编写文档 | 自然语言描述，AI 生成计划 |
| 架构设计 | 手动画图设计 | Spec Mode 迭代确认 |
| 编码实现 | 逐行编写代码 | AI 生成，人工审查 |
| 调试优化 | 手动分析问题 | 描述问题，AI 定位修复 |
| 测试验证 | 手动编写测试 | AI 生成测试用例 |

**从零到可运行的全栈 RL 项目，整个过程可能只需要 30 分钟！**

---

## 9. 总结与资源

### 总结

通过本教程，你已经学会了：

1. ✅ 配置现代化终端（Kitty/Warp）
2. ✅ 美化 Shell 环境（Oh-My-Zsh + Powerlevel10k）
3. ✅ 安装和配置 Factory Droid
4. ✅ 选择合适的 LLM 模型（BYOK）
5. ✅ 使用 Skills 增强 AI 能力
6. ✅ 配置 MCP 扩展功能
7. ✅ 创建 Custom Droids

### 相关资源

**终端工具**

- Kitty 终端 - GPU 加速的现代终端
- Warp 终端 - 内置 AI 的现代终端
- Kitty Themes - Kitty 主题集合
- Kitty Config - 自定义 Kitty 配置

**Shell 配置**

- Oh-My-Zsh - Zsh 配置管理框架
- Powerlevel10k - Zsh 主题
- Nerd Fonts - 编程字体图标

**AI 编程工具**

- Factory Droid - AI 编程 CLI 工具
- Factory Droid 文档
- Claude Code - Anthropic 官方 CLI
- OpenAI Codex CLI
- Gemini CLI - Google 官方 CLI
- OpenCode - 多模型支持 CLI

**LLM 模型**

- Claude Opus 4.5
- Claude Sonnet 4.5
- GPT-5.2
- Gemini 3 Flash
- DeepSeek-V3.2
- SWE-Rebench - LLM 编程能力排行榜

**Skills 与扩展**

- Agent Skills - 社区 Skills 平台
- Superpowers - Skills 套件
- Planning With Files - 文件化规划 Skill
- Awesome Claude Skills
- Droid Skills - 预配置 Skills 集合

**MCP 协议**

- MCP 官方文档
- Smithery - MCP Server 市场

**字体**

- Berkeley Mono - 编程字体
- Maple Mono CN - 中文等宽字体

**延伸阅读**

- Vibe Coding - Wikipedia
- Simon Willison: Not all AI-assisted programming is vibe coding
- Andrej Karpathy (X/Twitter)

### 下一步

- 探索更多 Skills 和 Custom Droids
- 根据 SWE-Rebench 数据尝试不同模型
- 为你的特定工作流创建自定义配置

---

> 🎉 恭喜你完成了 Vibe Coding 环境的配置！开始享受 AI 辅助编程的乐趣吧！

*最后更新：2025年1月21日*

---