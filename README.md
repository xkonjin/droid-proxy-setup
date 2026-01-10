# Factory Droid Proxy Setup

Auto-start CLIProxyAPI for Factory Droid with Claude Pro Max, ChatGPT Pro Max, and Google Antigravity (Gemini) support.

## What This Does

Uses [CLIProxyAPI](https://github.com/router-for-me/CLIProxyAPI) to proxy your subscription OAuth tokens to Factory Droid, allowing you to use:

- **Claude Pro Max** - Claude Opus 4.5, Sonnet 4.5, Haiku 4.5
- **ChatGPT Pro Max** - GPT-5.2-Codex-Max, GPT-5
- **Google Antigravity** - Gemini 3 Pro, Gemini 2.5 Pro

## Installation

### Prerequisites
- Go 1.24+ installed (`brew install go`)
- Factory Droid CLI installed
- Active subscriptions (Claude Pro Max / ChatGPT Pro / Google One AI Premium)

### 1. Clone and Build CLIProxyAPI

```bash
cd ~
git clone https://github.com/router-for-me/CLIProxyAPI.git
cd CLIProxyAPI
go build -o cli-proxy-api ./cmd/server
```

### 2. Copy Config Files

```bash
# Copy proxy config
cp config.yaml ~/CLIProxyAPI/config.yaml

# Copy Factory config
cp factory-config.json ~/.factory/config.json

# Copy LaunchAgent (macOS auto-start)
cp com.cliproxyapi.plist ~/Library/LaunchAgents/
```

### 3. Authenticate OAuth

```bash
cd ~/CLIProxyAPI

# Claude Pro Max
./cli-proxy-api --claude-login

# ChatGPT Pro Max (Codex)
./cli-proxy-api --codex-login

# Google Antigravity (Gemini)
./cli-proxy-api --antigravity-login
```

### 4. Start the Service

```bash
# Load LaunchAgent (auto-starts on login)
launchctl load ~/Library/LaunchAgents/com.cliproxyapi.plist

# Or start manually
cd ~/CLIProxyAPI && ./cli-proxy-api --config config.yaml
```

### 5. Use in Droid

```bash
droid
/model  # Select your model
```

## Available Models (Latest Only)

| Provider | Model ID | Description |
|----------|----------|-------------|
| Claude | `claude-opus-4-5-20251101` | Opus 4.5 - Most capable |
| Claude | `claude-sonnet-4-5-20250929` | Sonnet 4.5 - Best balance |
| Claude | `claude-haiku-4-5-20251001` | Haiku 4.5 - Fastest |
| OpenAI | `gpt-5.2-codex-max` | GPT-5.2 Codex Max - Latest |
| Google | `gemini-3-pro` | Gemini 3 Pro - Latest |

## Troubleshooting

### Check if proxy is running
```bash
launchctl list | grep cliproxyapi
# Or
ps aux | grep cli-proxy-api
```

### View logs
```bash
tail -f ~/CLIProxyAPI/proxy.log
```

### Restart service
```bash
launchctl unload ~/Library/LaunchAgents/com.cliproxyapi.plist
launchctl load ~/Library/LaunchAgents/com.cliproxyapi.plist
```

### Re-authenticate
```bash
cd ~/CLIProxyAPI
./cli-proxy-api --claude-login
./cli-proxy-api --codex-login
./cli-proxy-api --antigravity-login
```

## Credits

- [CLIProxyAPI](https://github.com/router-for-me/CLIProxyAPI) by router-for-me
- [Factory Droid](https://factory.ai)
