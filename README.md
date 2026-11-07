# novelist-skill

![version](https://img.shields.io/badge/version-0.2.0-blue)
![license](https://img.shields.io/badge/license-MIT-green)
![skill](https://img.shields.io/badge/Agent%20Skill-SKILL.md-8A2BE2)

A workflow skill for long-form Chinese novel writing — turn a few keywords into a confirmable,
checkable, portable novel framework, then write it chapter by chapter without losing consistency.

中文长篇小说写作流程 skill：**少关键词启动 → 约束 → 定调（明确故事·人物·世界）→ 施工（明确情节·章节·一致性）→ 试写 → 正文**，
并在写作期管住人物、时间线、伏笔与归档迁移。

---

## 这是什么

- **一条可确认的流水线**：每一步只产出一件东西、只过一道关，不满意就回退，不会写到一半推倒重来。
- **一套可验收的标准**：节拍配额、因果链三段、信息出场顺序、人物双栏检查、物证与数字表——把“感觉对不对”变成“查得出来”。
- **一份可迁移的存档**：压缩包 / 归档包 / 接续确认单，换台电脑、换个 Agent 能接着写。

它**保证**结构不犯低级错误（节点齐全、因果不断、伏笔能收、数字对得上），**不保证**写得好（语言辨识度、情感真实、原创眼光）。详见 [`SKILL.md`](skills/novelist-skill/SKILL.md) 模块 1.7。

---

## 安装

### 方式 1：Claude Code 插件（推荐）

在 Claude Code 里执行**两步**（注册市场 ≠ 安装插件，两步都要做）：

```text
/plugin marketplace add JaneKinsley/novelist-skill
/plugin install novelist-skill@novelist-skill
```

安装时会让你选 scope（user / project / local）。装完直接说“帮我写一本……”，或显式调用 `/novelist-skill:novelist-skill`。

> 更新方式：本仓库版本号 +1 后，执行 `/plugin update` 才会拉到新版本。

### 方式 2：手动放进 skills 目录（任何支持 Agent Skills 的客户端）

```bash
git clone --depth 1 https://github.com/JaneKinsley/novelist-skill.git /tmp/novelist-skill
mkdir -p ~/.claude/skills
cp -R /tmp/novelist-skill/skills/novelist-skill ~/.claude/skills/
```

Windows PowerShell：

```powershell
git clone --depth 1 https://github.com/JaneKinsley/novelist-skill.git "$env:TEMP\novelist-skill"
New-Item -ItemType Directory -Force "$env:USERPROFILE\.claude\skills" | Out-Null
Copy-Item -Recurse "$env:TEMP\novelist-skill\skills\novelist-skill" "$env:USERPROFILE\.claude\skills\"
```

只想要最小安装？`SKILL.md` 一个文件就够用；`templates/` 是工作区骨架，可以不要。

### 方式 3：其他 Agent（Codex / Cursor / 通用）

| 客户端 | 放这里 |
|---|---|
| 通用约定 | `<项目>/.agents/skills/novelist-skill/` |
| Codex | `<项目>/.codex/skills/novelist-skill/` |
| Cursor | `<项目>/.cursor/skills/novelist-skill/` |

目录名必须等于 `SKILL.md` frontmatter 里的 `name`（`novelist-skill`），且 `SKILL.md` 首行是 `---`。放完重开会话。

### 方式 4：不做 git，直接下载

仓库页 **Code → Download ZIP**，解压后把 `skills/novelist-skill/` 复制到你的 skills 目录即可。

### 没有文件系统的 Agent

把 [`SKILL.md`](skills/novelist-skill/SKILL.md) 模块 8.2 的“系统提示词原文”贴进 system prompt，即可降级为粘贴模式使用（无记账、无归档，长文一致性会打折）。

---

## 快速上手

```text
① 装好（上面任选一种）
② 说一句：题材 + 篇幅 + 禁忌
③ 它出约束清单 → 你说“确认” → 逐关推进
```

第一条消息可以直接抄：

```text
用 novelist-skill 开一本新书。
关键词：近未来，记忆可以租赁，主角是租赁公司的调查员；
冷峻短句，不要穿越；中篇，约 4 万字。
先出约束清单，等我确认。
```

预期回应：一张五列约束清单，然后停下问你“确认还是修改”。

| 阶段 | 产出 | 你要做的 |
|---|---|---|
| 约束 | 约束清单 | 增删改，说“确认”（C1） |
| 定调 | 定调包（故事·人物·世界） | 说“通过”，或指出要改的字段（G1） |
| 施工 | 施工包（情节·章节·一致性） | 同上（G2） |
| 试写 | 开篇一个场景 | 找人盲读三问（G3） |
| 正文 | 逐章正文 + 章后记账 | 说“开始写正文”（G4） |

---

## 目录结构

```text
novelist-skill/                     ← 本仓库 = 一个插件 = 一个市场
├── .claude-plugin/
│   ├── plugin.json                 插件元信息（name / version / description）
│   └── marketplace.json            市场目录（/plugin marketplace add 读它）
├── skills/novelist-skill/          ← 真正的 skill：安装时只需要这一层
│   ├── SKILL.md                    规范全文：模块 0—11 + 附录 A/B
│   ├── README.md                   详细导读：流程图、关卡表、FAQ
│   └── templates/                  工作区骨架（复制到小说项目后用）
├── README.md                       本文件
└── CHANGELOG.md
```

---

## 版本与更新

- 当前 **0.2.0**（2026-11-03）：新增 15 项写作约束，见 [CHANGELOG](CHANGELOG.md)。
- 装插件的人要在 version 变更后才拿到更新；手动安装的人 `git pull` 后覆盖目录即可。

## 许可

[MIT](LICENSE) © 2026 HJB
