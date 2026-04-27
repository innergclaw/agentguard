# AgentGuard 🛡️

> **The execution control layer for AI agents.**
> Intercept, evaluate, and control every action your AI agents take — before it's too late.

[![Live Site](https://img.shields.io/badge/site-live-brightgreen)](https://innergclaw.github.io/agentguard/)
[![Status](https://img.shields.io/badge/status-pre--launch-orange)](https://innergclaw.github.io/agentguard/)
[![Built by InnerG Intel](https://img.shields.io/badge/built%20by-InnerG%20Intel-indigo)](https://nasirr.innergintel.org)

---

## 🧠 The Problem

AI agents are powerful. They can write code, send emails, run commands, modify databases, and interact with external APIs — all autonomously.

But here's the gap:

**Most AI agent safety relies on two things:**

1. **Prompt engineering** — "Don't do X" — literally just asking nicely. Breaks when context shifts, prompts leak, or the agent gets creative.
2. **Tool restrictions** — Limit which tools exist. All-or-nothing. Either the agent can send emails or it can't. No middle ground.

**There is no layer between "the agent decides to act" and "the action executes."**

That's like having employees with no manager review — they can send emails, delete files, run commands, and the first time you find out is *after* it's done.

This is a failure mode that keeps showing up in production agent systems.

---

## 💡 The Solution

AgentGuard adds an **explicit execution control layer** — something that intercepts every proposed action, evaluates it, and decides whether it's allowed to run.

### How It Works

```
┌─────────────┐     ┌──────────────────┐     ┌──────────────┐     ┌───────────┐
│  AI Agent    │────▶│  AgentGuard      │────▶│  Policy      │────▶│  Execute  │
│  Proposes    │     │  Intercepts      │     │  Engine      │     │  Action   │
│  Action      │     │  Action          │     │  Evaluates   │     │  (or not) │
└─────────────┘     └──────────────────┘     └──────────────┘     └───────────┘
                                                    │
                                            ┌───────┴───────┐
                                            │               │
                                         Allow          Deny / Escalate
```

**Three-step flow:**

1. **Agent Proposes** — Instead of executing directly, your agent emits a structured action proposal with context, target, and intent.
2. **Guard Evaluates** — The policy engine checks rules, the risk scorer classifies the action, and decides: auto-approve, auto-deny, or escalate to a human.
3. **Action Executes** — Approved actions run. Denied actions are logged. Escalated actions pause until a human decides. Full audit trail every time.

### Example

```json
// Agent wants to send an email
PROPOSAL: { "action": "send_email", "to": "client@company.com" }
POLICY CHECK: external_communication → requires_approval
ESCALATED: Waiting for human approval...
✓ APPROVED — action executed at 14:32:07
```

---

## ✨ Features

### 📋 Policy Engine
Define rules in simple YAML or JSON. Auto-approve safe actions (reads, searches), deny dangerous ones (production deletes), and escalate uncertain ones (external emails, API calls).

```yaml
rules:
  - action: "read_file"
    auto: approve
  - action: "send_email"
    risk: medium
    require_approval: true
  - action: "delete"
    env: "production"
    auto: deny
```

### ⚡ Risk Scoring
Every action gets an automatic risk classification — **low**, **medium**, or **high** — based on impact type, target system, data sensitivity, and context.

### 🔔 Human Escalation
Medium and high-risk actions pause and ping you via **Slack**, **Discord**, or **email**. One-click approve or deny. No digging through logs.

### 📊 Audit Log
Every action ever proposed, approved, denied, or escalated — full timestamped trail. Built for compliance (SOC2, HIPAA) and debugging.

### 🔌 Simple API
One `POST` request to intercept any action. Works with any agent framework:

```bash
curl -X POST https://api.agentguard.dev/v1/check \
  -H "Authorization: Bearer YOUR_KEY" \
  -d '{"action": "send_email", "to": "client@company.com", "tool": "gmail"}'
```

Compatible with **LangChain**, **CrewAI**, **AutoGPT**, **OpenClaw**, or any custom agent system.

### ⏱️ Timeout Auto-Deny
No human response within the configured timeout? Action is **automatically denied**. Safe by default, not sorry after the fact.

---

## 💰 Pricing

| Tier | Price | Actions/day | Key Features |
|------|-------|-------------|-------------|
| **Free** | $0/mo | 100 | Basic policy engine, email notifications |
| **Pro** | $29/mo | Unlimited | Custom policies, Slack + Discord, full audit log, risk scoring |
| **Enterprise** | $199/mo | Unlimited | Team dashboard, SSO, role-based access, compliance reports, priority support |

Profitable at **1 paid user**. Margins at **85-95%**.

---

## 🏗️ Architecture

```
AgentGuard
├── Proposal Interceptor    # Hooks into agent tool calls, catches everything
├── Policy Engine           # YAML/JSON rules engine
├── Risk Scorer             # Classifies actions by impact level
├── Approval Dashboard      # Web UI to view/manage pending actions
├── Audit Log               # Full history of all proposed actions
├── Notification Layer      # Slack / Discord / email / SMS alerts
└── API Gateway             # REST API for agent integration
```

### Tech Stack (Planned)

| Layer | Technology | Why |
|-------|-----------|-----|
| Frontend | Next.js + Tailwind CSS | Fast, clean, responsive |
| Backend | Next.js API Routes | One codebase |
| Database | Supabase | Free tier, auth built-in, real-time |
| Hosting | Vercel | Zero-config deploys |
| Notifications | Slack Webhooks + Resend | Simple and reliable |

---

## 🗺️ Roadmap

- [x] Concept validation
- [x] Landing page + waitlist
- [ ] Core API + policy engine MVP
- [ ] Approval dashboard (web UI)
- [ ] Slack/Discord integration
- [ ] Public beta launch
- [ ] VS Code extension (inline approvals)
- [ ] CLI tool for terminal-based workflows
- [ ] Mobile push notifications
- [ ] Compliance report generation (SOC2, HIPAA)

---

## 🎯 Target Market

- **Developers** building AI agent workflows (LangChain, CrewAI, AutoGPT users)
- **Companies** deploying autonomous AI agents in production
- **Enterprise teams** needing audit trails and compliance for AI actions
- **Agencies** running agents on behalf of clients
- **DevOps / Platform teams** managing AI agent permissions at scale

---

## 🔗 Links

- 🌐 **Live Site:** [innergclaw.github.io/agentguard](https://innergclaw.github.io/agentguard/)
- 🎥 **YouTube:** [youtube.com/@innergintel](https://www.youtube.com/@innergintel)
- 🧠 **InnerG Intel:** [nasirr.innergintel.org](https://nasirr.innergintel.org)
- 📋 **AI Program:** [innergclaw.github.io/innerg-ai-program-signup](https://innergclaw.github.io/innerg-ai-program-signup/)

---

## 📄 License

MIT

---

## 👤 Author

**Nasirr Mayo** — Founder, [InnerG Intel](https://nasirr.innergintel.org)

Philly-based builder. AI education + agent readiness.

- 📧 nasirr@innergintel.org
- 📞 267-473-0397
- 🌐 [nasirr.innergintel.org](https://nasirr.innergintel.org)

---

> *"The real unlock isn't any single app. It's the protocol layer. Build that right and every agent, every OS, every startup idea becomes 10x easier to ship on top of it."*

---

**🚧 Pre-launch / Validation Phase** — [Join the waitlist →](https://innergclaw.github.io/agentguard/)
