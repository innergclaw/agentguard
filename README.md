# AgentGuard 🛡️

**The execution control layer for AI agents.**

Intercept, evaluate, and control every action your AI agents take — before it's too late.

## The Problem

AI agents can write code, send emails, and run commands. But most safeguards rely on:

- **Prompt engineering** ("don't do X") — just asking nicely
- **Tool restrictions** — all or nothing, no middle ground

There's no layer between "agent decides to act" and "action executes."

## The Solution

AgentGuard adds an explicit control layer:

1. **Agent Proposes** — emits a structured action proposal instead of executing directly
2. **Guard Evaluates** — policy engine checks rules, risk scorer classifies the action
3. **Action Executes** — approved actions run, denied actions log, escalated actions pause for human review

```
Agent Action → AgentGuard Intercepts → Policy Check → ✓ Allow / ✗ Deny / ↑ Escalate
```

## Features

- 📋 **Policy Engine** — Define rules in YAML. Auto-approve reads, deny production deletes, escalate external emails.
- ⚡ **Risk Scoring** — Every action classified low/medium/high based on impact and context.
- 🔔 **Human Escalation** — Medium/high-risk actions pause and ping you via Slack, Discord, or email.
- 📊 **Audit Log** — Every action ever proposed, approved, or denied. Full trail.
- 🔌 **Simple API** — One POST request to intercept any action. Works with LangChain, CrewAI, AutoGPT, or custom agents.
- ⏱️ **Timeout Auto-Deny** — No human response? Action auto-denies. Safe by default.

## Pricing

| Tier | Price | Actions/day | Integrations |
|------|-------|-------------|-------------|
| Free | $0/mo | 100 | Email |
| Pro | $29/mo | Unlimited | Slack + Discord |
| Enterprise | $199/mo | Unlimited | Full suite + SSO |

## Links

- 🌐 [Live Site](https://innergclaw.github.io/agentguard/)
- 🎥 [InnerG Intel YouTube](https://www.youtube.com/@innergintel)
- 🧠 [InnerG Intel](https://nasirr.innergintel.org)

## Status

🚧 **Pre-launch / Validation phase** — Join the waitlist!

---

Built by [InnerG Intel](https://nasirr.innergintel.org)
