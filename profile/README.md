<p align="center">
  <img src="https://raw.githubusercontent.com/harnessprotocol/.github/main/profile/assets/banner.svg" alt="Harness Protocol — the open standard for AI coding harnesses" width="100%">
</p>

<p align="center">
  <a href="https://github.com/harnessprotocol/harness-protocol/blob/main/LICENSE"><img alt="License" src="https://img.shields.io/badge/license-Apache--2.0-0b9bd4?style=flat-square"></a>
  <a href="https://harnessprotocol.io/spec"><img alt="Spec" src="https://img.shields.io/badge/schema-v1%20·%20candidate-0b9bd4?style=flat-square"></a>
  <a href="https://harnessprotocol.io"><img alt="Docs" src="https://img.shields.io/badge/docs-harnessprotocol.io-0b9bd4?style=flat-square"></a>
  <a href="https://github.com/harnessprotocol/harness-kit"><img alt="harness-kit stars" src="https://img.shields.io/github/stars/harnessprotocol/harness-kit?style=flat-square&color=0b9bd4&label=harness-kit"></a>
  <a href="https://github.com/harnessprotocol/harness-protocol/tree/main/heps"><img alt="Governance" src="https://img.shields.io/badge/governance-HEP%20process-0b9bd4?style=flat-square"></a>
</p>

<p align="center">
  <b>An open specification for portable AI coding harnesses.</b><br>
  A vendor-neutral <code>harness.yaml</code> format that captures the complete operational context of an AI coding agent —<br>
  plugins, MCP servers, environment, instructions, and permissions.
</p>

<p align="center">
  What <a href="https://modelcontextprotocol.io">MCP</a> is to tool communication, the Harness Protocol is to harness configuration.
</p>

---

### The problem

AI coding tools — Claude Code, Cursor, GitHub Copilot — each have their own proprietary format for capturing agent context. A configuration tuned for one tool can't be shared with a teammate on another, published for a team to reuse, or carried when you switch tools.

The Harness Protocol defines a common format so harness configurations become **portable, shareable artifacts** — the same way MCP made tool communication portable.

### `harness.yaml` at a glance

```yaml
$schema: https://harnessprotocol.io/schema/v1/harness.schema.json
version: "1"
metadata:
  name: data-engineer
  description: Harness for data engineering work in Go and SQL.

plugins:
  - name: sql-explorer
    source: acme-org/sql-explorer
    version: "^1.2.0"

mcp-servers:
  filesystem:
    transport: stdio
    command: npx
    args: ["-y", "@modelcontextprotocol/server-filesystem", "/workspace"]

permissions:
  tools:
    allow: [Read, Glob, Grep, Write, Edit]
    deny: ["mcp__*__drop_*"]
```

A profile is a YAML file validated against the Harness Protocol JSON Schema, which is the authoritative source for conformance.

### Protocol layers

The specification is organized into three decoupled layers — a tool can implement Schema-layer validation today with no dependency on the others.

| Layer | What it covers | Status |
|-------|----------------|--------|
| **Schema** | The `harness.yaml` format, JSON Schema validation, security model, plugin manifest | 🟢 **v1 — current** |
| **Exchange** | Harness-to-harness sharing: publish, fetch, and compose across tools and teams | ⚪ v2 — planned |
| **Registry** | Hosted discovery at harnessprotocol.io: search, publish, version resolution, integrity | ⚪ v2/v3 — planned |

---

### Repositories

| Repository | What it is | Start here if you want to… |
|------------|------------|----------------------------|
| **[harness-kit](https://github.com/harnessprotocol/harness-kit)** ⭐ | The reference implementation — parser, validator, plugin loader, MCP lifecycle manager, and CLI | **Use the protocol today** |
| **[harness-protocol](https://github.com/harnessprotocol/harness-protocol)** | The specification — JSON Schema, protocol prose, security model, and HEPs | Read or contribute to the spec |
| **[homebrew-tap](https://github.com/harnessprotocol/homebrew-tap)** | Homebrew tap for harness-kit | `brew install` the CLI |

> Conformance doesn't require harness-kit — **any** implementation that correctly validates and applies `harness.yaml` per the spec is conformant.

### Where to start

**🛠️ Harness authors** — writing `harness.yaml` for your project or team:
1. [Profile schema reference](https://github.com/harnessprotocol/harness-protocol/blob/main/protocol/profile-schema.md) — every field, explained
2. [Example profiles](https://github.com/harnessprotocol/harness-protocol/tree/main/examples) — annotated configs to copy from
3. [`harness-kit`](https://github.com/harnessprotocol/harness-kit) — validate and apply your file

**⚙️ Tool implementers** — building a conformant implementation or IDE integration:
1. [Overview](https://github.com/harnessprotocol/harness-protocol/blob/main/protocol/overview.md) — what the protocol is and how the layers fit
2. [Architecture](https://github.com/harnessprotocol/harness-protocol/blob/main/protocol/architecture.md) — system model and trust boundaries
3. [Application pipeline](https://github.com/harnessprotocol/harness-protocol/blob/main/protocol/application.md) — how a profile becomes effective configuration
4. [Security model](https://github.com/harnessprotocol/harness-protocol/tree/main/security) — sensitive data, permissions, and the threat model

### Contributing & governance

Normative spec changes go through the **HEP** (Harness Enhancement Proposal) process; editorial fixes can be submitted directly as pull requests. See [CONTRIBUTING.md](https://github.com/harnessprotocol/harness-protocol/blob/main/CONTRIBUTING.md) and [GOVERNANCE.md](https://github.com/harnessprotocol/harness-protocol/blob/main/GOVERNANCE.md).

<br>

<p align="center">
  <a href="https://harnessprotocol.io">Docs</a> ·
  <a href="https://harnessprotocol.io/spec">Specification</a> ·
  <a href="https://github.com/harnessprotocol/harness-protocol/blob/main/LICENSE">Apache-2.0</a>
</p>

<p align="center"><sub>Portable across tools. Shareable across teams.</sub></p>
