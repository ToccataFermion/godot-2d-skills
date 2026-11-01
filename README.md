# Godot 2D Skills 合集

面向 **Godot 4.x 2D 游戏开发**的 AI Agent 技能合集。从 7 个上游开源仓库整理而来，剔除引擎无关项、Unity/虚幻技能与付费服务依赖，统一冲突命名，共 **234 个技能**。

目的很直接：让你不必在几十个仓库间逐页翻找，直接拿到一套能覆盖 2D 游戏全生命周期的技能，并且清楚每个技能该在什么时候用。

## 这个合集解决什么问题

上游仓库各自完整，但混在一起用会出现三类摩擦，这里已经处理完：

| 摩擦 | 具体表现 | 本合集的处置 |
|---|---|---|
| 同名技能互相覆盖 | `godot-*` 系列在两个包中各有一套；`export-pipeline` 分属 Godot 与 Blender | 逐项裁决，见 [冲突裁决](#冲突裁决) |
| 平台不相关技能占位 | 跨引擎包内含 14 个 Unity / 虚幻技能 | 全部删除 |
| 付费服务硬依赖 | Scenario 资产包必须配置付费 API Key 才能运行 | 整包剔除，见 [剔除说明](#剔除说明) |

此外补入了 Game-Studios 的支撑脚本，让它 43 个依赖 `.claude/scripts/` 的技能不是空壳。

## 收录内容

| 来源包 | 技能数 | 许可证 | 定位 |
|---|---|---|---|
| [GodotPrompter](https://github.com/jame581/GodotPrompter) | 58 | MIT | **2D 主力**：Godot 4.x 纵深手册，含引擎 API、架构模式、插件生态 |
| [awesome-gamedev-agent-skills](https://github.com/gamedev-skills/awesome-gamedev-agent-skills) | 64 | Apache-2.0 | **调度骨架**：`router` 引擎识别 + 引擎中立的学科/类型/工作流方法论 |
| [game-ui-design-workflow](https://github.com/guiguiyan930-source/game-ui-design-workflow) | 7 | MIT | UI 规范 → 整页生成 → 组件拆分 → 切图 → 图集打包 |
| [novel-to-game](https://github.com/zenstory-ai/novel-to-game) | 7 | MIT | 小说改编为可玩游戏的证据驱动流水线 |
| [blender-skills](https://github.com/arjun988/blender-skills) | 23 | MIT | Blender 建模、雕刻、绑定、贴图、导出（2.5D / 三维渲染序列帧用） |
| [Claude-Code-Game-Studios](https://github.com/Donchitos/Claude-Code-Game-Studios) | 74 | MIT | 工作室流程：立项、拆解、冲刺、QA、发布 |

完整技能列表含每个技能的描述：[SKILLS.md](SKILLS.md)

## 安装

技能是纯文本（`SKILL.md` + 可选 `references/`），任何支持读取本地文件的 Agent 都能用。选与你工具对应的方式：

### Claude Code

```bash
# 全局可用
git clone https://github.com/<你的账号>/godot-2d-skills.git
cp -r godot-2d-skills/skills/* ~/.claude/skills/

# 或仅当前项目可用（推荐，便于随项目版本化）
mkdir -p .claude && cp -r godot-2d-skills/skills .claude/skills
```

Game-Studios 的技能依赖仓库内的 `.claude/scripts/`，若要用它，把 `.claude/` 整个目录复制到项目根目录，而不是只复制 `skills/`。

### magc

```bash
cp -r godot-2d-skills/skills/* ~/.magc/skills/
```

### Cursor 及其他 Agent

把 `skills/` 放进项目内任意位置，在规则文件里指明「技能位于 `skills/`，按需读取对应 `SKILL.md`」。多数 Agent 会依据 `SKILL.md` 的 `description` 字段自行判断该读哪个。

### 按需精简

不必全量安装。只做 Godot 2D 的话，`godot-*`、`2d-essentials`、`gdscript-*`、`game-feel`、`platformer` 等约 40 个就够跑通一个项目。完整清单见 [Godot 2D 快速索引](#godot-2d-快速索引)。

## 用法

技能不会自动生效，需要 Agent 读取对应 `SKILL.md`。两种触发方式：

**自动路由** — 先读 `router`，它会扫描项目识别引擎（见到 `project.godot` 即锁定 Godot），再把你的需求分类并列出该读哪些技能。适合不确定该用什么的时候。

**直接点名** — 明确知道要做什么时，直接让 Agent 读特定技能。例如「读 `skills/godot-2d-movement/SKILL.md`，实现玩家左右移动和跳跃」。比自动路由少一步，也更准。

一个典型 2D 项目的技能使用顺序：

```
立项期      router → platformer（系统清单）→ level-design
    ↓
搭地基      godot-project-setup → gdscript-patterns → event-bus / component-system
    ↓
做玩法      godot-2d-movement → godot-physics → godot-tilemap → animation-system
    ↓
做手感      game-feel → camera-systems → input-handling
    ↓
做界面      godot-ui → hud-system → game-ui-workflow（要出美术图时）
    ↓
做敌人      ai-navigation → beehave / limboai → game-ai
    ↓
收尾        godot-testing → godot-debugging → godot-optimization
    ↓
出包        export-pipeline → itch-publish / steam-publish
```

## Godot 2D 快速索引

按你当下要做的事查表。

### 项目起步与代码架构

| 要做的事 | 技能 |
|---|---|
| 新建项目、目录结构、项目设置 | `godot-project-setup` |
| 不知道从哪开始、该用哪些技能 | `router` |
| 判断项目当前处于什么阶段 | `project-stage-detect`、`start` |
| 写规范 GDScript（静态类型、生命周期、注解） | `godot-gdscript` |
| 常用写法与设计模式 | `gdscript-patterns` |
| 高级特性（协程、元编程、RefCounted） | `gdscript-advanced` |
| 节点与场景组织 | `godot-nodes-scenes` |
| 信号与分组 | `godot-signals-groups` |
| 自定义 Resource 做数据驱动 | `godot-resources` |
| 解耦全局消息 | `event-bus` |
| 组合优于继承 | `component-system` |
| 依赖注入 | `dependency-injection` |
| 数值与向量数学 | `math-essentials` |

### 2D 核心玩法

| 要做的事 | 技能 |
|---|---|
| TileMap、视差、2D 光照、canvas 层、2D 粒子 | `2d-essentials` |
| 玩家移动（平台跳跃 / 俯视八向、斜坡、碰撞读取） | `godot-2d-movement` |
| 瓦片地形自动过渡、无缝地形 | `godot-tilemap` |
| 碰撞体、射线、物理层掩码 | `godot-physics` |
| 物理手感调校 | `physics-tuning` |
| 精灵动画与 AnimationPlayer | `animation-system`、`godot-animation` |
| 2D 着色器与后处理 | `godot-shaders`、`shader-programming` |
| 输入映射与设备切换 | `input-handling`、`input-systems` |
| 相机跟随、死区、前瞻、震屏 | `camera-systems`、`camera-system` |
| 打击感、顿帧、挤压拉伸、击退 | `game-feel` |
| 程序化生成关卡与内容 | `procedural-gen` |

### 玩法系统

| 要做的事 | 技能 |
|---|---|
| 背包与物品 | `inventory-system` |
| 技能、冷却、buff、状态加成 | `ability-system` |
| 对话与分支叙事 | `dialogue-manager`（Dialogue Manager）、`dialogue-system`（Dialogic）、`dialogue-systems`（引擎中立方法论） |
| 存档与设置持久化 | `save-systems` |
| 音频总线、混音、动态音乐 | `audio-system`、`audio-design`、`godot-audio` |
| 多语言 | `localization`、`localize` |
| 联机 | `godot-multiplayer`、`dedicated-server` |

### 敌人 AI

| 要做的事 | 技能 |
|---|---|
| 寻路 | `ai-navigation` |
| 行为树插件（Beehave / LimboAI） | `beehave`、`limboai` |
| 行为树与效用 AI 原理 | `ai-behavior-trees-utility-ai` |
| 状态机、转向、A* 算法层 | `game-ai` |

### 界面

| 要做的事 | 技能 |
|---|---|
| Control 节点与布局 | `godot-ui`、`godot-ui-control` |
| HUD 与血条 | `hud-system` |
| 锚点响应式布局、分辨率与安全区 | `game-ui-ux` |
| UI 规范、整页设计、组件拆分、切图、图集与九宫格 | `game-ui-workflow` → `game-ui-specification` → `game-ui-page-generator` → `game-ui-component-breakdown` → `game-ui-sprite-sheet-splitter` → `game-ui-asset-pipeline` |

### 类型模板

挑一个最接近的，它给出该类型的完整系统清单与拼装路线。

`platformer` · `roguelike` · `rpg` · `tower-defense` · `card-game` · `puzzle` · `visual-novel` · `survival-crafting`

俯视（top-down）没有独立类型技能，参考 `rpg` 的移动与视角章节，配合 `godot-2d-movement` 的八向移动部分。

### 测试、优化与发布

| 要做的事 | 技能 |
|---|---|
| 单元测试 | `godot-testing` |
| 无头 CI 测试 | `godot-gdscript-headless-testing` |
| 调试手段 | `godot-debugging` |
| 渲染与绘制调用优化 | `godot-optimization` |
| 性能剖析 | `perf-profile` |
| 导出预设与平台配置 | `export-pipeline`、`godot-export` |
| GitHub Actions 自动出包 | `export-pipeline` |
| 上架 itch.io / Steam | `itch-publish`、`steam-publish` |

### 工程管理（按需，小团队多数用不上）

`vertical-slice`（先做纵向切片验证玩法）、`scope-check`（防止范围失控）、`prototype`、`playtest-report`、`balance-check`、`bug-triage`、`release-checklist`、`code-review`、`godot-code-review`、`retrospective`、`tech-debt`。

### 学习与自查

`godot-mentor`（概念答疑）、`godot-grill`（代码拷问找问题）、`godot-brainstorming`（玩法头脑风暴）、`brainstorm`。

## 冲突裁决

同名技能只保留一个版本，裁决原则是**保留更深入、更贴合 Godot 版本差异的那一份**。

| 技能 | 冲突来源 | 保留 | 理由 |
|---|---|---|---|
| `godot-*` 共 9 个（`godot-gdscript`、`godot-physics`、`godot-tilemap`、`godot-animation` 等） | GodotPrompter vs awesome-gamedev | **GodotPrompter** | 带明确版本基线（4.3+ / 4.7）、含 GDScript 与 C# 双实现、篇幅与示例更完整；跨引擎版为精简摘要 |
| `export-pipeline` | GodotPrompter vs blender-skills | 两个都留 | 语义完全不同。Godot 版保留原名，Blender 版改名 `blender-export-pipeline` |
| `camera-system` / `camera-systems`、`audio-system` / `audio-design`、`input-handling` / `input-systems`、`dialogue-system` / `dialogue-manager` / `dialogue-systems`、`localization` / `localize` | 不同包的同义技能 | 全部保留 | 名称本就不同，未互相覆盖。语义边界：`*-system` 多为 Godot 具体实现，`*-systems` / `-design` 多为引擎中立方法论，建议先读方法论再读实现 |

`dialogue-*` 三个技能的区分：`dialogue-manager` 对应 Dialogue Manager 插件，`dialogue-system` 对应 Dialogic 插件，`dialogue-systems` 是不绑定插件的对话系统设计方法。

## 剔除说明

### 付费服务依赖（已整包剔除）

原 Scenario 资产包（`scenario-labs/skills`，56 个技能）**未收录**。它的每个技能都通过 Scenario MCP 调用云端模型生成图像、视频、音频，必须配置付费账号与 API Key，`model_run` 按次计费，无 Key 时整包不可用。为保证本合集开箱即用，不予收录。

若你确实有 Scenario 账号，可自行安装：`https://github.com/scenario-labs/skills`。

替代方案：`create-game-assets`（引擎中立的资产生成与规范化方法论）、`game-ui-workflow` 系列（UI 资产，前半段规范与切图环节不依赖付费服务）。

### 平台不相关（已删除）

跨引擎包内的 8 个 `unity-*` 与 6 个 `unreal-*` 技能全部删除。`3d-essentials`、`godot-3d-essentials` 予以保留但对纯 2D 项目无用，做 2.5D 时可参考。

## 已知限制

**Game-Studios 的技能依赖仓库内脚本。** 它的 74 个技能中，43 个会调用 `.claude/scripts/*.sh`（如 `md-section.sh`、`gate-check` 的校验脚本）读取项目状态。本合集已补齐 `.claude/scripts`、`.claude/hooks`、`.claude/rules`、`.claude/agents` 四个目录，但脚本原本设计为在项目根目录的 `.claude/` 下运行 —— 安装时请按上文把 `.claude/` 复制到项目根，而非塞进全局技能目录，否则路径解析会失败。纯文档类技能（`vertical-slice`、`scope-check`、`release-checklist` 等）不受影响。

**references 有少量缺档。** 上游 `novel-to-game` 的 3 个大型参考文件（`game-writing-craft.md`、`dialogue-design-method.md`、`intake-benchmark-reference.md`）在下载阶段因网络问题多次重试仍失败，对应技能主体可用，仅深度参考材料缺失。

**版本基线。** 本合集锁定的是**抓取当日**各仓库默认分支的内容，未固定 commit。上游更新不会自动同步进你的副本。GodotPrompter 与跨引擎包的 API 基线为 Godot 4.3+ / 4.7，用于更早版本时需自行核对 API。

## 目录结构

```
godot-2d-skills/
├── README.md                  本文档
├── SKILLS.md                  全部 234 个技能清单（含描述）
├── COMPLIANCE.md              许可证与合规说明
├── LICENSE                    本合集整理工作采用 MIT
├── skills/                    234 个技能
│   ├── router/
│   │   ├── SKILL.md           技能主体
│   │   └── references/        按需加载的深度材料
│   ├── godot-2d-movement/
│   └── ...
├── .claude/                   Game-Studios 的支撑脚本（可选）
│   ├── scripts/
│   ├── hooks/
│   ├── rules/
│   └── agents/
└── licenses/                  上游原始许可证全文
```

## 合规

收录的 6 个仓库许可证为 MIT（5 个）与 Apache-2.0（1 个），均允许再分发与修改。所有原始许可证全文归档在 `licenses/`，各技能的来源与作者归属见 [SKILLS.md](SKILLS.md) 与 [COMPLIANCE.md](COMPLIANCE.md)。

**本合集的整理工作**（筛选、冲突裁决、文档编写、缺陷修复）采用 MIT 许可证。**各技能内容**的著作权归原作者，遵循其各自许可证。二次分发时请保留 `licenses/` 目录。

## 上游仓库

| 仓库 | 星标 | 许可证 |
|---|---|---|
| [Donchitos/Claude-Code-Game-Studios](https://github.com/Donchitos/Claude-Code-Game-Studios) | 31.8k | MIT |
| [jame581/GodotPrompter](https://github.com/jame581/GodotPrompter) | 912 | MIT |
| [gamedev-skills/awesome-gamedev-agent-skills](https://github.com/gamedev-skills/awesome-gamedev-agent-skills) | 6.4k | Apache-2.0 |
| [zenstory-ai/novel-to-game](https://github.com/zenstory-ai/novel-to-game) | 952 | MIT |
| [guiguiyan930-source/game-ui-design-workflow](https://github.com/guiguiyan930-source/game-ui-design-workflow) | 380 | MIT |
| [arjun988/blender-skills](https://github.com/arjun988/blender-skills) | 1.6k | MIT |

星标数为抓取时数据。

## 贡献

上游技能的改进请直接提交至对应上游仓库，这样能惠及更多人。本仓库只处理三类问题：收录范围调整、冲突裁决争议、文档与结构修正。

## 免责

本合集仅为开源技能的整理与索引，不对技能内容的正确性、安全性作担保。技能中的脚本会在你的项目目录执行，使用前请自行审阅。
