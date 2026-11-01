# 合规与许可证说明

本合集收录的每个技能都来自公开开源仓库。此文档说明来源、许可证、归属与再分发要求。

## 一、上游许可证

| 上游仓库 | 技能数 | 许可证 | 允许商用 | 允许再分发 | 要求保留版权声明 |
|---|---|---|---|---|---|
| [Donchitos/Claude-Code-Game-Studios](https://github.com/Donchitos/Claude-Code-Game-Studios) | 74 | MIT | 是 | 是 | 是 |
| [jame581/GodotPrompter](https://github.com/jame581/GodotPrompter) | 58 | MIT | 是 | 是 | 是 |
| [gamedev-skills/awesome-gamedev-agent-skills](https://github.com/gamedev-skills/awesome-gamedev-agent-skills) | 64 | Apache-2.0 | 是 | 是 | 是，且需保留 NOTICE |
| [zenstory-ai/novel-to-game](https://github.com/zenstory-ai/novel-to-game) | 7 | MIT | 是 | 是 | 是 |
| [guiguiyan930-source/game-ui-design-workflow](https://github.com/guiguiyan930-source/game-ui-design-workflow) | 7 | MIT | 是 | 是 | 是 |
| [arjun988/blender-skills](https://github.com/arjun988/blender-skills) | 23 | MIT | 是 | 是 | 是 |

许可证信息取自各仓库的 `LICENSE` 文件及 GitHub 仓库元数据（抓取当日核实）。

原始许可证全文归档于 [`licenses/`](licenses/) 目录：

```
licenses/
├── Claude-Code-Game-Studios.LICENSE              MIT
├── GodotPrompter.LICENSE                         MIT
├── awesome-gamedev-agent-skills.LICENSE          Apache-2.0
├── awesome-gamedev-agent-skills.NOTICE           Apache-2.0 要求的 NOTICE 文件
├── game-ui-design-workflow.LICENSE               依据仓库元数据（MIT）
├── novel-to-game.LICENSE                         依据仓库元数据（MIT）
└── blender-skills.LICENSE                        依据仓库元数据（MIT）
```

> `game-ui-design-workflow`、`novel-to-game`、`blender-skills` 三个仓库未在仓库根目录提供 `LICENSE` 文件，但 GitHub API 元数据均标记为 MIT License。为稳妥起见，本文档明确记录这一事实，建议在引用前自行向上游仓库确认。

## 二、MIT 许可证要求

MIT 的核心义务只有一条：**保留版权声明与许可声明**。

具体到本合集，再分发时需要：

1. 保留 `licenses/` 目录下对应上游的许可证全文
2. 保留各技能 `SKILL.md` 中的原始内容（含作者署名，若原文有）
3. 不得移除本文件与 README 中的来源标注

MIT 允许修改、合并、再发布、商用、私有化，无 copyleft 传染性。

## 三、Apache-2.0 额外要求

`awesome-gamedev-agent-skills` 的 64 个技能使用 Apache-2.0，在 MIT 义务之外还需：

1. **保留 NOTICE 文件** —— 已归档为 `licenses/awesome-gamedev-agent-skills.NOTICE`，再分发时不可删除
2. **标注修改** —— 本合集对该包做了两项修改，下文「四、本合集所做的修改」已明确记录
3. **保留许可证副本** —— 已归档
4. **商标与专利** —— Apache-2.0 含专利授权条款，但不授予商标使用权。使用时不得暗示上游作者为本合集背书

## 四、本合集所做的修改

### 4.1 Apache-2.0 包（awesome-gamedev-agent-skills，64 个技能）

| 修改 | 说明 |
|---|---|
| 删除 Unity / 虚幻技能 | 移除 `skills/unity/`（8 个）与 `skills/unreal/`（6 个）共 14 个技能，其余 64 个保留 |
| 删除重名技能 | 9 个 `godot-*` 技能因与 GodotPrompter 同名，采用后者版本，本包对应技能未收录。详见 README「冲突裁决」 |
| 目录扁平化 | 原始目录为 `skills/<分类>/<技能名>/`，本合集统一为 `skills/<技能名>/`，技能内容未作改动 |

**技能文件内容本身未作任何编辑。**

### 4.2 MIT 包

| 包 | 修改 | 说明 |
|---|---|---|
| GodotPrompter（58） | 无内容修改 | 仅目录层级由 `skills/<技能名>/` 原样保留。部分技能因同名覆盖了跨引擎包版本 |
| Claude-Code-Game-Studios（74） | 补充支撑目录 | 技能的 `.claude/scripts/` 等依赖在源仓库中位于 `.claude/` 而非 `skills/` 内，本合集补齐 `.claude/scripts`、`hooks`、`rules`、`agents` 四个目录，使技能可运行 |
| blender-skills（23） | 重命名 1 个技能 | `export-pipeline` 改名为 `blender-export-pipeline`，以与同名的 Godot 技能区分。仅改目录名，`SKILL.md` 内容未动 |
| novel-to-game（7） | 缺档标注 | 3 个 `references/*.md` 因网络问题未能获取，已在 README「已知限制」中说明 |
| game-ui-design-workflow（7） | 无内容修改 | 取自 `v0.3.1` 版本标签 |

升级说明：本合集锁定抓取当日各仓库默认分支，未固定 commit。上游后续变更不会自动同步。

## 五、未收录的内容

| 内容 | 原仓库 | 技能数 | 未收录原因 |
|---|---|---|---|
| Scenario 资产包 | `scenario-labs/skills` | 56 | 所有技能均需 Scenario 付费账号与 API Key，按次计费，无 Key 时整包不可用。与「开箱即用」目标冲突 |
| Unity 技能 | awesome-gamedev-agent-skills | 8 | 目标平台为 Godot |
| 虚幻技能 | awesome-gamedev-agent-skills | 6 | 目标平台为 Godot |

上述内容均为 MIT 许可，如需使用可直接从上游安装，不受本合集影响。

## 六、本合集自身的许可

本合集的**整理工作** —— 即筛选范围、冲突裁决、目录结构设计、README 与本文档的撰写、依赖修复 —— 采用 **MIT 许可证**，见根目录 [`LICENSE`](LICENSE)。

各**技能内容**的著作权归原作者所有，遵循其各自的 MIT 或 Apache-2.0 许可证，不受本合集 LICENSE 覆盖。

## 七、使用建议

1. **商用无碍** —— MIT 与 Apache-2.0 均允许商业使用，可用于商业游戏项目
2. **保留归属** —— 在你的项目或产品中保留 `licenses/` 目录与本文件
3. **审阅脚本** —— 技能内的 shell 与 Python 脚本会在你的项目目录执行，首次使用前建议阅读内容
4. **不暗示背书** —— 不要以「上游官方推荐」等措辞宣传本合集
5. **改进回上游** —— 若你修复了某个技能的缺陷，建议向上游仓库提交 PR

## 八、联系方式

若你是上游作者，认为本合集的收录方式不妥，请提交 Issue，我们会尽快调整或移除相关内容。
