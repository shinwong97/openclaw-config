# OpenClaw Configuration Backup

Complete backup of the `~/.openclaw` directory structure for OpenClaw agent framework. Similar to [JosephSaw/openclaw-workspace](https://github.com/JosephSaw/openclaw-workspace).

## 🔒 Security Notice

**Credentials are sanitized in this repository.** All sensitive values are replaced with `[ADD_FROM_PASSWORD_MANAGER]` placeholders.

**Before deploying**, you MUST restore:
- `openclaw.json` - Gateway URL, token, bot credentials
- `credentials/telegram-*.json` - Bot tokens, user IDs
- `agents/main/agent/auth-profiles.json` - API keys
- `identity/device*.json` - Authentication tokens

## Directory Structure

```
openclaw-config/
├── agents/main/
│   ├── agent/
│   │   ├── auth-profiles.json    # [SANITIZED] API key profiles
│   │   └── models.json           # Model configurations
│   └── sessions/                 # [EXCLUDED] Session logs (restore from ~/.openclaw)
├── canvas/                       # Canvas UI configurations
├── credentials/                  # [SANITIZED] Telegram bot config
├── cron/                         # Scheduled job definitions
├── devices/                      # Device pairing configurations
├── identity/                     # [SANITIZED] Device identity & auth
├── telegram/                     # Telegram integration setup
├── openclaw.json                 # [SANITIZED] Main config
└── README.md                     # This file
```

## Restoration Guide

### Quick Start

```bash
# 1. Clone this repository
git clone https://github.com/shinwong97/openclaw-config.git
cd openclaw-config

# 2. Backup existing ~/.openclaw (if it exists)
mv ~/.openclaw ~/.openclaw.backup.$(date +%s)

# 3. Copy configuration to home
cp -r . ~/.openclaw/

# 4. Fix permissions
chmod 700 ~/.openclaw
chmod 600 ~/.openclaw/{openclaw.json,credentials/*.json,agents/main/agent/*.json}

# 5. Restore secrets from password manager (SEE BELOW)
nano ~/.openclaw/openclaw.json

# 6. Verify installation
openclaw gateway status
```

### Step-by-Step: Restoring Credentials

#### 1. Main Config (`openclaw.json`)

Replace placeholders with your actual values:

```json
{
  "agent": {
    "name": "main",
    "model": "anthropic/claude-haiku-4-5"
  },
  "gateway": {
    "url": "https://your-gateway-domain.com",
    "token": "gw_actual_token_here"
  },
  "telegram": {
    "botToken": "123456:ABC-DEF1234ghIkl-zyx57W2v1u123ew11",
    "allowFrom": "your_user_id,other_user_id"
  }
}
```

**Location:** `~/.openclaw/openclaw.json`

#### 2. Telegram Credentials (`credentials/telegram-allowFrom.json`)

```json
{
  "version": 1,
  "botToken": "123456:ABC-DEF1234ghIkl-zyx57W2v1u123ew11",
  "allowFrom": ["123456789", "987654321"],
  "chatIds": {
    "main": "123456789"
  }
}
```

**Location:** `~/.openclaw/credentials/telegram-allowFrom.json`

#### 3. Agent Credentials (`agents/main/agent/auth-profiles.json`)

Replace the Anthropic API key:

```json
{
  "version": 1,
  "profiles": {
    "anthropic:default": {
      "type": "api_key",
      "provider": "anthropic",
      "key": "sk-ant-actual-api-key-here"
    }
  },
  "lastGood": { "anthropic": "anthropic:default" },
  "usageStats": {}
}
```

**Location:** `~/.openclaw/agents/main/agent/auth-profiles.json`

#### 4. Device Identity (`identity/device.json`, `identity/device-auth.json`)

Restore from your password manager.

#### 5. Session Logs (Optional)

Session logs are excluded from this repo for security. To restore them:

```bash
# If you have a backup
cp /backup/path/~/.openclaw/agents/main/sessions/* ~/.openclaw/agents/main/sessions/

# Or regenerate by running OpenClaw
openclaw gateway restart
```

### What's Included vs. Excluded

✅ **Included:**
- `agents/main/agent/` - Configuration structure
- `canvas/` - Canvas settings
- `credentials/` - Sanitized placeholders
- `cron/` - Job definitions
- `devices/` - Device pairing setup
- `identity/` - Identity structure
- `telegram/` - Telegram integration config
- `openclaw.json` - Main config template

❌ **Excluded (Restore Separately):**
- `agents/main/sessions/` - Session logs with API interactions
- `workspace/` - Use git to restore individual projects
- `logs/`, `media/`, `browser/` - Runtime data
- `node_modules/` - Run `npm install` in workspace

## Using with an Existing ~/.openclaw

If you have an existing OpenClaw setup:

```bash
# Merge specific directories
cp -r agents/* ~/.openclaw/agents/
cp -r credentials/* ~/.openclaw/credentials/
cp -r cron/* ~/.openclaw/cron/
# ... etc for other directories

# Then restore secrets in the merged files
```

## Version Control & Updates

Keep this repo updated with your OpenClaw configuration:

```bash
# Copy updated config back
cp -r ~/.openclaw/* /path/to/openclaw-config/

# Sanitize secrets before committing
nano credentials/telegram-allowFrom.json  # Replace actual values
nano openclaw.json                        # Replace actual tokens

# Commit and push
git add -A
git commit -m "Update OpenClaw config"
git push origin main
```

### Recommended .gitignore for Local Changes

Add to `.git/info/exclude` (local gitignore):

```
# Local secrets (never commit)
openclaw.json.actual
credentials/*.secret.json
agents/main/sessions/

# Large files
workspace/node_modules/
```

## Project Structure

- **agents/** - Agent definitions and authentication
- **canvas/** - Visual rendering configurations
- **credentials/** - Service credentials (Telegram, etc.)
- **cron/** - Scheduled task definitions
- **devices/** - Connected device configurations
- **identity/** - Device and agent identity
- **telegram/** - Telegram bot integration
- **workspace/** - User workspace (managed separately)

## Security Considerations

1. **Never commit secrets** - GitHub secret scanning will catch them
2. **Use environment variables** for sensitive values in production
3. **Rotate credentials regularly** - especially API keys
4. **Backup encrypted** - store backups in a secure location
5. **Use password manager** - keep actual credentials in 1Password, Bitwarden, etc.

## Troubleshooting

### Gateway Connection Failed

Check `openclaw.json`:
- Verify `gateway.url` is correct
- Verify `gateway.token` is valid
- Ensure no spaces in token

### Telegram Bot Not Responding

Check `credentials/telegram-allowFrom.json`:
- Verify `botToken` is valid
- Verify your user ID in `allowFrom`
- Verify chat ID in `chatIds`

### Permissions Errors

```bash
# Fix directory permissions
chmod 700 ~/.openclaw
chmod 700 ~/.openclaw/{agents,credentials,identity}
chmod 600 ~/.openclaw/*.json
chmod 600 ~/.openclaw/**/*.json
```

## Reference Projects

- [OpenClaw Docs](https://github.com/shinwong97/openclaw)
- [JosephSaw/openclaw-workspace](https://github.com/JosephSaw/openclaw-workspace)

## License

Personal configuration backup. Use freely; adjust to your needs.

---

**Last Updated:** 2026-02-24  
**Host:** Mac mini (arm64)  
**OpenClaw Version:** Latest
