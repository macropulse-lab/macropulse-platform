<div align="center">

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="brand/logo-mono.svg">
  <img src="brand/logo-green.svg" alt="MacroPulse" width="96" height="96">
</picture>

# MacroPulse

**Know the macro regime before the market does — and prove every decision your agents make.**

Two products, one platform. A daily macro-regime signal for quant teams, and a cryptographic
pre-execution compliance layer for autonomous trading agents.

[Website](https://macropulse.live) · [API Docs](https://macropulse.live/api-docs) · [IRL Engine](https://macropulse.live/irl) · [Track Record](https://macropulse.live/track-record) · [Live Sandbox](https://irl.macropulse.live)

</div>

---

## The two products

### 🟢 MacroPulse — Macro Regime API
A daily macro-regime classification for US markets: four regimes (**Expansion · Recovery · Tightening · Risk-Off**)
derived from Fed liquidity, credit spreads, volatility, and the yield curve, served over a REST API and signed
with Ed25519 so every reading is independently verifiable. Free tier, then Starter and Pro.

→ Start at [macropulse.live](https://macropulse.live) · `pip install macropulse-mcp` to use it inside any AI agent.

### 🟡 IRL Engine — Immutable Reasoning Log
A pre-execution compliance gateway that sits between an AI trading agent and the exchange. Before any order is
placed, the agent's reasoning is cryptographically sealed (SHA-256 / RFC 8785), written to a bitemporal ledger,
and anchored daily to Bitcoin via OpenTimestamps — producing a tamper-evident audit trail that **anyone can
verify offline, without trusting us.**

→ Try the [live sandbox](https://irl.macropulse.live) (no signup) · read the [protocol spec](https://github.com/macropulse-lab/irl-public-docs).

---

## How it fits together

```mermaid
flowchart LR
    subgraph MP["MacroPulse — signal"]
        PIPE["Daily pipeline: XGBoost + HMM"] --> API["Regime API"]
        API --> MTA["Signed regime (Ed25519 MTA)"]
    end

    subgraph IRL["IRL Engine — compliance"]
        AGENT["Your AI agent"] --> ENGINE["IRL Engine (self-hosted)"]
        ENGINE --> LEDGER["Bitemporal ledger + Merkle root"]
        LEDGER --> BTC["Bitcoin anchor (OpenTimestamps)"]
    end

    subgraph CONSUME["Integrate & verify"]
        SDKPY["irl-sdk Python"]
        SDKTS["irl-sdk TypeScript"]
        MCP["macropulse-mcp"]
        VERIFY["irl-verify (offline, MIT)"]
        DASH["Compliance dashboard"]
    end

    MTA -->|"market-truth anchor"| ENGINE
    API --> SDKPY
    API --> SDKTS
    API --> MCP
    LEDGER --> VERIFY
    LEDGER --> DASH

    style MP fill:#0d1f14,stroke:#3fb85a,color:#fff
    style IRL fill:#1f180a,stroke:#f5a623,color:#fff
    style CONSUME fill:#12122b,stroke:#4f46e5,color:#fff
```

---

## Repository index

| Repo | What it is | Stack | Ships to |
|------|-----------|-------|----------|
| **[macropulse](https://github.com/GabrielGauss/macropulse)** 🔒 | Core: regime pipeline, REST API, dashboard, marketing site | Python / React | VPS · Vercel |
| **[irl](https://github.com/macropulse-lab/irl)** | IRL Engine — pre-execution compliance gateway (FSL-1.1-ALv2, free to use) | Rust | self-host |
| **[irl-gateway](https://github.com/macropulse-lab/irl-gateway)** | MCP server — any AI agent trades through IRL under a mandate | Python | PyPI · `irl-gateway` · MCP Registry |
| **[irl-public-docs](https://github.com/macropulse-lab/irl-public-docs)** | IRL protocol spec, whitepaper, integration & compliance guides | Markdown | — |
| **[irl-sdk-python](https://github.com/macropulse-lab/irl-sdk-python)** | IRL client SDK for Python | Python | PyPI · `irl-sdk` |
| **[irl-sdk-ts](https://github.com/macropulse-lab/irl-sdk-ts)** | IRL client SDK for TypeScript | TypeScript | npm · `irl-sdk` |
| **[irl-verify](https://github.com/macropulse-lab/irl-verify)** | Offline proof-bundle verifier — frozen spec, MIT | Rust | crates.io |
| **[irl-dashboard](https://github.com/macropulse-lab/irl-dashboard)** | Read-only compliance console for an IRL Engine | TypeScript | Vercel |
| **[macropulse-mcp](https://github.com/macropulse-lab/macropulse-mcp)** | MCP server — the regime signal as native AI-agent tools | Python | PyPI · `macropulse-mcp` |

🔒 = private source.

---

## Pick your path

**I want the macro regime signal** → get a free key at [macropulse.live](https://macropulse.live), or drop it into
your AI assistant with `pip install macropulse-mcp`.

**I want my trading agent to be auditable** → connect any MCP agent with `pip install irl-gateway`, or wrap
your own code with `pip install irl-sdk`. Try the [sandbox](https://irl.macropulse.live), then self-host the
[engine](https://github.com/macropulse-lab/irl).

**I need to verify someone's proof** → you never need an account. Clone
[irl-verify](https://github.com/macropulse-lab/irl-verify) and check any proof bundle offline, or use the
in-browser [explorer](https://macropulse.live/proof).

---

## Brand

Canonical logo and colors live in [`brand/`](brand/). The mark is a phase-offset striped sphere —
the interference seam represents a regime transition. Primary green `#3fb85a`; on dark surfaces use the
mono (white) variant.

<div align="center">
<img src="brand/logo-green.svg" width="64" height="64" alt="green mark">
&nbsp;&nbsp;&nbsp;
<img src="brand/logo-black.svg" width="64" height="64" alt="black mark">
</div>

---

<div align="center">
<sub>© 2026 MacroPulse · <a href="https://macropulse.live">macropulse.live</a> · licensing@macropulse.live</sub>
</div>
