# Auto-Loop

**从一个 Idea 开始，让多 agent 持续推进科研探索。**

**中文** · [English](./README.en.md)

Auto-Loop 是面向 **Codex 本地项目**的科研协作 skill 与模板。人类提供研究问题、材料和预算，主管协调研究指导、探索执行与独立审查，依据实验与反证修正假设，并把进展保存在一份 `LOOP.md` 中。

指导与执行分离，保留负结果，审查固定版本的证据；在授权范围与预算内持续选择下一项有依据的探索。

**[下载中文完整包](./Auto-Loop-zh-CN.zip?raw=true)** · Windows / macOS / Linux / WSL · MIT

## 工作流程

![Auto-Loop 科研循环：指导、执行、独立审查、记录与下一轮探索](https://github.com/user-attachments/assets/4054be74-a3ea-414e-8bfb-fa567869095b)

主循环持续推进；实现或计算有误时返回执行，反证或证据不足时返回指导。达到阶段目标、预算耗尽或遇到真实阻塞时保存进展并交接。

## 快速使用

1. 下载并解压中文包，保留 `.agents` 和 `.codex` 隐藏目录。包内说明、规则、skill、角色配置和 Idea 示例均为中文，标准文件名与配置键保持不变。
2. 在 Codex 的**本地环境**中打开解压后的 `Auto-Loop` 根目录。完整协作需要实际可用的原生子 agent、终端及 notebook 执行能力。
3. 将 `Idea.md` 替换为真实的**问题、材料访问条件、阶段目标、范围与预算**，状态改为“待探索”；将 `LOOP.md` 初始化为新课题的实际进展。方法与实验路径可以留给 agent 探索。
4. 由人类阅读 `AGENTS.md` 并设置、检查适合当前系统的只读保护，然后发送下方启动指令。

<details>
<summary>文件保护：按实际系统选择，由人类执行</summary>

在解压后的课题根目录执行。ZIP 和 Git 不保证保留文件保护。

**Windows（PowerShell）**

```powershell
attrib +R ".\AGENTS.md"
Get-Item -LiteralPath ".\AGENTS.md" | Select-Object Name, IsReadOnly
icacls ".\AGENTS.md"
```

`attrib` 设置只读属性，`icacls` 查看 ACL；这不等于同账户无法解除的强制保护。需要更强隔离时，由人类或管理员配置 agent 无权更改的权限与执行环境。参见 [Microsoft 文件属性](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/attrib)与[权限说明](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/icacls)。

**macOS**

```bash
chmod a-w AGENTS.md
chflags uchg AGENTS.md
ls -lO AGENTS.md
```

**Linux / WSL**

```bash
chmod a-w AGENTS.md
ls -l AGENTS.md
```

WSL 使用 Windows 挂载目录时，还需核对 [Windows 侧实际权限](https://learn.microsoft.com/en-us/windows/wsl/file-permissions)；不能把 `chmod` 返回成功当作强制隔离证据。文件保护及其恢复均由人类维护，agent 只读检查。

</details>

```text
使用 auto-loop 技能，读取当前项目的 Idea.md。
我授权在 Idea.md 指定的范围与预算内使用原生多 agent 协作。
请按根目录 AGENTS.md，分派研究指导、探索执行与独立审查，
核对实际系统、文件保护、notebook 内核与计算设备，
保持指导与执行分离，在 LOOP.md 记录实际证据、结果和下一步，
持续推进到本次收尾条件；若 Idea 仍为示例，仅检查输入。
```

若 skill 未显示，可先要求读取 `.agents/skills/auto-loop/SKILL.md`，再执行上述指令。角色未自动发现时，skill 提供文件绑定方式；没有真实子 agent 能力时不能宣称已完成独立审查。配置入口见 [OpenAI 子 agent 文档](https://learn.chatgpt.com/docs/agent-configuration/subagents#custom-agents)与[技能文档](https://learn.chatgpt.com/docs/build-skills#where-codex-loads-local-skills)。

<details>
<summary>运行环境与 Windows 注意事项</summary>

- 在选定的 Python/虚拟环境中准备 `ipykernel` 和 notebook 执行工具（如 `nbclient`）。科学依赖由课题决定，PyTorch 按需使用；notebook 内核与依赖环境必须一致。
- Windows 可使用原生 PowerShell；WSL 是另一种执行环境，路径、Python 和依赖应保持在同一侧。使用方式见 [OpenAI Windows 文档](https://learn.chatgpt.com/docs/windows/windows-sandbox)。
- macOS 按实际支持使用 MPS；Windows/Linux/WSL 按硬件、驱动与框架支持使用 CUDA 等后端；不可用时使用 CPU，记录实际设备。
- Windows notebook 中的 PyTorch DataLoader 先用 `num_workers=0` 验证，再按实测决定并行，参见 [PyTorch Windows FAQ](https://docs.pytorch.org/docs/stable/notes/windows.html)。科研实现仍直接写入并执行 `.ipynb`。

本版完成静态配置、语言与打包检查；尚未进行 Windows 端到端科研运行。模板不附带真实数据、训练模型或科研性能指标。

</details>

### 查看、暂停与恢复

- **查看**：读取 `LOOP.md` 顶部的当前认识、待验证事项和下一步。
- **暂停**：发送“暂停 auto-loop，保存实际运行状态、证据位置和恢复位置。”
- **恢复**：发送“使用 auto-loop 恢复此前已授权的课题，核对实际进程、产物与剩余预算后继续。”新聊天需同时说明原任务范围和已有授权。

## 许可证

[MIT License](https://opensource.org/license/mit) · © 2026 Haichuan-Zhao。压缩包内附完整 `LICENSE`。标准 MIT 许可正文保留英文。

<details>
<summary>完整 MIT 许可</summary>

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

</details>
