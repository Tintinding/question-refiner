# Question Refiner · 问题优化与完善助手

本技能通过逐轮澄清，补全提问中的背景、关键条件和输出要求，并生成可以直接交给其他 AI 使用的优化版本。

## 功能

- 最多 6 轮交互，每轮最多确认 1～2 个问题。
- 区分核心必问信息与可选补充信息。
- 接收用户随时新增的想法、修改条件与跳过指令，并检查信息冲突。
- 生成极简版、简洁增强版、详细完整版三种提问。
- 只优化提问，不解答原问题；不编造用户背景。

## 文件

```text
question-refiner/
├── SKILL.md                       # 技能元数据和完整指令
├── README.md                      # 本说明
└── original/
    └── Question Refiner.txt        # 完整原始指令文本
```

`SKILL.md` 使用标准技能格式，包含技能名称、触发描述和完整指令正文。原始文本也单独保留，方便手动使用。示例展示的是信息收集阶段，并非完整对话记录。

## 安装到 Codex

在 PowerShell 中运行以下命令，将技能安装到当前用户的 Codex 技能目录：

```powershell
$skillsRoot = if ($env:CODEX_HOME) { Join-Path $env:CODEX_HOME 'skills' } else { Join-Path $env:USERPROFILE '.codex\skills' }
New-Item -ItemType Directory -Force -Path $skillsRoot | Out-Null
git clone https://github.com/Tintinding/question-refiner.git (Join-Path $skillsRoot 'question-refiner')
```

随后可以显式调用：

```text
请用 $question-refiner 帮我优化下面的问题：
我想比较两种学习方案，怎么选？
```

如果技能没有出现在当前会话中，请重新启动 Codex 后再试。其他支持 `SKILL.md` 的工具也可以按各自说明加载该技能目录；其安装方法以对应工具的文档为准。

## 交互约定

你可以随时补充想法或修改条件，说“忽略这个”跳过某项，也可以说“停止收集”直接生成结果。发起请求时附上已知背景和条件，有助于减少澄清轮次。

## 授权

本次发布未指定开源许可证。公开可见不等于授予开放式再分发或商用许可；需要额外使用授权时，请联系作者。

