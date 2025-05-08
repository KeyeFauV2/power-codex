<h1 align="center">⚡️ Power-Codex CLI for Windows & PowerShell ⚡️</h1>

> 🚀 Forked from OpenAI Codex CLI — now Windows-native!  
> 💻 Use your terminal automation superpowers with AI, directly in PowerShell.

<p align="center">
  <img src="https://github.com/user-attachments/assets/68f25ef9-cb3d-4f40-833b-560a6a3f5e36" width="160" alt="power-codex logo" align="center">
</p>

<p align="center">
  <b>Lightweight coding agent — Unleash AI workflows in PowerShell</b>
</p>

---

<details>
<summary><strong>Table of contents</strong></summary>

<!-- Begin ToC -->
- [Experimental technology disclaimer](#experimental-technology-disclaimer)
- [Quickstart (Windows/PowerShell)](#quickstart-windowspowershell)
- [Why Power-Codex?](#why-power-codex)
- [Security & permissions (PowerShell)](#security--permissions-powershell)
- [System requirements](#system-requirements)
- [CLI reference](#cli-reference)
- [Project docs & memory](#project-docs--memory)
- [Non-interactive/CI mode](#non-interactiveci-mode)
- [Installation](#installation)
- [Configuration guide](#configuration-guide)
- [FAQ](#faq)
- [Contributing](#contributing)
- [License](#license)
<!-- End ToC -->

</details>

---

## ⚠️ Experimental Technology Disclaimer

`Power-Codex` is an **experimental fork** of OpenAI Codex CLI, tailored for Windows.  
It skips Linux-style sandboxing and executes all commands natively in **PowerShell**.  
**Warning : This tool grants AI direct access to your PowerShell terminal — handle with care!**

---

## 🚀 Quickstart (Windows/PowerShell)

1. **Install globally:**  
   _(Requires Node.js 16+ and npm/yarn/PNPM/Bun)_
   ```powershell
   npm install -g @openai/codex
   ```
2. **Set your OpenAI API key:**
   ```powershell
   $env:OPENAI_API_KEY = "your-api-key-here"
   ```
   Or place a `.env` file with your key in your project root:
   ```
   OPENAI_API_KEY=your-api-key-here
   ```

3. **Launch Power-Codex:**
   ```powershell
   codex
   ```
   Or run a single-shot AI job:
   ```powershell
   codex "convert all .docx files in this folder to PDF"
   ```

---

## 🦾 Why Power-Codex?

- **Windows/PowerShell native:** No more WSL2 or Linux sandbox!  
- **OpenAI-level reasoning:** Chat, code, explain, automate – all from Windows Command line.
- **Rich PowerShell & file access:** Use AI to automate file changes, scripting, test generation, documentation, and more.
- **Full repo control:** Works inside any Git repo for commit/PR workflows.

---

## 🔐 Security & permissions (PowerShell)

**Danger: No sandbox on Windows!**  
This agent runs PowerShell commands directly.  
You control how much autonomy is allowed (via the `--approval-mode` flag):

| Mode           | What AI can do automatically                         | Needs approval for              |
| -------------- | ---------------------------------------------------- | ------------------------------- |
| Suggest        | Read all files                                       | All edits & commands            |
| Auto Edit      | Read & write files (patch only)                      | Arbitrary shell commands        |
| Full Auto      | Read/write files, run any PowerShell command         | (Nothing—dangerous!)            |

**Best practice:**  
Always work in a versioned (Git) repo and review suggestions.

---

## 🖥️ System requirements

| Requirement       | Details                                                |
| ----------------- | ------------------------------------------------------ |
| Operating system  | **Windows 10/11** (PowerShell 5+, or PowerShell Core)  |
| Node.js           | 16+ (LTS recommended)                                  |
| Git               | 2.23+ (optional, for best workflow)                    |
| RAM               | 4-GB minimum (8-GB recommended)                        |

> **Do not** run this CLI on highly sensitive, production, or critical systems.

---

## 📕 CLI Reference

| Command                      | Purpose                          | Example                                     |
|------------------------------|----------------------------------|---------------------------------------------|
| `codex`                      | Interactive REPL                 | `codex`                                     |
| `codex "..."`                | Prompt for an answer             | `codex "Write a PowerShell script"`         |
| `codex -q`                   | Non-interactive/quiet mode       | `codex -q "Test if all .ps1 files compile"` |

Key flags: `--model`, `--approval-mode`, `--quiet`, `--notify`

---

## 🧠 Project docs & memory

- Reads:
  1. Global `~/.codex/instructions.md`
  2. Project-level `codex.md`
- Can be disabled:  
  ```powershell
  codex --no-project-doc
  ```

---

## 🤖 Non-interactive/CI mode

Example (in PowerShell, for CI/CD pipelines):  
```powershell
$env:OPENAI_API_KEY = "<your-key>"
codex -a auto-edit --quiet "Update CHANGELOG for next release"
```
Use `CODEX_QUIET_MODE=1` to silence UI prompts.

---

## 💾 Installation

<details open>
<summary><b>From npm (Recommended)</b></summary>
<p>

```powershell
npm install -g @openai/codex
# or for yarn, pnpm, bun
yarn global add @openai/codex
pnpm add -g @openai/codex
bun install -g @openai/codex
```
</p>
</details>

<details>
<summary><b>Build from source (Windows workflow)</b></summary>
<p>

```powershell
git clone https://github.com/your-username/power-codex.git
cd power-codex/codex-cli
pnpm install
pnpm build
pnpm link
```
To run the CLI:
```powershell
node ./dist/cli.js
```
</p>
</details>

---

## ⚙️ Configuration guide

Config files live in `~/.codex/` and support JSON or YAML.

#### Example config (`config.json`):

```json
{
  "model": "gpt-4",
  "approvalMode": "auto-edit",
  "notify": true,
  "providers": {
    "openai": { "name": "OpenAI", "baseURL": "https://api.openai.com/v1", "envKey": "OPENAI_API_KEY" }
    // Add other providers here if needed
  }
}
```

Set your keys as environment variables  
(i.e. `$env:OPENAI_API_KEY = "..."` before running).

---

## ❓ FAQ

<details>
<summary><b>Does it run natively on Windows?</b></summary>

<strong>YES!</strong>  
Power-Codex is tailored for Windows & PowerShell environments.  
No need for WSL2, Docker, or virtual Linux environments.
</details>

<details>
<summary><b>Is there any sandbox?</b></summary>

<strong>Not in this fork!</strong>  
Power-Codex runs directly on your Windows system.  
Do <b>NOT</b> run on production systems or with sensitive files.
</details>

<details>
<summary><b>How to avoid dangerous commands?</b></summary>

Use `--approval-mode suggest` or `auto-edit` and manually approve critical steps.
</details>

---

## 🤝 Contributing

- Fork it 🍴, Clone it 🚀, Open a PR!
- Please open an issue/discussion first for proposals.
- For major changes, ensure tests and docs are up-to-date.
- See [CONTRIBUTING.md](./CONTRIBUTING.md) for workflow & coding style.

---

## 📜 License

Licensed under the [Apache-2.0 License](LICENSE).

---

<sub>
Made with ❤️ by forking the brilliant <a href="https://github.com/openai/codex">OpenAI Codex CLI</a> and unleashing it for every Windows dev!  
</sub>
