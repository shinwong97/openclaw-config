# OpenClaw Configuration Backup

This repository contains a backup of OpenClaw configuration files for easy restoration and version control.

## Files Included

- **SOUL.md** - Core identity and purpose definition
- **USER.md** - User profile and preferences
- **IDENTITY.md** - Identity configuration
- **AGENTS.md** - Agent definitions and workspace structure
- **TOOLS.md** - Local tools configuration (secrets sanitized)
- **MEMORY.md** - Long-term memory and learnings
- **BOOTSTRAP.md** - Bootstrap configuration (if applicable)

## Restore Instructions

### 1. Install OpenClaw

If you haven't already installed OpenClaw, follow the installation guide on the OpenClaw repository.

### 2. Copy Configuration Files

Clone this repository and copy the files to your OpenClaw workspace:

```bash
git clone https://github.com/shinwong97/openclaw-config.git
cp openclaw-config/*.md ~/.openclaw/workspace/
```

### 3. Restore Secrets

This repository does NOT contain API keys, tokens, or other secrets for security reasons.

Open `TOOLS.md` in the repository and add your secrets from your password manager:

- **GitHub Access Tokens** (starts with `ghp_`)
- **Vercel API Token** (starts with `vcp_`)
- **Figma Token** (starts with `figd_`)
- **SSH Public Keys** (if needed)
- Any other **.env** files or API keys

Refer to the placeholder comments in `TOOLS.md` for what needs to be restored.

### 4. Verify Restore

Check that all files are in place:

```bash
ls -la ~/.openclaw/workspace/*.md
```

You should see all the backup files listed.

## Security Note

⚠️ **This is a PUBLIC repository.** Secrets and API keys are intentionally excluded. Always manage secrets through your password manager or secure environment variable storage.

Never commit secrets to any repository, even private ones.

## Backup & Version Control

To keep this backup updated:

```bash
# Copy latest configs
cp ~/.openclaw/workspace/*.md /path/to/openclaw-config/

# Commit and push
cd /path/to/openclaw-config
git add *.md
git commit -m "Update OpenClaw config backup"
git push origin main
```

---

For more information about OpenClaw, visit the official repository.
