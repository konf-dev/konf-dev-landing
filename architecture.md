---
title: konf.dev Architecture
description: Concise engineering overview of konf.dev components, flows, and security posture.
created: 2025-10-03
updated: 2025-10-03
tags: [architecture, sutra, smrti, astra, adapters]
---

# konf.dev — Architecture (overview)

A concise view of the architecture that powers konf.dev. Designed for engineers and partners: modular, observable, secure, and practical.

---

## Core pillars

- **Sutra (execution)** — Declarative workflow compiler and runtime. Compiles visual flows to executable graphs, enforces routing, retries, and observability.
- **Smrti (memory)** — Multi-tier memory: Working (STM), Short-term (vector), Episodic (persistent), and Semantic layers with provenance and lifecycle controls.
- **Astra (adapters)** — Adapter registry exposing tools, providers, and MCP endpoints through typed contracts and protocols.

---

## Architecture diagram

Below is a compact SVG that illustrates the logical components and data flows. You can also download it as an <a href="assets/architecture-diagram.svg">SVG file</a> for slides or documentation.

<!-- Architecture SVG -->

<div style="max-width:900px">

<svg viewBox="0 0 900 420" width="100%" height="auto" xmlns="http://www.w3.org/2000/svg" role="img" aria-label="konf.dev architecture diagram">
  <defs>
    <linearGradient id="g1" x1="0" x2="1"><stop offset="0" stop-color="#eef2ff"/><stop offset="1" stop-color="#f8fbff"/></linearGradient>
    <linearGradient id="g2" x1="0" x2="1"><stop offset="0" stop-color="#fff7ed"/><stop offset="1" stop-color="#fffbf5"/></linearGradient>
    <filter id="shadow" x="-20%" y="-20%" width="140%" height="140%"><feDropShadow dx="0" dy="6" stdDeviation="8" flood-color="#000" flood-opacity="0.06"/></filter>
  </defs>

  <!-- UI -->
  <rect x="20" y="20" width="220" height="120" rx="10" fill="url(#g1)" stroke="#e6e9ee"/>
  <text x="30" y="48" font-size="14" font-weight="700" fill="#0f1720">Browser UI</text>
  <text x="30" y="68" font-size="12" fill="#6b7280">Visual builder • Authoring • Demo</text>

  <!-- Runtime -->
  <rect x="310" y="20" width="260" height="120" rx="10" fill="#fff" stroke="#e6e9ee" filter="url(#shadow)"/>
  <text x="330" y="48" font-size="14" font-weight="700">Sutra (Runtime)</text>
  <text x="330" y="68" font-size="12" fill="#6b7280">Compiler • Executor • Tracing</text>

  <!-- Memory -->
  <rect x="610" y="20" width="260" height="120" rx="10" fill="url(#g2)" stroke="#e6e9ee"/>
  <text x="630" y="48" font-size="14" font-weight="700">Smrti (Memory)</text>
  <text x="630" y="68" font-size="12" fill="#6b7280">STM • Vectors • Episodic</text>

  <!-- Tools / Providers -->
  <rect x="20" y="170" width="850" height="120" rx="10" fill="#fff" stroke="#e6e9ee"/>
  <text x="30" y="196" font-size="14" font-weight="700">Adapters & Integrations (Astra)</text>
  <text x="30" y="216" font-size="12" fill="#6b7280">Third-party APIs • Connectors • MCP</text>

  <!-- arrows -->
  <path d="M240 80 L310 80" stroke="#94a3b8" stroke-width="2" marker-end="url(#arrow)"/>
  <path d="M570 80 L610 80" stroke="#94a3b8" stroke-width="2" marker-end="url(#arrow)"/>
  <path d="M460 140 L460 170" stroke="#94a3b8" stroke-width="2" marker-end="url(#arrow)"/>
  <path d="M200 140 L200 170" stroke="#94a3b8" stroke-width="2" marker-end="url(#arrow)"/>

  <defs>
    <marker id="arrow" markerWidth="10" markerHeight="10" refX="8" refY="5" orient="auto">
      <path d="M0 0 L10 5 L0 10 z" fill="#94a3b8"/>
    </marker>
  </defs>

  <!-- small notes -->
  <text x="330" y="112" font-size="11" fill="#6b7280">Deterministic routing • Retries • Spans</text>
  <text x="630" y="112" font-size="11" fill="#6b7280">Provenance • TTL • Hybrid retrieval</text>
  <text x="50" y="300" font-size="11" fill="#6b7280">Providers • Datastores • Webhooks • Secrets</text>

</svg>

</div>

---

## Key flows (short)

1. Author: user composes a visual flow in the browser; versioned artifact is created.
2. Compile: Sutra compiles the visual flow to an executable graph with typed nodes and tool contracts.
3. Execute: Sutra executes the graph, writing events and spans to telemetry and consulting Smrti for context.
4. Persist & retrieve: Smrti stores vectors, episodic records, and maintains provenance for replay and debugging.
5. Integrate: Astra adapters translate external services into typed contracts the runtime can call safely.

---

## Example metrics (illustrative)

- Average end-to-end run latency (API): 120–350 ms per step (depends on provider)
- Median token consumption per assistant turn: 350 tokens
- Typical memory vector size: 1536 dims (configurable)
- Observability: per-run spans, token accounting, and per-step timing are captured

> Note: these numbers are illustrative and will vary by deployment and provider selection.

---

## Security & compliance (short)

- Sandbox templating (Jinja) with strict filters
- Typed tool contracts and runtime checks
- Externalized secrets and tenant isolation
- Audit logs and traceable provenance for each run

---

## Where this lives

For partners and customers, we publish integration guides, adapter contracts, and certification checklists. Contact engineering@konf.dev for partner access and diagrams in higher resolution.

### Link anchors

- /architecture.md (this document)
- /assets/architecture-diagram.svg (downloadable diagram)

---

*Document created: 2025-10-03 — concise, visual, and focused for engineers.*
