OpenClaw Mission Control is the centralized operations and governance platform for running OpenClaw across teams and organizations, with unified visibility, approval controls, and gateway-aware orchestration. It gives operators a single interface for work orchestration, agent and gateway management, approval-driven governance, and API-backed automation.
Platform overview
Mission Control is designed to be the day-to-day operations surface for OpenClaw. Instead of splitting work across multiple tools, teams can plan, execute, review, and audit activity in one system.

Core operational areas:

Work orchestration: manage organizations, board groups, boards, tasks, and tags.
Agent operations: create, inspect, and manage agent lifecycle from a unified control surface.
Governance and approvals: route sensitive actions through explicit approval flows.
Gateway management: connect and operate gateway integrations for distributed environments.
Activity visibility: review a timeline of system actions for faster debugging and accountability.
API-first model: support both web workflows and automation clients from the same platform.
Use cases
Multi-team agent operations: run multiple boards and board groups across organizations from a single control plane.
Human-in-the-loop execution: require approvals before sensitive actions and keep decision trails attached to work.
Distributed runtime control: connect gateways and operate remote execution environments without changing operator workflow.
Audit and incident review: use activity history to reconstruct what happened, when it happened, and who initiated it.
API-backed process integration: connect internal workflows and automation clients to the same operational model used in the UI.
What makes Mission Control different
Operations-first design: built for running agent work reliably, not just creating tasks.
Governance built in: approvals, auth modes, and clear control boundaries are first-class.
Gateway-aware orchestration: built to operate both local and connected runtime environments.
Unified UI and API model: operators and automation act on the same objects and lifecycle.
Team-scale structure: organizations, board groups, boards, tasks, tags, and users in one system of record.
Who it is for
Platform teams running OpenClaw in self-hosted or internal environments.
Operations and engineering teams that need clear approval and auditability controls.
Organizations that want API-accessible operations without losing a usable web UI.
Get started in minutes
Option A: One-command production-style bootstrap
If you haven't cloned the repo yet, you can run the installer in one line:

curl -fsSL https://raw.githubusercontent.com/abhi1693/openclaw-mission-control/master/install.sh | bash
This clones the repository into ./openclaw-mission-control if no local checkout is found in your current directory.

If you already cloned the repo:

./install.sh
The installer is interactive and will:

Ask for deployment mode (docker or local).
Install missing system dependencies when possible.
Generate and configure environment files.
Bootstrap and start the selected deployment mode.
Installer support matrix: docs/installer-support.md

Option B: Manual setup
Prerequisites
Supported platforms: Linux and macOS. On macOS, Docker mode requires Docker Desktop; local mode requires Homebrew and Node.js 22+.
Docker Engine
Docker Compose v2 (docker compose)
1. Configure environment
cp .env.example .env
Before startup:

Set LOCAL_AUTH_TOKEN to a non-placeholder value (minimum 50 characters) when AUTH_MODE=local.
NEXT_PUBLIC_API_URL=auto (default) resolves to http(s)://<current-host>:8000.
Set an explicit URL when your API is behind a reverse proxy or non-default port.
2. Start Mission Control
docker compose -f compose.yml --env-file .env up -d --build
If you are iterating on the UI in Docker and want automatic frontend rebuilds on source changes, run:

docker compose -f compose.yml --env-file .env up --build --watch
Notes:

Compose Watch requires Docker Compose 2.22.0+.
You can also run watch separately after startup:
docker compose -f compose.yml --env-file .env up -d --build
docker compose -f compose.yml --env-file .env watch
After pulling new changes, rebuild and recreate all services:

docker compose -f compose.yml --env-file .env up -d --build --force-recreate
For a fully clean rebuild (no cached build layers):

docker compose -f compose.yml --env-file .env build --no-cache --pull
docker compose -f compose.yml --env-file .env up -d --force-recreate
3. Open the application
Mission Control UI: http://localhost:3000
Backend health: http://localhost:8000/healthz
4. Stop the stack
docker compose -f compose.yml --env-file .env down
Authentication
Mission Control supports two authentication modes:

local: shared bearer token mode (default for self-hosted use)
clerk: Clerk JWT mode
Environment templates:

Root: .env.example
Backend: backend/.env.example
Frontend: frontend/.env.example
