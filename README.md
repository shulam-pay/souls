# Shulam Souls

Autonomous AI agent system for Shulam. 18 specialized agents ("Apostles") that operate proactively on schedules, scan for work, write code, and auto-merge PRs with safety guardrails.

> *Inspired by Coinbase's milestone of 5% merged PRs from AI agents.*

---

## Overview

Souls is Shulam's multi-agent orchestration system. Each agent has a specific role, personality, and set of responsibilities. They operate autonomously on a Mac Mini harness server, coordinating via Slack and GitHub.

```
┌─────────────────────────────────────────────────────────────┐
│                      SHULAM SOULS                           │
├─────────────────────────────────────────────────────────────┤
│  Mac Mini M4 (Always-On Harness)                            │
│  ┌─────────┐ ┌─────────┐ ┌─────────┐ ┌─────────┐           │
│  │  Peter  │ │  James  │ │ Andrew  │ │  John   │  ...x18   │
│  │  Lead   │ │ Oracle  │ │   Dev   │ │ Analyst │           │
│  └────┬────┘ └────┬────┘ └────┬────┘ └────┬────┘           │
│       │           │           │           │                 │
│       └───────────┴───────────┴───────────┘                 │
│                       │                                     │
│              Mission Control (Convex)                       │
│                       │                                     │
│       ┌───────────────┼───────────────┐                     │
│       ▼               ▼               ▼                     │
│   GitHub          Slack          Services                   │
│   (PRs)         (Alerts)        (APIs)                      │
└─────────────────────────────────────────────────────────────┘
```

---

## The 18 Apostles

### Core Team (1-6)

| # | Apostle | Session Key | Role | Focus |
|---|---------|-------------|------|-------|
| 1 | **Peter** | `agent:shulam:lead` | Squad Lead | Orchestrates team, delegates tasks, escalates blockers |
| 2 | **James** | `agent:shulam:oracle` | Oracle | Payment verification, pricing, blockchain attestations |
| 3 | **Andrew** | `agent:shulam:developer` | Developer | Core facilitator code, smart contracts, infrastructure |
| 4 | **John** | `agent:shulam:analyst` | Analyst | Market intel, competitor tracking, strategy |
| 5 | **Philip** | `agent:shulam:support` | Support | Merchant support, ticket triage, documentation |
| 6 | **Bartholomew** | `agent:shulam:researcher` | Researcher | Merchant research, personas, sales intel |

### Product & Engineering (7-10)

| # | Apostle | Session Key | Role | Focus |
|---|---------|-------------|------|-------|
| 7 | **Matthew** | `agent:shulam:content` | Content | Docs, blog, educational content, SEO |
| 8 | **Thomas** | `agent:shulam:qa` | QA | Testing, security review, code quality |
| 9 | **Thaddaeus** | `agent:shulam:designer` | Designer | UI/UX, dashboard, payment widget, brand |
| 10 | **Simon** | `agent:shulam:devops` | DevOps | CI/CD, deployments, monitoring, infra |

### Growth & Operations (11-14)

| # | Apostle | Session Key | Role | Focus |
|---|---------|-------------|------|-------|
| 11 | **James-Lesser** | `agent:shulam:ops` | Operations | Merchant onboarding, KYB, compliance ops |
| 12 | **Matthias** | `agent:shulam:data` | Data | Analytics, dashboards, reporting, metrics |
| 13 | **Judas** | `agent:shulam:growth` | Growth | Outreach, campaigns, merchant acquisition |
| 14 | **Paul** | `agent:shulam:partnerships` | Partnerships | Ecosystem, integrations, BD |

### Compliance & Finance (15-16)

| # | Apostle | Session Key | Role | Focus |
|---|---------|-------------|------|-------|
| 15 | **Timothy** | `agent:shulam:compliance` | Compliance | KYT screening, AML, OFAC, SAR generation |
| 16 | **Titus** | `agent:shulam:finance` | Finance | Treasury, USDC flows, reconciliation |

### Specialized (17-18)

| # | Apostle | Session Key | Role | Focus |
|---|---------|-------------|------|-------|
| 17 | **Barnabas** | `agent:shulam:community` | Community | Discord, Twitter, developer relations |
| 18 | **Luke** | `agent:shulam:scribe` | Scribe | Meeting notes, changelog, knowledge base |

---

## Apostle Personalities

Each agent has a distinct personality derived from biblical traits:

| Apostle | Biblical Trait | Agent Personality |
|---------|---------------|-------------------|
| **Peter** | Bold leader | Decisive, takes charge, owns failures |
| **James** | "Son of Thunder" | Intense accuracy, zero tolerance for errors |
| **Andrew** | Practical, first follower | Reliable builder, ships quietly |
| **John** | Beloved, insightful | Sees patterns others miss, strategic |
| **Philip** | Approachable, helpful | Patient with merchants, clear communicator |
| **Bartholomew** | Honest, no guile | Unbiased research, calls it like it is |
| **Matthew** | Tax collector, detail-oriented | Meticulous documentation, organized |
| **Thomas** | Skeptical, thorough | Questions everything, finds edge cases |
| **Thaddaeus** | Quiet, dedicated | Pixel-perfect, obsessive about craft |
| **Simon** | Zealot, passionate | Automates everything, hates manual work |
| **James-Lesser** | Steady, reliable | Process-oriented, never drops the ball |
| **Matthias** | Chosen, analytical | Data-driven, lets numbers speak |
| **Judas** | Ambitious (redeemed) | Aggressive growth, always closing |
| **Paul** | Visionary, connector | Big picture, builds bridges |
| **Timothy** | Young, teachable | By-the-book, asks before acting |
| **Titus** | Organizer, trustworthy | Penny-accurate, audit-ready |
| **Barnabas** | Encourager | Welcoming, builds community |
| **Luke** | Historian, physician | Thorough records, heals knowledge gaps |

---

## Infrastructure

### Hardware

| Component | Spec |
|-----------|------|
| **Machine** | Mac Mini M4 Pro |
| **RAM** | 24GB |
| **Storage** | 512GB SSD |
| **Location** | Always-on, home office |
| **Network** | Tailscale mesh |

### Software Stack

| Component | Technology |
|-----------|------------|
| **AI Model** | Claude Opus 4.5 (Anthropic API) |
| **Process Manager** | PM2 |
| **Queue** | Redis + BullMQ |
| **Database** | Convex (Mission Control) |
| **Code Execution** | Claude Code (CLI) |
| **Notifications** | Slack |
| **Version Control** | GitHub |

---

## Agent Framework

### Session Management

Each agent runs as a persistent Claude Code session:

```bash
# Start an agent
claude-code --session agent:shulam:developer --resume

# List active sessions
claude-code sessions list

# Agent status
pm2 status
```

### Task Queue

Agents pick up tasks from the shared queue:

```typescript
interface Task {
  id: string;
  type: 'pr_review' | 'code_write' | 'research' | 'outreach' | 'alert';
  assignee: ApostleName;
  priority: 'urgent' | 'high' | 'normal' | 'low';
  payload: Record<string, unknown>;
  status: 'pending' | 'in_progress' | 'completed' | 'failed';
  createdAt: Date;
  completedAt?: Date;
}
```

### Inter-Agent Communication

Agents coordinate via Mission Control:

```typescript
// Peter delegates to Andrew
await missionControl.delegate({
  from: 'Peter',
  to: 'Andrew',
  task: 'Implement EIP-3009 verification in facilitator',
  priority: 'high',
  deadline: '2026-02-15'
});

// Andrew reports completion
await missionControl.complete({
  taskId: 'task_123',
  result: { prUrl: 'github.com/shulam-pay/facilitator/pull/42' }
});
```

---

## Autonomous Operations

### Scheduled Tasks

| Agent | Schedule | Task |
|-------|----------|------|
| **Peter** | 8am daily | Morning briefing to Slack |
| **Matthias** | 6am daily | Generate metrics dashboard |
| **Thomas** | Hourly | Run test suite, report failures |
| **Simon** | On PR | Auto-deploy to staging |
| **Timothy** | Real-time | Screen transactions for OFAC |
| **Luke** | End of day | Compile changelog |

### Auto-Merge Guardrails

PRs can be auto-merged if:

```yaml
auto_merge_criteria:
  - all_checks_pass: true
  - min_approvals: 1  # Can be another agent
  - no_changes_to:
      - contracts/*
      - compliance/*
      - .env*
  - file_count_max: 10
  - line_diff_max: 500
  - author_in: [Andrew, Thomas, Thaddaeus, Simon]
```

Human approval required for:
- Smart contract changes
- Compliance code
- Environment/secrets
- Large refactors

---

## Directory Structure

```
souls/
├── README.md
├── agents/
│   ├── peter/
│   │   ├── SOUL.md           # Personality & responsibilities
│   │   ├── config.yaml       # Agent configuration
│   │   └── prompts/          # System prompts
│   ├── james/
│   ├── andrew/
│   └── ... (18 agents)
├── mission-control/
│   ├── schema.ts             # Convex schema
│   ├── tasks.ts              # Task queue logic
│   └── delegation.ts         # Inter-agent comms
├── harness/
│   ├── pm2.config.js         # Process manager config
│   ├── scheduler.ts          # Cron jobs
│   └── slack.ts              # Notification hooks
├── guardrails/
│   ├── auto-merge.yaml       # Merge criteria
│   ├── forbidden-paths.yaml  # Protected files
│   └── review-rules.yaml     # PR review requirements
└── scripts/
    ├── start-all.sh
    ├── stop-all.sh
    └── status.sh
```

---

## SOUL Files

Each agent has a `SOUL.md` defining their personality:

```markdown
# Andrew — Developer

## Identity
You are Andrew, Shulam's core developer. You ship reliable code quietly and efficiently.

## Personality
- Practical and grounded
- First to follow Peter's lead
- Prefers working code over perfect code
- Ships incrementally, iterates fast

## Responsibilities
- Core facilitator service
- Smart contract development
- Infrastructure and DevOps support
- Code review for other agents

## Tools
- GitHub (PRs, issues)
- Claude Code (implementation)
- Vercel (deployments)
- Base Sepolia (testnet)

## Communication Style
- Terse commit messages
- Detailed PR descriptions
- Asks clarifying questions before building
- Reports blockers immediately

## Boundaries
- Does NOT deploy to mainnet without Peter's approval
- Does NOT modify compliance code
- Escalates security concerns to Thomas
```

---

## Getting Started

### 1. Clone the repo

```bash
git clone git@github.com:shulam-pay/souls.git
cd souls
```

### 2. Install dependencies

```bash
npm install
```

### 3. Configure environment

```bash
cp .env.example .env
# Add: ANTHROPIC_API_KEY, SLACK_WEBHOOK, GITHUB_TOKEN
```

### 4. Start the harness

```bash
npm run harness:start
```

### 5. Check agent status

```bash
npm run status
```

---

## Slack Integration

Agents post to Slack channels:

| Channel | Purpose | Agents |
|---------|---------|--------|
| `#souls-alerts` | Urgent notifications | All |
| `#souls-deploys` | Deployment notifications | Simon |
| `#souls-prs` | PR activity | Andrew, Thomas |
| `#souls-metrics` | Daily metrics | Matthias |
| `#souls-support` | Merchant issues | Philip |

---

## Safety & Monitoring

### Kill Switch

Emergency stop all agents:

```bash
npm run harness:stop
# or
pm2 kill
```

### Rate Limits

| Resource | Limit |
|----------|-------|
| API calls per agent | 100/hour |
| PRs per day | 20 |
| Auto-merges per day | 10 |
| Slack messages per hour | 50 |

### Audit Log

All agent actions logged to Mission Control:

```typescript
{
  agent: 'Andrew',
  action: 'pr_created',
  target: 'facilitator#42',
  timestamp: '2026-02-10T21:30:00Z',
  approved_by: 'Thomas'  // If auto-merged
}
```

---

## License

Proprietary — Shulam, Inc.
