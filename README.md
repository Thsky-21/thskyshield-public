# 🛡️ Thskyshield — The Final Layer of AI Governance

**Stopping "Denial of Wallet" (DWL) at the Atomic Level.**

[![NPM Version](https://img.shields.io/npm/v/@thsky-21/thskyshield)](https://www.npmjs.com/package/@thsky-21/thskyshield)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

---

## 🚨 The Reality of 2026: Everything is Compromised

In March 2026, the **TeamPCP supply chain attacks** proved that traditional perimeter security is dead. By poisoning **LiteLLM** (v1.82.7/8) and **Axios** (v1.14.1), attackers exfiltrated thousands of OpenAI/Anthropic API keys directly from environment variables and CI/CD pipelines.

**The Problem:** Most AI startups have *zero* per-user spend controls. Once a key is leaked, an attacker can spin up infinite recursive agent loops, leading to a total **Denial of Wallet (DWL)** attack.

* **OWASP LLM10:2025 (Unbounded Consumption):** Formally recognizes resource exhaustion and uncontrolled cost growth as a top critical risk for LLM applications.
* **McKinsey Global Tech Agenda (2026):** 72% of CIOs identify cybersecurity as the #1 barrier to scaling Agentic AI.
* **The "Invisible" Loss:** Industry data shows 41% of LLM-native companies exceed their monthly budgets by over 200% due to unmanaged agentic loops and token abuse.

---

## 🛠️ Thskyshield: The Last Layer of Defense

Thskyshield is a B2B AI Governance SaaS designed to sit between your application and your LLM provider. Even if your **API keys are compromised**, Thskyshield enforces your governance policies at the edge before a single cent is spent.

### Why We Are Different (The Tech Moat)
Most "AI Firewalls" are too slow or rely on simple rate-limiting. Thskyshield uses an **Atomic Lua Governance Engine**.

1.  **Atomic Reservations:** We use custom Lua scripts inside **Upstash Redis** to perform a "Check-and-Reserve" operation in a single millisecond-fast round trip. This eliminates race conditions where multiple parallel requests might exceed a budget before the first one is logged.
2.  **24h Spend Persistence:** Our engine writes to spend keys immediately with a 24-hour TTL, ensuring that even if an Edge instance dies mid-request, the budget enforcement remains consistent.
3.  **Plan-Aware Governance:** Automatically toggle between `free`, `pro`, and `enterprise` daily budgets in real-time. A $5.00 limit for a free user is enforced even if your master OpenAI key has a $50,000 limit.

---

## 🏗️ Architecture

Thskyshield acts as a secure proxy/governance layer for your compute:

```mermaid
graph LR
    A[Compromised App/Bot] -->|Attacks API| B{Thskyshield Edge}
    B -->|Check Budget/Plan| C[(Atomic Redis)]
    C -->|Allowed| D[OpenAI / Anthropic]
    C -->|Blocked| E[429 Budget Exceeded]
    D -->|Reconcile Cost| B