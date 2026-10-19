# Auto-Loop

**从一个 Idea 开始，让多 agent 持续推进科研探索。**

Auto-Loop 是面向 **Codex 本地项目**的科研协作 skill 与模板。人类提供研究问题、材料和预算，主管协调研究指导、探索执行与独立审查，依据实验与反证修正假设，并把进展保存在一份 `LOOP.md` 中。

指导与执行分离，审查固定版本的证据；保留负结果，在授权范围与预算内持续选择下一项有依据的探索。

**[下载完整项目](./Auto-Loop.zip?raw=true)**

## 工作流程

![Auto-Loop 科研循环：指导、执行、独立审查、记录与下一轮探索](https://github.com/user-attachments/assets/4054be74-a3ea-414e-8bfb-fa567869095b)

主循环推进研究；实现或计算有误时返回执行，反证或证据不足时返回指导。达到阶段目标、预算耗尽或遇到真实阻塞时，保存进展并交接。

## 快速使用

1. 下载并解压 `Auto-Loop.zip`，保留 `.agents` 和 `.codex` 两个隐藏目录。
2. 用 Codex App 的**本地环境**打开解压后的项目根目录。完整协作需要实际可用的原生子 agent、终端和 notebook 执行能力。
3. 将 `Idea.md` 示例替换为真实的**研究问题、材料访问条件、阶段目标、执行范围与预算**，状态改为“待探索”；将 `LOOP.md` 初始化为新课题的实际进展。具体方法和实验路径可以留给 agent 探索。
4. 由人类阅读并维护 `AGENTS.md` 及其保护。当前 Mac 规则要求在课题根目录手动执行：

```bash
chmod a-w AGENTS.md
chflags uchg AGENTS.md
ls -lO AGENTS.md
```

随后在主管聊天发送：

```text
使用 auto-loop 技能，读取当前项目的 Idea.md。
我授权在 Idea.md 指定的范围与预算内使用原生多 agent 协作。
请按根目录 AGENTS.md，分派研究指导、探索执行与独立审查，
保持指导与执行分离，在 LOOP.md 记录实际证据、结果和下一步，
持续推进到本次收尾条件；若 Idea 仍为示例，仅检查输入。
```

若 skill 未显示，可先要求读取 `.agents/skills/auto-loop/SKILL.md`，再执行上述指令。其他平台由人类先适配规则与环境。

### 查看、暂停与恢复

- **查看进展**：读取 `LOOP.md` 顶部的当前认识、待验证事项和下一步。
- **暂停**：发送“暂停 auto-loop，保存实际运行状态、证据位置和恢复位置。”
- **恢复**：发送“使用 auto-loop 恢复此前已授权的课题，核对实际进程、产物与剩余预算后继续。”新聊天需同时说明原任务范围和已有授权。

包内 `README.md` 保留了原项目的完整说明。当前发布的是工作流与配置模板，附带 Idea 为未启动示例；科研代码按项目规则在 `.ipynb` 中编写并实际执行。

## 许可证

[MIT License](https://opensource.org/license/mit) · © 2026 Haichuan-Zhao。完整许可证也包含在压缩包内的 `LICENSE` 中。

<details>
<summary>MIT 许可全文</summary>

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
