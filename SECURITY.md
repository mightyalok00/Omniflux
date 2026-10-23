# Security Policy & Assurance Architecture

Omniflux is designed from the ground up as a **local-first personal AI assistant**, prioritizing local data sovereignty, secure agent execution, and verifiable runtime safety.

---

## 🛡️ Security Model & Threat Boundaries

Omniflux enforces strict security boundaries between user credentials, model inference, external network interfaces, and tool executions.

```
       ┌─────────────────────────────────────────────────────────────────┐
       │                       Host Environment                          │
       │                                                                 │
       │   ┌─────────────────────────────────────────────────────────┐   │
       │   │                Omniflux Agent Core                      │   │
       │   │                                                         │   │
       │   │   ┌───────────────────┐       ┌─────────────────────┐   │   │
       │   │   │  Taint Tracker    │       │ Credential Stripper │   │   │
       │   │   └─────────┬─────────┘       └──────────┬──────────┘   │   │
       │   │             │                            │              │   │
       │   │             ▼                            ▼              │   │
       │   │   ┌───────────────────┐       ┌─────────────────────┐   │   │
       │   │   │  Boundary Guard   │       │  Encrypted Vault    │   │   │
       │   │   └─────────┬─────────┘       └─────────────────────┘   │   │
       │   └─────────────┼───────────────────────────────────────────┘   │
       │                 │                                               │
       │                 ▼                                               │
       │       [ Execution Sandboxes ]                                   │
       │       · Subprocess Sandbox (Resource & Env isolation)           │
       │       · AST-verified Code Interpreter                           │
       │       · Explicit Confirmation Gates on destructive actions      │
       └─────────────────────────────────────────────────────────────────┘
```

---

## 🔬 Adversarial Defenses & Verification Matrix

Every defense layer in Omniflux is covered by dedicated adversarial test suites:

| Security Domain | Defense Mechanism | Test Suite & Evidence |
|---|---|---|
| **Prompt Injection** | Multi-layer heuristic & semantic injection scanner analyzing input prompts before agent execution. | [`tests/security/test_injection_scanner.py`](tests/security/test_injection_scanner.py) |
| **SSRF Defense** | Validates, resolves, and blocks loopback, link-local, private cloud metadata (169.254.169.254), and disguised hex/octal IPs. | [`tests/security/test_ssrf.py`](tests/security/test_ssrf.py)<br>[`tests/security/test_ssrf_disguised.py`](tests/security/test_ssrf_disguised.py) |
| **Tool Execution Sandbox** | Dynamic Python and shell tools run with AST security inspection, restricted builtins, and path traversal guards. | [`tests/security/test_subprocess_sandbox.py`](tests/security/test_subprocess_sandbox.py)<br>[`tests/tools/test_template_loader_security.py`](tests/tools/test_template_loader_security.py) |
| **Data Boundary Guard** | Ensures confidential memory traces and conversation history never cross from private local stores to external third parties. | [`tests/security/test_boundary_guard.py`](tests/security/test_boundary_guard.py)<br>[`tests/security/test_data_boundary_audit.py`](tests/security/test_data_boundary_audit.py) |
| **Secret Sanitization** | Automatically redacts API keys, OAuth tokens, and bearer credentials before writing to persistent logs or debug traces. | [`tests/security/test_log_sanitization.py`](tests/security/test_log_sanitization.py)<br>[`tests/security/test_credential_stripper.py`](tests/security/test_credential_stripper.py) |
| **Destructive Action Gates** | Requires explicit user confirmation before executing file overwrites, deletion commands, or system package operations. | [`tests/security/test_tool_confirmation.py`](tests/security/test_tool_confirmation.py) |
| **Taint Propagation** | Tracks untrusted data received from external web queries through multi-turn agent tool calls to prevent privilege escalation. | [`tests/security/test_taint.py`](tests/security/test_taint.py)<br>[`tests/security/test_taint_propagation.py`](tests/security/test_taint_propagation.py) |

---

## 🔒 Security Profiles

Omniflux supports selectable security profiles configured via `~/.openjarvis/config.toml`:

```toml
[security]
profile = "personal" # Options: "personal" (default) or "restricted"
rate_limit_enabled = true
credential_vault = true
```

- **`personal`**: Standard local mode. Sandboxed tools with direct user confirmation for irreversible operations.
- **`restricted`**: Hardened isolation. Disables arbitrary shell execution; enforces strict allowlist for local filesystem directories and network domains.

---

## 🛡️ Static Analysis & CI Verification

The repository enforces continuous static application security testing (SAST) on every pull request and push to `main`:
- **Bandit & CodeQL**: Automated Python AST analysis for security vulnerabilities (injection, insecure deserialization, weak ciphers).
- **Dependency Auditing**: Automated Dependabot and `npm audit` checking transitive dependencies across Python and TypeScript.
- **Workflow Permissions**: Least-privilege GitHub Actions tokens (`contents: read`) preventing workflow privilege escalation.

---

## 📩 Reporting a Vulnerability

We take the security of Omniflux seriously. If you discover a security vulnerability, please report it responsibly:

1. **Do not open a public GitHub issue.**
2. Email the maintainer directly at: `security@mightyalok.dev` (or via GitHub Private Vulnerability Reporting on the repository).
3. Include detailed steps to reproduce the vulnerability, including relevant prompt inputs or environment configurations.
4. We will acknowledge receipt within 48 hours and provide a timeline for patch remediation.
