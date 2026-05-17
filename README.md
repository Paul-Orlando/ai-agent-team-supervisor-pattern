# AI Agent Team — Supervisor Pattern
### Flowise AgentFlows V2/V3 — Dynamic Multi-Agent Routing

A production-ready multi-agent software development team 
built using Flowise AgentFlows V2/V3. A Supervisor agent 
dynamically routes work between a Software Engineer and 
Code Reviewer, iterating until the solution is complete — 
then synthesizes a final production-ready deliverable.

---

## System Architecture

\`\`\`
User Request (chat input)
        ↓
┌─────────────────────────────────────────┐
│         SUPERVISOR (gpt-4o-mini)        │
│  Routes work to the right specialist   │
│  Decides: SOFTWARE | REVIEWER | FINISH │
└──────────────┬──────────────────────────┘
               ↓
    ┌──────────────────────┐
    │   CONDITION ROUTER   │
    │  Reads $flow.state   │
    └──┬───────────┬───────┘
       │           │          │
       ▼           ▼          ▼
  SOFTWARE     REVIEWER    FINISH
  ENGINEER     (QA Eng)      │
  Full Stack   Quality       │
  Developer    Assurance     │
       │           │          │
    Loop↑       Loop↑         │
   (max 5)    (max 5)         │
       └───────────┘          │
               └──────┬───────┘
                      ↓
          ┌───────────────────────┐
          │   FINAL ANSWER AGENT │
          │  Full code solution  │
          │  + improvements      │
          │  + QA review         │
          └───────────────────────┘
\`\`\`

---

## Agent Roles

| Agent | Role | Responsibility |
|---|---|---|
| Supervisor | Orchestrator | Routes tasks, manages flow state, decides when work is complete |
| Software Engineer | Developer | Full stack web development based on supervisor instructions |
| Code Reviewer | QA Engineer | Quality assurance, bug detection, improvement suggestions |
| Final Answer | Synthesizer | Combines full conversation into production-ready deliverable |

---

## Key Features

- Supervisor-pattern dynamic routing — not fixed linear chaining
- Structured output routing via enum state (SOFTWARE / REVIEWER / FINISH)
- Shared flow state management ($flow.state.next / instructions)
- Loop control — each agent iterates up to 5 times per cycle
- Full conversation memory shared across all agents
- Synthesis agent produces unified final deliverable
- Built on Flowise AgentFlows V2/V3 framework

---

## How the Supervisor Routes Work

The Supervisor uses structured output to decide the next worker:

| Decision | Action |
|---|---|
| `SOFTWARE` | Routes to Software Engineer for development |
| `REVIEWER` | Routes to Code Reviewer for QA |
| `FINISH` | Routes to Final Answer synthesis |

Each routing decision includes specific instructions passed
via `$flow.state.instructions` to the receiving agent.

---

## Tech Stack

- **Flowise AgentFlows V2/V3** — visual agentic workflow engine
- **OpenAI API** — gpt-4o-mini (all agents)
- **LangChain** — agent orchestration framework
- **Condition Nodes** — dynamic state-based routing
- **Loop Nodes** — iterative refinement control

---

## Agent Configuration

| Setting | Value |
|---|---|
| Model | gpt-4o-mini |
| Temperature | 0.9 |
| Memory | All messages (shared) |
| Max Loops | 5 per agent |
| Routing | Enum structured output |
| Framework | Flowise AgentFlows V2/V3 |

---

## Setup & Import

1. Install and run Flowise:
\`\`\`bash
npm install -g flowise
npx flowise start
\`\`\`

2. Open Flowise at `http://localhost:3000`

3. Import the agent:
   - Click **Agentflows** → **Add New**
   - Click **Import**
   - Upload `ai_agent_team.json`

4. Add your OpenAI API key in Flowise credentials

5. Click **Save** and **Deploy**

6. Enter a software development request to start

---
**Supervisor** analyzes the request and routes to
Software Engineer with specific instructions.

**Software Engineer** builds the implementation,
loops back to Supervisor when complete.

**Supervisor** routes to Code Reviewer for QA.

**Code Reviewer** checks for bugs, security issues,
and improvements, loops back to Supervisor.

**Supervisor** decides work is complete → FINISH.

**Final Answer Agent** synthesizes:
- Full working code
- Security improvements
- QA review summary
- Implementation notes

---

## Supervisor Pattern vs Sequential Pipeline

| Approach | This Repo | Previous Repo |
|---|---|---|
| Routing | Dynamic (Supervisor decides) | Fixed linear sequence |
| Iteration | Loop-based (up to 5x) | Single pass |
| Flexibility | High — any agent can be called multiple times | Low — fixed order |
| Framework | AgentFlows V2/V3 | Sequential Agents |
| Best for | Complex iterative tasks | Linear content pipelines |

---

## Customization

**Change the team composition**
Replace Software Engineer and Code Reviewer with any
specialist agents — Data Analyst, Content Writer,
SEO Specialist, etc.

**Adjust loop limits**
Increase or decrease max loop count per agent
in the Loop nodes.

**Add more specialists**
Add additional agent nodes and update the Supervisor's
enum values and routing logic.

**Change the model**
Swap gpt-4o-mini for gpt-4o or any supported
OpenAI model in each agent node.

---

## Related Repos

| Repo | Pattern | Framework |
|---|---|---|
| [ai-multi-agent-content-pipeline](https://github.com/Paul-Orlando/ai-multi-agent-content-pipeline) | Sequential | Flowise Sequential Agents |
| [ai-web-scraper-research-agent](https://github.com/Paul-Orlando/ai-web-scraper-research-agent) | RAG Pipeline | Flowise + FAISS |
| [ai-research-assistant-rag](https://github.com/Paul-Orlando/ai-research-assistant-rag) | RAG + Python | Python + OpenAI |

---

## Changelog

See [changelog.md](changelog.md) for full version history.

---

## Author

Paul Orlando
Creative Technologist | AI Agent Developer | Data Analytics
🌐 [paulforlando.com](https://www.paulforlando.com)
💼 [LinkedIn](https://www.linkedin.com/in/paul-orlando-7841b5154)
🐙 [GitHub](https://github.com/Paul-Orlando)
