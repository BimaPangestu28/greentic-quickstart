# Greentic Quickstart

A multi-channel chatbot demo using Greentic platform. Supports WebChat, Slack, Teams, Telegram, and Webex.

## Quick Start (Local Development)

### 1. Install GTC CLI

```bash
# macOS/Linux
curl -fsSL https://get.greentic.ai | sh

# Or via Homebrew
brew install greenticai/tap/gtc
```

### 2. Clone and Setup

```bash
# Clone the repo
git clone https://github.com/BimaPangestu28/greentic-quickstart.git
cd greentic-quickstart

# Download provider packs (first time only)
gtc setup .

# Copy and edit your secrets
cp private-answers-template.json private-answers.json
# Edit private-answers.json with your credentials

# Run setup with your secrets
gtc setup --answers private-answers.json .
```

### 3. Run

```bash
# Start with Cloudflare tunnel (public URL)
gtc start .

# Or with ngrok instead
gtc start . --cloudflared off --ngrok on
```

The WebChat GUI is available at the public URL shown in the console.

---

## Alternative: Wizard Flow (OCI Registry)

For automated bundle creation from published packs:

### 1. Create Bundle from Wizard

```bash
# Create bundle directly from URL (requires gtc >= 0.4.63)
gtc wizard --answers https://raw.githubusercontent.com/BimaPangestu28/greentic-quickstart/main/wizard-answers.json --yes --non-interactive
```

This creates: `greentic-quickstart.gtbundle/`

### 2. Setup Secrets

```bash
# Generate private answers template
gtc setup ./greentic-quickstart.gtbundle --dry-run --emit-answers private-answers.json

# Edit private-answers.json with your secrets, then:
gtc setup ./greentic-quickstart.gtbundle --answers private-answers.json
```

### 3. Run

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
