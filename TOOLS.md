# TOOLS.md - Local Notes

Skills define _how_ tools work. This file is for _your_ specifics — the stuff that's unique to your setup.

## What Goes Here

Things like:

- Camera names and locations
- SSH hosts and aliases
- Preferred voices for TTS
- Speaker/room names
- Device nicknames
- Anything environment-specific

## Examples

```markdown
### Cameras

- living-room → Main area, 180° wide angle
- front-door → Entrance, motion-triggered

### SSH

- home-server → 192.168.1.100, user: admin

### TTS

- Preferred voice: "Nova" (warm, slightly British)
- Default speaker: Kitchen HomePod
```

## Why Separate?

Skills are shared. Your setup is yours. Keeping them apart means you can update skills without losing your notes, and share skills without leaking your infrastructure.

---

## SSH Hosts

### Tactlink DigitalOcean

- **Host alias:** `tactlink_do`
- **IP:** 188.166.189.200
- **Droplet:** tactlink-staging
- **User:** root
- **Key:** `~/.ssh/tactlink_do` (ed25519)
- **Key fingerprint:** SHA256:y43NAyJclONyB7v+BTX65lLJPvEor7vwOURYvGQJnoQ
- **Config location:** ~/.ssh/config (entry added)
- **Command:** `ssh tactlink_do`

### Public Key (for DigitalOcean Console)

Add your SSH public key to the `tactlink-staging` droplet in DigitalOcean:

```
[ADD_FROM_PASSWORD_MANAGER or ~/.ssh/id_*.pub]
```

---

## GitHub Access Tokens

### shinwong97 Personal Account (Kanban Dashboard)
- **Token:** `[ADD_FROM_PASSWORD_MANAGER]` (starts with `ghp_`)
- **Usage:** Push to `shinwong97/kanban-dashboard` repo
- **For commands:** `GH_TOKEN=[YOUR_TOKEN] git push origin main`

### TactLink-Malaysia Organization
- **Token:** `[ADD_FROM_PASSWORD_MANAGER]` (starts with `ghp_`)
- **Usage:** TactLink org repos (tactlink-app, services, etc.)

---

## Vercel Deployment

### Kanban Dashboard
- **Project ID:** `prj_YBuW6Lgc4XryEt8QMjceEDRdZtcg`
- **Project Name:** `kanban-agent-management`
- **GitHub Repo:** `shinwong97/kanban-dashboard` (personal account)
- **Live URL:** https://kanban-agent-management.vercel.app
- **Vercel API Token:** `[ADD_FROM_PASSWORD_MANAGER]` (starts with `vcp_`)
- **Auto-deploy:** Enabled on push to main branch
- **Build:** `npm run build`, Output: `.next`

---

## Figma

### Tactlink Design Files
- **Figma Token:** `[ADD_FROM_PASSWORD_MANAGER]` (starts with `figd_`)
- **Design File:** https://www.figma.com/design/saAOpeMi3YsvwefGMMBoMl/Tactlink-HIFI-Ui-Design-by-Amber--Copy-
- **Node ID for Mini Program Directory:** 83-1329
- **Usage:** Fetch design specs, translate UI to code

---

## Infrastructure

### DigitalOcean Spaces

- Storage service for Tactlink (Docker images, assets)
- Configured in tactlink services (see .env)

### Tactlink Services (Deployed)

- **API Gateway** (Production: dev.tactlink.com)
- **User Service**
- **Name Card Service**
- **Subscription Service** (WebSocket, commented in gateway)
- **Admin Backend**

### Kanban Dashboard Components

- **Frontend:** Next.js React
- **Database:** Supabase PostgreSQL
- **Real-time:** WebSocket
- **Notifications:** Telegram integration

### Agent Monitor Dashboard

- **Project:** `agent-monitor` (standalone)
- **Live URL:** https://agent-monitor-dun.vercel.app
- **Vercel Project ID:** `prj_TK7hsg6cVEDtH3qfiAa1XCTYaCUn`
- **Supabase:** Same as Kanban (yhrtnejoeenzjubbmttk)
- **Tables:** `monitor_agents`, `monitor_tasks`, `monitor_sessions`, `monitor_prompts`
- **Real-time:** Supabase subscriptions enabled on all 4 tables
- **Local path:** `agent-monitor/`

---

Add whatever helps you do your job. This is your cheat sheet.
