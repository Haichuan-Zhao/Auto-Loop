# Auto-Loop

**Start with an Idea. Keep research moving through multi-agent exploration.**

[Chinese](./README.md) · **English**

Auto-Loop is a research skill and template for **local Codex projects**. You provide the question, materials, and budget. A coordinator assigns research guidance, exploration execution, and independent review, revises hypotheses using experiments and counterevidence, and preserves progress in one `LOOP.md`.

Guidance and execution remain separate. Reviewers inspect frozen evidence, negative findings are retained, and the next justified exploration stays within authorization and budget.

**[Download the complete English package](./Auto-Loop-en.zip?raw=true)** · Windows / macOS / Linux / WSL · MIT

## Research Loop

![Auto-Loop research cycle: guidance, execution, independent review, records, and the next round](https://github.com/user-attachments/assets/3efc469d-df7a-461e-9da8-3705bb055ec2)

The main loop continues research. Implementation or computation errors return to execution; counterevidence or insufficient evidence returns to guidance. Stage goals, exhausted budgets, or real blockers trigger a saved handoff.

## Quick Start

1. Download and extract the English package, keeping the hidden `.agents` and `.codex` directories. Instructions, rules, skill, role configurations, and the Idea example are in English; standard filenames and configuration keys remain unchanged.
2. Open the extracted `Auto-Loop` root in a **local Codex environment**. Full collaboration requires actual native subagents, terminal access, and notebook execution.
3. Replace `Idea.md` with your **question, material access, stage goal, scope, and budget**, and set its status to "ready for exploration." Initialize `LOOP.md` for the actual project. Agents can explore methods and experiment routes.
4. The human reads `AGENTS.md`, sets and checks suitable read-only protection for the actual system, then sends the startup prompt below.

<details>
<summary>File protection: choose your system; the human runs these commands</summary>

Run in the extracted project root. ZIP archives and Git do not guarantee that file protection survives.

**Windows (PowerShell)**

```powershell
attrib +R ".\AGENTS.md"
Get-Item -LiteralPath ".\AGENTS.md" | Select-Object Name, IsReadOnly
icacls ".\AGENTS.md"
```

`attrib` sets the read-only attribute; `icacls` displays the ACL. This is not enforced protection against the same account removing it. Stronger isolation requires human- or administrator-managed permissions and an execution environment agents cannot change. See Microsoft's [file attributes](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/attrib) and [permissions](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/icacls) documentation.

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

For Windows-mounted directories in WSL, also inspect the [actual Windows permissions](https://learn.microsoft.com/en-us/windows/wsl/file-permissions). A successful `chmod` does not prove enforced isolation. The human maintains and restores protection; agents only inspect it.

</details>

```text
Use the auto-loop skill and read the current project's Idea.md.
I authorize native multi-agent collaboration within the scope and budget in Idea.md.
Follow root AGENTS.md and assign guidance, execution, and independent review.
Check the actual system, file protection, notebook kernel, and compute devices.
Keep guidance separate from execution. Record actual evidence, results, and
next steps in LOOP.md. Continue to this task's closure conditions.
If the Idea is still an example, only check the input.
```

If the skill is missing from the selector, first ask Codex to read `.agents/skills/auto-loop/SKILL.md`, then send the prompt. The skill provides file-bound roles when automatic discovery is unavailable. Without actual subagents, do not claim independent review. See OpenAI's [subagent](https://learn.chatgpt.com/docs/agent-configuration/subagents#custom-agents) and [skill](https://learn.chatgpt.com/docs/build-skills#where-codex-loads-local-skills) documentation.

<details>
<summary>Runtime requirements and Windows notes</summary>

- Prepare `ipykernel` and a notebook execution tool such as `nbclient` in your chosen Python/virtual environment. Scientific dependencies depend on the project; PyTorch is optional. Select the matching notebook kernel.
- Native PowerShell is supported for Windows workflows. WSL is a separate execution environment: keep paths, Python, and dependencies on the same side. See the [OpenAI Windows documentation](https://learn.chatgpt.com/docs/windows/windows-sandbox).
- Use MPS on macOS when actually supported, or a backend such as CUDA on Windows/Linux/WSL when hardware, drivers, and framework support it. Otherwise use CPU and record the actual device.
- For PyTorch DataLoader in Windows notebooks, validate with `num_workers=0` before deciding whether parallel workers work in that environment. See the [PyTorch Windows FAQ](https://docs.pytorch.org/docs/stable/notes/windows.html). Research logic still lives and executes directly in `.ipynb`.

This edition has static configuration, language, and packaging checks; end-to-end research execution on Windows has not been tested. No real datasets, trained models, or scientific performance results are included.

</details>

### Inspect, Pause, and Resume

- **Inspect:** read the current understanding, unresolved issues, and next step at the top of `LOOP.md`.
- **Pause:** say "Pause auto-loop and save the actual run state, evidence locations, and recovery point."
- **Resume:** say "Use auto-loop to resume the previously authorized project; check actual processes, artifacts, and remaining budget first." In a new chat, also provide the original scope and authorization.

## License

[MIT License](https://opensource.org/license/mit) · © 2026 Haichuan-Zhao. The complete `LICENSE` is included in the package.

<details>
<summary>Full MIT license</summary>

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
