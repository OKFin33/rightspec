# Change Spec: Publish rightspec to GitHub

## Purpose

将 rightspec 从本地文件包发布为公开的 GitHub repository，使其可被发现、安装和使用。

## Executor / Preconditions

**Executor**: 人类（repo 创建和 git 操作需要 GitHub 账户权限）。
**Must read before executing**: 本 spec + rightspec/ 目录的完整内容。

## Execution Order and Dependencies

Standalone。无外部依赖。

## Definitions

- **Agent Skills standard**: agentskills.io 定义的开放标准，SKILL.md + YAML frontmatter 格式，被 Claude Code、OpenClaw、VS Code Copilot、OpenAI Codex 等采用。
- **ClawHub**: OpenClaw 的公共 skill 注册表，类似 npm，通过 PR 到 github.com/openclaw/clawhub 发布。
- **GitHub topics**: repo 页面的标签，影响搜索发现。

## Change List

### PUB-01: 创建 GitHub repository

**Operation**: 手动操作

**Content**:
1. 在 GitHub 上创建新的 public repository，名称 `rightspec`
2. Description 填写: `Write specs and handoffs that AI agents can follow — without guessing what you meant.`
3. License 选择 MIT
4. 不要初始化 README（本地已有）

### PUB-02: 推送本地文件

**Operation**: 命令行操作

**Content**:
```bash
cd rightspec/
git init
git add .
git commit -m "v2.0: initial public release"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/rightspec.git
git push -u origin main
```

### PUB-03: 设置 repository metadata

**Operation**: GitHub web UI

**Content**:
1. 进入 repo Settings → 确认 visibility 为 Public
2. 在 repo 主页点击齿轮图标（About 区域右侧），设置：
   - Description: `Write specs and handoffs that AI agents can follow — without guessing what you meant.`
   - Website: 留空（暂无）
   - Topics 添加: `agent-skills`, `specification`, `handoff`, `zero-context`, `agents-md`, `markdown`, `ai-agent`, `openclaw`, `claude-code`, `spec-driven-development`
3. 勾选 "Releases"、"Packages" 如果有的话

### PUB-04: 创建 Release

**Operation**: GitHub web UI 或 CLI

**Content**:
1. 在 repo 页面点击 "Releases" → "Create a new release"
2. Tag: `v2.0`
3. Release title: `v2.0 — Initial Public Release`
4. Description:

```
rightspec helps you write specs and handoff documents that survive the transfer — when the next reader has zero access to your head, your chat history, or your "obvious" context.

## What's included

- **SKILL.md**: Core principles, process, and conventions for writing zero-context executable specs
- **Templates**: Full spec template, change spec template (for document modifications), skeleton template
- **Review checklist**: 30+ audit criteria including change spec–specific checks
- **Worked examples**: Agent-to-agent data handoff + document modification spec
- **Design decisions log**: Why every design choice was made, with evidence

## Platforms

Works with any platform supporting the Agent Skills standard (agentskills.io):
Claude Code, OpenClaw, VS Code / GitHub Copilot, OpenAI Codex CLI, and others.

## Quick install

Clone into your agent's skill directory and start using it immediately.
See README for platform-specific paths.
```

5. 附件：上传 rightspec.zip（方便不想 clone 的用户）

### PUB-05: 更新 README 中的 YOUR_USERNAME

**Operation**: 文本替换

**Content**: 在 README.md 中将所有 `YOUR_USERNAME` 替换为实际的 GitHub 用户名。共 4 处（Installation 段落的三个平台路径 + OpenClaw 路径）。

**Rationale**: *Design note* — README 里的 git clone URL 在本地起草时用占位符，发布时必须替换为真实 URL，否则用户 clone 会失败。

### PUB-06: ClawHub 发布

**Operation**: 命令行操作

**Content**:
```bash
clawhub publish ./rightspec --slug rightspec --name "rightspec" --version 2.0.0 --tags "specification,handoff,zero-context,productivity" --changelog "Initial public release"
```

**Rationale**: ClawHub 提供向量搜索和一键安装，增加可见性。

### PUB-07: 社区分发 (Community Awareness)

**Operation**: PR / Submission

**Content**:
1. **GitHub Awesome Lists**: 向以下仓库提交 PR，将 `rightspec` 加入其 Skills 列表：
   - `travisvn/awesome-claude-skills`
   - `alirezarezvani/claude-skills`
   - `jeremylongshore/claude-code-plugins-plus-skills`
2. **SkillsMP**: 访问 `skillsmp.com` 并提交 your repository URL。
3. **Claude-plugins.dev**: 如果该平台支持提交，进行登记。



## Output Contract

**Deliverable**: 一个公开的、可被搜到的、可被 clone 安装的 GitHub repository。
**Requirements**: README 可读且无占位符残留。Release 存在且可下载。Topics 已设置。

## Failure Handling

- **GitHub 用户名未确定**: 发布前必须确定用户名或组织名。如果犹豫，先用个人账号，以后可以 transfer。
- **README 中 YOUR_USERNAME 残留**: 发布后全文搜索 `YOUR_USERNAME`，确认零匹配。
- **zip 包过时**: 如果发布前对 rightspec 做了最后修改，重新打 zip 再上传到 Release。

## Evaluation Checklist

- [ ] PUB-01: Repository 存在且为 public
- [ ] PUB-02: 所有文件已推送，目录结构完整
- [ ] PUB-03: Description、Topics 已设置（至少 8 个 topics）
- [ ] PUB-04: v2.0 Release 存在，description 完整，zip 已上传
- [ ] PUB-05: README 中无 `YOUR_USERNAME` 残留
- [ ] PUB-06: ClawHub 发布成功 (可选)
- [ ] PUB-07: 已向至少一个社区仓库/注册表提交 PR 或登记
- [ ] 访问 repo 页面，README 正常渲染
- [ ] SKILL.md 在 repo 中可直接阅读
- [ ] Installation 段落的 git clone 命令可直接复制使用
