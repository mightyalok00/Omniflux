<div align="center">
  <h1>⚡ Omniflux</h1>
  <p><b>Unified, Local-First AI Assistant & Composable Agent Platform</b></p>
  <p><i>Unifying local and cloud LLMs, autonomous agents, messaging channels, and workflow automation into one extensible system.</i></p>

  <p>
    <a href="https://github.com/mightyalok00/Omniflux/actions/workflows/ci.yml"><img src="https://github.com/mightyalok00/Omniflux/actions/workflows/ci.yml/badge.svg" alt="CI Status"></a>
    <a href="https://github.com/mightyalok00/Omniflux/actions/workflows/security-sast.yml"><img src="https://github.com/mightyalok00/Omniflux/actions/workflows/security-sast.yml/badge.svg" alt="Security Scan"></a>
    <a href="https://github.com/mightyalok00/Omniflux/actions/workflows/frontend.yml"><img src="https://github.com/mightyalok00/Omniflux/actions/workflows/frontend.yml/badge.svg" alt="Frontend CI"></a>
    <img src="https://img.shields.io/badge/version-1.0.0-blue" alt="Version 1.0.0">
    <img src="https://img.shields.io/badge/python-%3E%3D3.10%2C%3C3.14-blue" alt="Python Versions">
    <a href="LICENSE"><img src="https://img.shields.io/badge/license-Apache%202.0-green" alt="License"></a>
  </p>
</div>

---

## 🌟 Overview

**Omniflux** is an extensible personal AI assistant framework designed for true local-first intelligence with seamless cloud fallback. It provides unified orchestration across local hardware (Ollama, vLLM, Apple MLX, llama.cpp) and frontier cloud models (OpenAI, Anthropic Claude, Google Gemini, OpenRouter), giving you full control over privacy, latency, energy, and costs.

```
                  ┌────────────────────────────────────────┐
                  │          Omniflux Core Gateway          │
                  │   (CLI · REST API · Desktop / Web GUI)  │
                  └───────────────────┬────────────────────┘
                                      │
         ┌────────────────────────────┼────────────────────────────┐
         │                            │                            │
         ▼                            ▼                            ▼
┌──────────────────┐        ┌──────────────────┐        ┌──────────────────┐
│  Agent Engines   │        │   Tool & Skill   │        │ Memory & Context │
│  · Orchestrator  │        │     Registry     │        │  · Vector Store  │
│  · ReAct Loop    │◄──────►│  · Code Exec     │◄──────►│  · Traces & FTS  │
│  · Operatives    │        │  · Web Search    │        │  · Local Vault   │
│  · Deep Research │        │  · Custom Skills │        │  · Session DB    │
└────────┬─────────┘        └──────────────────┘        └──────────────────┘
         │
         ▼
┌──────────────────────────────────────────────────────────────────────────┐
│                             Inference Layer                              │
│   Local: Ollama · vLLM · MLX · llama.cpp   |   Cloud: Anthropic · OpenAI │
└──────────────────────────────────────────────────────────────────────────┘
```

---

## ✨ Key Capabilities

- **Local-First by Default**: Run state-of-the-art models on consumer hardware (Mac Apple Silicon, NVIDIA RTX, Linux, and Windows) with zero telemetry leakage.
- **Hybrid Intelligence Routing**: Automatically execute lightweight reasoning and tool calls locally, escalating to cloud models only when higher reasoning capacity is requested.
- **Autonomous Agents**: Eight production-ready agent presets covering daily briefings, deep multi-hop research, code interpretation, and persistent background monitoring.
- **Standardized Skills Catalog**: Extensible skills system compatible with open agent standards (Hermes, OpenClaw, agent-skills) to give agents domain-specific procedural capabilities.
- **Security & Privacy First**: Sandboxed code execution, token redaction, permission profiles, and an encrypted credential vault for API keys.
- **Multi-Interface Access**: Interact through modern graphical desktop and web interfaces, an interactive terminal chat, or an OpenAI-compatible REST API.

---

## 🚀 Quick Start

### 1. Installation

Clone the repository and install dependencies using Python 3.10+ (or [uv](https://docs.astral.sh/uv/)):

```bash
# Clone the repository
git clone https://github.com/mightyalok00/Omniflux.git
cd Omniflux

# Create and activate a virtual environment
python -m venv .venv
# On Windows:
.venv\Scripts\activate
# On Linux/macOS:
source .venv/bin/activate

# Install Omniflux with desktop dependencies
pip install -e .
```

### 2. Verify Your Environment

Run built-in diagnostics to detect available hardware, local LLM engines, and speech backends:

```bash
jarvis doctor
```

### 3. Launching Interfaces

#### Option A: Graphical Web & Desktop GUI
Start the OpenAI-compatible backend and launch the responsive frontend interface:

```bash
jarvis gui
```
*Or visit [http://127.0.0.1:5173/](http://127.0.0.1:5173/) once running.*

#### Option B: Terminal Interactive Chat
Engage directly with the agent from your command line:

```bash
jarvis chat
```

#### Option C: Headless API Server
Start the background daemon exposing standard OpenAI-compatible endpoints (`/v1/chat/completions`):

```bash
jarvis serve --host 127.0.0.1 --port 8000
```
Interactive OpenAPI documentation will be accessible at [http://127.0.0.1:8000/docs](http://127.0.0.1:8000/docs).

---

## 🤖 Built-in Agent Profiles

Omniflux includes specialized agents tailored for different workflows:

| Agent | Mode | Description |
| --- | --- | --- |
| `orchestrator` | On-demand | Multi-turn reasoning agent with automated dynamic tool routing. |
| `native_react` | On-demand | Classic Thought-Action-Observation loop agent for step-by-step problem solving. |
| `native_openhands` | On-demand | CodeAct paradigm agent that writes, executes, and validates code directly. |
| `deep_research` | On-demand | Multi-hop autonomous research across web, local documents, and vector indexes. |
| `morning_digest` | Scheduled | Automated daily briefing summarizing emails, calendar, tasks, and news with TTS. |
| `monitor_operative` | Continuous | Persistent autonomous agent with memory compression and long-horizon monitoring. |
| `operative` | Continuous | Autonomous agent capable of maintaining stateful goals over extended sessions. |
| `simple` | On-demand | Minimalist single-turn conversation agent without external tool execution. |

---

## 🔒 Security & Privacy Model

Omniflux is architected with strict boundary isolation:
1. **Local Isolation**: By default, data and chat history remain stored locally in SQLite (`~/.openjarvis/`) and vector indexes.
2. **Credential Vault**: Sensitive API tokens (OpenAI, Anthropic, Telegram) are managed through an encrypted credential store rather than plaintext configs.
3. **Tool Sandboxing**: Code interpreter tools execute within containerized or strict AST-analyzed runtime constraints to guard against arbitrary execution vulnerabilities.
4. **Rate Limiting & Safety Profiles**: Built-in security profiles (`personal`, `restricted`) govern allowed shell commands, path access, and tool permissions.

---

## 🧪 Testing & Quality Assurance

Continuous testing and linting are enforced via GitHub Actions:

```bash
# Run unit and integration test suite
pytest tests/ -v

# Run code style and format checks
ruff check .
ruff format --check .

# Validate frontend checks
cd frontend
npm test
npx tsc --noEmit
```

---

## 🤝 Contributing

We welcome contributions from the community! Please review our [Contributing Guide](CONTRIBUTING.md) and [Code of Conduct](CODE_OF_CONDUCT.md).

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to your branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

---

## 📜 Acknowledgements & Lineage

Omniflux builds upon foundational research in local agent architectures and intelligence efficiency, notably inspired by the [OpenJarvis](https://openjarvis.stanford.edu/) framework developed by researchers at Stanford SAIL and Hazy Research as part of the [Intelligence Per Watt](https://www.intelligence-per-watt.ai/) initiative. Omniflux extends these principles into an independently maintained, production-oriented personal assistant platform.

---

## 📄 License

Distributed under the **Apache License, Version 2.0**. See [`LICENSE`](LICENSE) for more information.
