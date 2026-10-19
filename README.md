# Auto-Loop

**从一个 Idea 开始，让 Codex 持续推进有依据、可追溯、可审查的科研探索。**

Auto-Loop 是一套面向 **Codex 本地项目**的科研协作 skill 与项目模板。你提供研究问题、材料访问条件和预算，主管 agent 协调研究指导、探索执行与独立审查，在实验、诊断和假设修正之间持续迭代，并把进展保存在项目文件中。

它适合需要反复验证假设、运行计算实验、保留失败证据的探索性研究。方法、基线和实验顺序可以交给 agent 探索，人类负责研究目标、规则维护、数据授权和预算。

**[下载完整模板](./Auto-Loop.zip?raw=true)** · [工作流程](#工作流程) · [使用教程](#使用教程) · [常见问题](#常见问题) · [MIT 许可证](#许可证)

> 当前发布的是工作流与配置模板。附带的电池健康状态 Idea 是填写示例；包内没有真实课题数据、训练模型或科研性能指标。

## 你会得到什么

| 能力 | 如何实现 |
| --- | --- |
| 从想法开始研究 | `Idea.md` 描述问题、材料、目标与预算；具体方法允许保持开放 |
| 分离研究判断与实验执行 | 指导方检查依据与竞争解释，执行方实现和运行实验，重要路线转向回到指导方 |
| 独立检查阶段结论 | 未参与被审版本的审查者分别核验计算与科学解释 |
| 失败后继续探索 | 先排查实现和数据，再修正假设、补证或停止当前路线；保留负结果 |
| 中断后恢复 | 用一份 `LOOP.md` 连接历史问题、实际证据、审查状态和下一步 |
| 保留复算入口 | 科研逻辑直接写入并执行 `.ipynb`；必要模型和结果就近保存 |

“自动”体现为：在已授权范围与预算内，agent 自主安排和推进常规迭代。运行仍依赖 Codex 提供的工具、会话能力、本地环境与实际额度。

## 工作流程

![Auto-Loop：从 Idea 输入到研究指导、探索执行、独立审查与持续迭代的流程图](https://github.com/user-attachments/assets/ffb033fb-91ec-446a-ad3d-f82b7a26a2cf)

图中各角色的职责与使用方法见下文；可展开查看流程源码。

<details>
<summary>查看可编辑的 Mermaid 流程源码</summary>

```text
flowchart TD
    A["人类填写 Idea.md<br/>研究问题 · 材料访问 · 阶段目标 · 预算"] --> B["主管检查输入、正式规则与已有进展"]
    B --> C{"具备启动条件？"}
    C -->|仍为示例或缺少必要条件| D["报告缺项<br/>仅推进不受影响的工作"]
    D -->|人类补齐后| B
    C -->|是| E["研究指导<br/>依据 → 假设 → 预测 → 最小方法与对照"]
    E --> F["主管登记本轮问题与方法<br/>写入 LOOP.md"]
    F --> G["探索执行<br/>notebook 实现 → 小规模自查 → 实验与诊断"]
    G --> H["固定实际运行版本<br/>代码 · 数据 · 配置 · 模型 · 结果"]
    H --> I["独立审查<br/>计算是否正确？证据支持什么？"]
    I --> J{"本轮证据与审查结果"}
    J -->|实现或计算有误| K["执行方修复并重新运行"]
    K --> H
    J -->|反证、证据不足或有效性分歧| L["指导方核对证据<br/>诊断、补证、修正假设或停止路线"]
    L --> M["主管保留结果、分歧与下一步<br/>更新 LOOP.md"]
    J -->|支持有边界的结论| M
    M --> N{"继续条件与预算允许？"}
    N -->|是，选择下一项有依据的问题| E
    N -->|阶段目标、预算或真实阻塞触发收尾| O["交付阶段判断与必要产物<br/>记录限制和恢复位置"]

    classDef input fill:#F3F4F6,stroke:#6B7280,color:#111827;
    classDef guide fill:#E8F3FA,stroke:#0072B2,color:#123047;
    classDef execute fill:#FFF0E8,stroke:#D55E00,color:#6B2A0A;
    classDef review fill:#EAF6F0,stroke:#338363,color:#153D2E;
    class A,B,C,D,F,H,M,N,O input;
    class E,L guide;
    class G,K execute;
    class I,J review;
```

</details>

`AGENTS.md` 是贯穿流程的唯一正式规则入口。`LOOP.md` 保存过程与判断，项目内原有 `README.md` 保存课题说明、正式结论和图注；二者不覆盖规则。

### 角色怎样分工

| 角色 | 主要职责 | 对应配置 |
| --- | --- | --- |
| 主管 / 协调 | 核对目标与预算、分派路径、跟进实际运行、维护公共记录 | 当前主管聊天读取 `SKILL.md` |
| 研究指导 | 检查领域依据和实际证据，判断假设、关键对照及重要路线转向 | `Guide.toml` → `research_guide` |
| 探索执行 | notebook 实现、训练与评估、自查、排错及持续探索 | `Executor.toml` → `research_executor` |
| 独立审查 | 只读检查固定版本，分别给出计算核验与科学评审判断 | `Reviewer.toml` → `research_reviewer` |

指导与执行由不同的实际 agent 或人类承担。审查者不得参与被审版本的设计、实现或调参；参与修订后，修订版需交给其他独立审查者。角色实例数按研究问题和可用名额安排，不要求固定人数或全部并行。

## 使用教程

### 1. 下载并解压完整项目

下载本仓库中的 **[Auto-Loop.zip](./Auto-Loop.zip?raw=true)**，解压后得到：

```text
Auto-Loop/
├── AGENTS.md                         # 唯一正式规则；由人类维护
├── Idea.md                           # 研究输入与详细填写示例
├── README.md                         # 原有项目内说明，保留原文
├── LOOP.md                           # 唯一探索记录，含模板历史
├── LICENSE                           # MIT 许可证
├── .agents/skills/auto-loop/
│   ├── SKILL.md                      # 主管运行流程
│   └── agents/openai.yaml            # skill 界面元数据
└── .codex/agents/
    ├── Guide.toml
    ├── Executor.toml
    └── Reviewer.toml
```

`.agents` 和 `.codex` 是隐藏目录，迁移时需要一起保留。可以复制整个解压目录并改名，作为自己的新课题目录。数据、实验、模型和图目录在研究需要时创建。

本仓库首页 README 面向使用者；压缩包里的 README 是原有项目内说明。发布包保留原项目文件内容，另附 MIT 许可；不包含 `.git` 历史和系统缓存。

### 2. 准备 Codex 和本地环境

在 **Codex App 的本地环境**中打开解压后的课题根目录，并从该目录开始主管聊天。完整流程需要客户端实际支持原生子 agent 委派，以及研究所需的文件、终端和 notebook 执行能力。仅有角色配置文件，并不表示这些能力已经可用。

本模板采用项目级安装：保留 `.agents/skills/auto-loop` 与 `.codex/agents` 即可，无需把 skill 复制到全局目录。Codex 的本地 skill 发现位置和自定义 agent 文件格式见官方的[技能加载说明](https://learn.chatgpt.com/docs/build-skills#where-codex-loads-local-skills)与[子 agent 配置说明](https://learn.chatgpt.com/docs/agent-configuration/subagents#custom-agents)。

模板本身由 Markdown、TOML 和 YAML 文件组成。实际课题需要的 Python、Jupyter、数据处理或模型依赖，由研究任务确定；缺少 notebook 执行依赖时，需在获准环境中补齐后再运行相应实验。

**正式启动前，由人类阅读并维护 `AGENTS.md` 及其保护。** 当前规则面向本机 Mac，要求文件无写权限且带 `uchg` 标志。发布压缩包不保证携带这些文件属性；使用者应在自己的课题目录中手动设置并检查：

```bash
cd Auto-Loop
chmod a-w AGENTS.md
chflags uchg AGENTS.md
ls -lO AGENTS.md
```

预期权限中没有 `w`，标志中包含 `uchg`。这些是供人类执行的配置步骤，agent 不负责修改规则或其保护。需要适配 Linux、Windows、其他计算设备或本地制度时，由人类在启动研究前维护适用规则；本发布包未验证这些平台。

### 3. 把 Idea 示例替换为真实研究输入

包内 `Idea.md` 是“用短片段充电信息估计电池健康状态”的**未启动示例**。先整体替换示例，再将输入状态改为“待探索”。至少写清：

| 必填内容 | 写到什么程度即可 |
| --- | --- |
| 研究问题 | 想理解或解决什么问题，面向什么对象与使用场景 |
| 材料与访问条件 | 可访问的数据路径或公开来源、资料状态，以及允许的处理方式 |
| 阶段目标 | 本次希望形成什么判断或产物；允许得到负结果或“无法判断” |
| 执行范围与预算 | 允许的工作、时间或轮次上限、计算资源及必要的费用边界 |

方法、机制、具体基线和实验顺序可以写“待 agent 探索”。没有现成数据时，可以授权 agent 检索并选择许可适用的公开数据，同时说明不能购买数据或申请账号等边界。

可按以下简版组织输入；方括号内容需换成真实信息，时间和轮次由你确定：

```markdown
# Idea

**输入状态：待探索。**

## 研究问题
[研究对象、可用输入、目标量与实际使用场景。]

## 材料与访问
[真实路径或公开来源；说明是否非公开、是否敏感及允许的处理方式。]
[若需要寻找公开数据，明确是否授权检索与下载。]

## 已有认识与未知
[区分可核查的观察、已有结论与尚未验证的假设。]
方法、具体基线和探索顺序：待 agent 探索。

## 本次目标与预算
[希望回答的一个主要问题与阶段交付。]
[总时长或轮次上限；本机资源、费用与外部调用边界。]
允许负结果；证据不足时说明剩余疑点和下一步。
```

首次用于真实课题时，将 `LOOP.md` 初始化为该课题的实际状态。模板历史只描述模板维护，不能继承为新课题的科研证据。人类原始 Idea 保留，后续计划和变化记入 LOOP。

### 4. 发送启动指令

在课题根目录的主管聊天中，复制以下内容：

```text
使用 auto-loop 技能，读取当前项目的 Idea.md。
我授权本次使用 Codex 原生多 agent 协作，按根目录 AGENTS.md 开展研究。
你承担协调职责，实际分派研究指导、探索执行与独立审查任务，
保持指导与执行分离，各类角色数量按问题和实际资源安排。

在 Idea 指定的范围与预算内持续推进：先明确假设、预测、最小方法与对照，
再由执行方完成实现、小规模自查与实验；重要路线转向由指导方核对证据。
科研代码在 .ipynb 中直接编写并实际执行，不创建或调用自编 .py。
阶段结论交给未参与被审版本的审查者，分别核验计算和科学解释。

普通排错和方案内探索自主完成，保留负结果、失败工况和审查分歧。
将进展、实际证据版本、角色标识、审查状态与下一步集中记入 LOOP.md。
若 Idea 仍为示例，仅检查输入并报告缺项，不启动示例课题。
```

如果客户端没有显示该 skill，可明确要求：

```text
先读取当前项目 .agents/skills/auto-loop/SKILL.md，
再按上面的启动指令检查输入并推进已授权任务。
```

角色名称未被发现、但原生委派可用时，工作流允许让普通子 agent 读取对应 TOML 中的职责说明，并记录为“文件绑定角色”。没有真实委派能力时，由人类承担指导及必要独立审查，单 agent 的检查只能记为自查。

### 5. 查看进展、暂停与恢复

先看 `LOOP.md` 顶部的当前进展：已经知道什么、还不确定什么、下一步做什么。下方稳定编号的条目记录主要假设、对照、实际结果、证据位置和审查状态。

需要暂停时，在主管聊天中明确说明：

```text
暂停当前 auto-loop。记录当前实际运行状态、已完成与未完成内容，
在 LOOP.md 保存证据位置、累计预算与恢复位置，说明是否还有运行中的进程。
```

恢复时发送：

```text
使用 auto-loop 恢复此前已授权的任务。
先重读 AGENTS.md、Idea.md、LOOP.md 和有关证据，
核对是否仍有实际运行中的任务，再决定恢复，避免重复启动。
延续此前累计预算和已有授权；本次范围变化以我的明确说明为准。
```

若换了新聊天，同时说明原始任务范围、已有授权和恢复意图。记录中的“运行中”不是进程仍存活的证明；恢复要检查实际进程和产物。

## 研究产物与使用边界

实际课题按需要形成以下产物，不会为了凑齐目录而预生成空文件：

| 位置 | 内容 |
| --- | --- |
| `LOOP.md` | 假设、主要实验、负结果、证据定位、审查意见与恢复位置 |
| 项目内 `README.md` | 研究问题、数据来源、正式结论、限制、图注与复算入口 |
| `.ipynb` | 实际执行的数据处理、方法、训练、评估、诊断与绘图 |
| 实验目录中的 `Results/` | 必要的指标、模型及推理状态 |
| 实验或项目的 `Figures/` | 有证据支持、确有表达价值的 JPG 科研图 |

正式规则同时要求数据隔离、训练内拟合预处理、冻结方案后使用独立测试、保存实际运行依据，并优先在可用且可靠时使用本机 MPS。方法迭代应由项目特性与可检验假设推动；额外组件的必要性和收益需要对照支持。

这些文件说明了**预期工作方式**，并不构成强制权限隔离。agent 共享文件、进程与工具，独立上下文也不会自动产生只读沙箱。非公开数据外传、付费云计算和其他超出原授权的操作，仍需人类明确授权。

当前包保留了合成流程演练的历史摘要，但没有保留其可重放材料；它不能证明真实科研有效性、自动角色发现、长期运行稳定性或可靠的并发防护。使用者应根据自己课题的实际运行与独立审查判断结果。

## 常见问题

**只安装 `SKILL.md` 就够了吗？**

完整流程还依赖根目录规则、Idea、探索记录和角色配置。初次使用建议下载整包，从解压后的课题根目录启动。

**适用于电池以外的研究吗？**

工作流没有绑定电池模型或数据集，电池 Idea 只是输入示例。可以替换成其他可由本地工具研究的问题；具体适用性需要实际验证。

**会一直运行吗？**

它要求在授权范围和预算内持续探索；达到收尾条件、预算耗尽或遇到真实阻塞时保存状态并交接。包内没有外部调度器、定时唤醒或无人值守服务。

**一个 agent 能模拟整个团队吗？**

一个 agent 可以执行并自查，但切换角色名称不构成指导与执行分离，也不构成独立审查。缺少真实委派时，需要人类补充相关判断。

**允许改规则和用于自己的项目吗？**

项目按 MIT 许可发布，使用者可以复用和修改，并保留版权及许可声明。在具体课题中，`AGENTS.md` 的维护权属于人类项目负责人，agent 按其中规则执行。

**如何反馈或贡献？**

欢迎通过仓库 Issues 或 Pull Requests 提供可核查的问题、流程改进和适配经验。反馈时请说明客户端、相关配置和复现步骤，并去除非公开研究数据及密钥。

## 下载校验

本次压缩包的 SHA-256：

```text
240ae77503742625b03d11d489748fc721c4bbf7073f4223b2deddd317191ae3
```

macOS 可在下载目录执行 `shasum -a 256 Auto-Loop.zip`，核对结果是否一致。

## 许可证

本项目采用 [MIT License](https://opensource.org/license/mit)。完整文本同时包含在压缩包内的 `Auto-Loop/LICENSE`。本仓库采用“简介与教程 + 完整压缩包”的发布形式，因此也在此保留许可全文。

```text
MIT License

Copyright (c) 2026 Haichuan-Zhao

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```
