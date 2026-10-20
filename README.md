# Question Refiner · 问题优化与完善助手

本技能会通过简短的多轮澄清，补足提问中的背景、关键条件和输出要求，再将原问题整理成可以直接交给其他 AI 使用的提示词。它只负责优化问题，不替用户回答原问题。

## 示例

**用户：** 蓝牙耳机哪款好用？

**助手（第 1 轮）：** 我先确认两点：主要在哪些场景使用、预算大约多少？你用什么手机，最看重耳机的哪项表现？

**用户：** 通勤用，预算 1000 元以内，手机是 iPhone。最看重降噪和听歌体验。

**助手（第 2 轮）：** 收到：iPhone、通勤、预算 1000 元以内，优先考虑降噪和音乐体验。你希望比较中国市场当前在售的型号和价格吗？如果信息已经够了，也可以直接让我生成。

**用户：** 希望查当前在售型号和价格，信息够了。

**助手生成的三种提问：**

- **极简版：** 请推荐适用于 iPhone 通勤、预算不超过 1000 元，并优先考虑主动降噪和音乐体验的蓝牙耳机。
- **简洁增强版：** 请比较中国市场目前在售、适用于 iPhone 通勤且价格不超过 1000 元的蓝牙耳机，优先考虑主动降噪与音乐体验，并说明主要取舍。
- **详细完整版：** 请根据中国市场当前可购买的信息，为 iPhone 用户挑选适合通勤的蓝牙耳机，预算不超过 1000 元，优先考虑主动降噪和音乐表现。比较至少 3 款符合条件的型号，并用表格列出当前价格范围、降噪表现、音质特点、佩戴舒适度、通话表现和主要优缺点；注明信息来源和查询日期。最后给出不同偏好下的选择建议；如果价格或性能数据无法确认，请明确标注不确定之处，不要编造。

## 功能

- 最多 6 轮交互，每轮最多确认 1～2 个问题。
- 区分核心必问信息与可选补充信息。
- 接收用户随时新增的想法、修改条件与跳过指令，并检查信息冲突。
- 生成极简版、简洁增强版、详细完整版三种提问。
- 不编造用户背景；遇到有害内容时拒绝优化。

## 文件

```text
question-refiner/
├── SKILL.md                       # 技能元数据和完整指令
├── README.md                      # 本说明
└── original/
    └── Question Refiner.txt        # 完整原始指令文本
```

## 安装到不同 Agent

仓库根目录的 `SKILL.md` 是标准 Agent Skill。GitHub CLI 的 `gh skill` 命令可以把仓库里的技能安装到多种 Agent；请使用支持 `gh skill` 的 GitHub CLI 版本（v2.90.0 或更新版本）。因为本仓库的 `SKILL.md` 位于根目录，命令中用 `SKILL.md` 指定该文件。

在终端运行对应命令。`--scope user` 表示安装到当前用户的全局技能目录；去掉它或改为 `--scope project`，即可按 GitHub CLI 的默认项目范围安装。

| Agent | 安装命令 | 调用方式 |
| --- | --- | --- |
| Codex | `gh skill install Tintinding/question-refiner SKILL.md --agent codex --scope user` | `$question-refiner`，或直接描述想优化的问题 |
| Claude Code | `gh skill install Tintinding/question-refiner SKILL.md --agent claude-code --scope user` | `/question-refiner` |
| Cursor | `gh skill install Tintinding/question-refiner SKILL.md --agent cursor --scope user` | `/question-refiner`，或在 Agent 对话中描述需求 |
| Gemini CLI | `gh skill install Tintinding/question-refiner SKILL.md --agent gemini-cli --scope user` | 输入 `/skills list` 确认已加载，然后描述想优化的问题 |
| GitHub Copilot | `gh skill install Tintinding/question-refiner SKILL.md --agent github-copilot --scope user` | 在支持 Agent Skills 的 Copilot Agent 对话中描述需求 |
| Qwen Code | `gh skill install Tintinding/question-refiner SKILL.md --agent qwen-code --scope user` | `/question-refiner`，或直接描述想优化的问题 |
| Kimi Code CLI | `gh skill install Tintinding/question-refiner SKILL.md --agent kimi-cli --scope user` | `/skill:question-refiner` |
| TRAE CN | `gh skill install Tintinding/question-refiner SKILL.md --agent trae-cn --scope user` | 在 Agent 对话中描述想优化的问题 |
| Qoder | `gh skill install Tintinding/question-refiner SKILL.md --agent qoder --scope user` | 在 Agent 对话中描述想优化的问题 |

GitHub CLI 当前支持表中这些 Agent 标识。首次安装遇到提示时，按 CLI 说明确认技能来源。更新技能时，可在支持 `gh skill update` 的版本中运行 `gh skill update question-refiner`。不同 Agent 的技能发现和显式调用方式可能随版本变化；若未自动触发，请在该 Agent 的技能列表中确认安装状态。

### 腾讯 WorkBuddy

WorkBuddy 支持导入本地 Skill 技能包。先从 [GitHub 下载仓库 ZIP](https://github.com/Tintinding/question-refiner/archive/refs/heads/main.zip)，解压后新建 `question-refiner` 文件夹，将根目录的 `SKILL.md` 放入该文件夹并压缩；在 WorkBuddy 的「技能」页面选择「上传技能」，导入该 ZIP 后启用即可。[WorkBuddy 官方技能文档](https://www.workbuddy.cn/docs/workbuddy/From-Beginner-to-Expert-Guide/Function-Description/Skills-Market)介绍了上传本地技能包的步骤。

### 豆包自定义智能体

豆包也能创建和定制智能体。打开豆包的智能体创建/定制界面，把 [`original/Question Refiner.txt`](original/Question%20Refiner.txt) 的完整内容粘贴到描述智能体背景或工作方式的设置中，保存后打开该智能体即可使用。豆包的智能体设置和上面的 GitHub CLI 安装方式不同；具体入口名称以你当前使用的豆包版本为准。[豆包官方功能介绍](https://www.doubao.com/legal/feature_intro)说明可以定制智能体的说话风格、技能和背景。

### 腾讯 WorkBuddy

WorkBuddy 支持导入本地 Skill 技能包。先从 [GitHub 下载仓库 ZIP](https://github.com/Tintinding/question-refiner/archive/refs/heads/main.zip)，解压后新建 `question-refiner` 文件夹，将根目录的 `SKILL.md` 放入该文件夹并压缩；在 WorkBuddy 的「技能」页面选择「上传技能」，导入该 ZIP 后启用即可。[WorkBuddy 官方技能文档](https://www.workbuddy.cn/docs/workbuddy/From-Beginner-to-Expert-Guide/Function-Description/Skills-Market)介绍了上传本地技能包的步骤。

也可以手动将 `SKILL.md` 放进目标 Agent 支持的技能目录中，或打开 [`original/Question Refiner.txt`](original/Question%20Refiner.txt)，把指令粘贴到支持自定义指令的 AI 设置里。平台专属目录请以其官方文档为准。

## 交互约定

你可以随时补充想法或修改条件，说“忽略这个”跳过某项，也可以说“停止收集”直接生成结果。发起请求时附上已知背景和条件，有助于减少澄清轮次。

## 授权

本次发布未指定开源许可证。公开可见不等于授予开放式再分发或商用许可；需要额外使用授权时，请联系作者。

