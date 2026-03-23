# Greentic Quickstart

A multi-channel chatbot demo using Greentic platform. Supports WebChat, Slack, Teams, Telegram, and Webex.

## Quick Start

### 1. Install GTC CLI

```bash
# macOS/Linux
curl -fsSL https://get.greentic.ai | sh

# Or via Homebrew
brew install greenticai/tap/gtc
```

### 2. Create Bundle

```bash
# Create bundle from wizard answers
gtc wizard --answers https://raw.githubusercontent.com/BimaPangestu28/greentic-quickstart/main/wizard-answers.json
```

This creates: `greentic-quickstart.gtbundle/`

### 3. Setup Secrets

```bash
# Generate private answers template
gtc setup ./greentic-quickstart.gtbundle --dry-run --emit-answers private-answers.json

# Edit private-answers.json with your secrets, then:
gtc setup ./greentic-quickstart.gtbundle --answers private-answers.json
```

### 4. Run

```bash
# Start with Cloudflare tunnel (public URL)
gtc start ./greentic-quickstart.gtbundle
```

## Supported Channels

| Channel | Setup Required |
|---------|---------------|
| WebChat GUI | None - works out of the box |
| Slack | Bot token from api.slack.com |
| Teams | Azure Bot registration |
| Telegram | Bot token from @BotFather |
| Webex | Bot token from developer.webex.com |

## Project Structure

```
greentic-quickstart/
├── wizard-answers.json          # Public config (no secrets)
├── private-answers-template.json # Template for secrets
├── bundle.yaml                   # Bundle definition
├── apps/
│   └── quickstart-app/          # Main application
│       └── flows/
│           ├── on_message.ygtc  # Chat handler
│           └── on_event.ygtc    # Webhook handler
└── packs/
    ├── component-msg2events/    # Message to events
    ├── component-events2msg/    # Events to message
    └── component-http/          # HTTP requests
```

## Configuration

### wizard-answers.json (Public)

Contains bundle configuration without secrets:
- Bundle ID and name
- Selected messaging providers
- App pack references

### private-answers.json (Secret - DO NOT COMMIT)

Contains your credentials:
- Slack bot token
- Teams app credentials
- Telegram bot token
- Webex bot token

## Flows

### on_message.ygtc

Handles incoming chat messages. Simple echo test by default.

### on_event.ygtc

Handles webhook events (GitHub, etc.).

## License

MIT
