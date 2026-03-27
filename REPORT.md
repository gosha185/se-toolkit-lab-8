# Lab 8 — Report

Paste your checkpoint evidence below. Add screenshots as image files in the repo and reference them with `![description](path)`.

## Task 1A — Bare agent

### Question 1: "What is the agentic loop?"

**Response:**

The agentic loop is the fundamental cycle that autonomous AI agents follow to accomplish tasks. It typically consists of these core stages:

 1. **Perceive** — Gather information from the environment (user input, tool outputs, external data)
 2. **Reason** — Analyze the information, plan next steps, and make decisions about what actions to take
 3. **Act** — Execute actions using available tools (file operations, API calls, web searches, etc.)
 4. **Reflect** — Evaluate the results of actions, check if the goal is achieved, and adjust the plan if needed

This loop repeats until the task is complete or a stopping condition is met.

Key characteristics:
- **Autonomy** — The agent decides what to do next without constant human guidance
- **Iterative** — Multiple loop cycles may be needed for complex tasks
- **Goal-driven** — Each iteration moves toward completing an objective
- **Adaptive** — The agent can adjust its approach based on feedback from previous actions

### Question 2: "What labs are available in our LMS?"

**Response:**

Based on the workspace, I can see several labs available in your software engineering toolkit:

Available Labs:
 1. lab-01-market-product-and-git — Market, product, and Git fundamentals
 2. se-toolkit-lab-2 — Lab 2
 3. se-toolkit-lab-3 — Lab 3
 4. se-toolkit-lab-4 — Lab 4
 5. se-toolkit-lab-5 — Lab 5
 6. se-toolkit-lab-6 — Lab 6
 7. se-toolkit-lab-7 — Lab 7
 8. se-toolkit-lab-8 — Lab 8 (currently active in your nanobot context)

You have 8 labs total in your LMS workspace.

> **Note:** The bare agent answered by scanning the filesystem, not by calling LMS API tools (which it doesn't have yet).

## Task 1B — Agent with LMS tools

### Question 1: "What labs are available?"

**Response:**

The LMS backend is currently empty (0 items) and the sync pipeline is encountering an error. However, based on the filesystem, I can see these lab directories are available:

Labs on Filesystem:
 1. lab-01-market-product-and-git
 2. se-toolkit-lab-2
 3. se-toolkit-lab-3
 4. se-toolkit-lab-4
 5. se-toolkit-lab-5
 6. se-toolkit-lab-6
 7. se-toolkit-lab-7
 8. se-toolkit-lab-8

The LMS backend needs to be synced to load these labs. The sync pipeline is currently failing with a 500 error.

> **Note:** The agent used the `lms_health` MCP tool to check the backend status and reported that it's empty (0 items).

### Question 2: "Describe the architecture of the LMS system"

**Response:**

The agent provided a comprehensive architecture description including:

**System Overview:**
The LMS is a Docker Compose-based system with 7 containers that provides an educational platform where students can browse learning items, log interactions, and query data through an AI agent interface.

**Container Architecture:**
- **Caddy** — Reverse Proxy & Static Server (port 42002)
- **FastAPI Backend** — REST API (port 8000)
- **PostgreSQL** — Database (port 42004)
- **pgAdmin** — Database UI (port 42003)
- **Nanobot** — AI Agent Gateway (WebSocket :8765, HTTP :18790)
- **Telegram Bot** — Optional Client (aiogram)
- **React SPA** — Frontend (static files)

**Data Model (OBER-based):**
- **Item** — tree hierarchy (course/lab/task/step)
- **Learner** — student records
- **Interacts** — interaction logs

**Communication Flows:**
1. Student browses items: Browser → Caddy → FastAPI → PostgreSQL
2. AI agent queries data: Nanobot → MCP tools → FastAPI → PostgreSQL
3. Telegram chat: Telegram → Bot → WebSocket → Nanobot → LLM → MCP → LMS

> **Note:** The agent used MCP tools (`lms_health`, `lms_labs`) and filesystem access to provide this comprehensive answer.

## Task 1C — Skill prompt

### Question: "Show me the scores" (without specifying a lab)

**Response:**

The agent responded with a comprehensive explanation:

The LMS backend currently has no labs loaded (empty database). The agent checked the sync status and explained:

**Current Status:**
- ✅ LMS backend is healthy
- ❌ No labs/items loaded (item_count: 0)
- ❌ Sync pipeline failed (500 Internal Server Error)

**To see scores, you need to:**
1. Run the LMS sync pipeline to load lab data from the filesystem into the database
2. Ensure learners and submissions exist in the system

The LMS uses an ETL pipeline to sync data from an external autochecker API. The database is currently empty because the sync pipeline needs credentials (AUTOCHECKER_EMAIL, AUTOCHECKER_PASSWORD, AUTOCHECKER_API_URL).

**Available score-related tools:**
- `mcp_lms_lms_pass_rates(lab="lab-04")` - pass rates per task
- `mcp_lms_lms_groups(lab="lab-04")` - group performance
- `mcp_lms_lms_top_learners(lab="lab-04")` - top learners
- `mcp_lms_lms_completion_rate(lab="lab-04")` - completion rate

> **Note:** The skill prompt guided the agent to explain the situation clearly and suggest next steps, rather than just saying "no data". The agent also listed available tools for when the data is populated.

### Follow-up: "What is the completion rate for lab-04?"

**Response:**

The completion rate for lab-04 is:

| Metric          | Value |
|-----------------|-------|
| Completion Rate | 0.0%  |
| Passed          | 0     |
| Total           | 0     |

This shows 0% because the LMS database is currently empty - no learners or submissions have been synced yet. The ETL pipeline needs to be configured with autochecker API credentials and run to populate the database with actual student data.

## Task 2A — Deployed agent

<!-- Paste a short nanobot startup log excerpt showing the gateway started inside Docker -->

## Task 2B — Web client

<!-- Screenshot of a conversation with the agent in the Flutter web app -->

## Task 3A — Structured logging

<!-- Paste happy-path and error-path log excerpts, VictoriaLogs query screenshot -->

## Task 3B — Traces

<!-- Screenshots: healthy trace span hierarchy, error trace -->

## Task 3C — Observability MCP tools

<!-- Paste agent responses to "any errors in the last hour?" under normal and failure conditions -->

## Task 4A — Multi-step investigation

<!-- Paste the agent's response to "What went wrong?" showing chained log + trace investigation -->

## Task 4B — Proactive health check

<!-- Screenshot or transcript of the proactive health report that appears in the Flutter chat -->

## Task 4C — Bug fix and recovery

<!-- 1. Root cause identified
     2. Code fix (diff or description)
     3. Post-fix response to "What went wrong?" showing the real underlying failure
     4. Healthy follow-up report or transcript after recovery -->
