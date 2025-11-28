
# NOFX – AI-Driven Crypto Trading (First Dev Version)

NOFX is an AI-assisted crypto trading framework.  
It connects a large-language-model (LLM) with your exchange account, so the AI can read market data, follow your rules, and automatically place trades.

> **Status:** Early developer preview – for testing, research and paper-trading.  
> **Use at your own risk.** Always start with demo / small size.

---

## What NOFX Can Do

- **AI Trading Assistant**
  - Uses an AI model (via API) to read market context and your instructions.
  - Generates trade ideas (long/short, entry, stop, take-profit, size).
  - Can be tuned for trend-following, scalping, grid-style, etc. by changing the prompt.

- **Rule-Based Risk Management**
  - Fixed or percentage-based position sizing.
  - Take-profit / stop-loss suggested by the AI but checked against your limits.
  - Optional max daily loss / max concurrent positions (depending on config).

- **Exchange Integration**
  - Connects to crypto exchanges through API keys (e.g. futures / perpetuals).
  - Supports paper-trading / sandbox first (recommended).

- **Web UI**
  - Simple dashboard to:
    - Configure API keys and secrets.
    - Edit the AI prompt / strategy template.
    - Monitor open positions and recent trades.
    - View basic logs of AI decisions.

- **Log & Replay**
  - Stores AI prompts and responses for later review.
  - Helps you iterate and improve the prompt / strategy.

---

## Project Structure (Dev Package)

After extracting `nofx-dev.zip` you will typically see:

- `docker/` – Dockerfiles and runtime scripts.
- `start.sh` – Helper script to build and run the stack.
- `config.example.json` – Example configuration.
- `config.json` – Your actual configuration (created by you).
- `README.md` – This file.

The first dev version focuses on **backend + basic UI**.  
Models are **not** stored on the server; they are called via external API.

---

## Prerequisites

- A Linux server or VPS (recommended) or a local machine.
- **Docker** and **Docker Compose** installed.
- An AI provider API key (e.g. OpenAI-compatible endpoint).
- Exchange API key/secret (paper or real – start with paper).

---

## Quick Deployment (Docker, Recommended)

### 1. Download & Extract

```bash
# On your server
cd /www/wwwroot   # or any directory you prefer
# Upload nofx-dev.zip to this folder first (via GitHub download / SFTP / panel)
unzip nofx-dev.zip -d nofx
cd nofx
2. Create Configuration
Copy the example config and edit it:

cp config.example.json config.json
nano config.json
In config.json set at least:

AI settings

model_base_url – your AI API endpoint.

model_api_key – your API key.

model_name – model ID to use.

Exchange settings

exchange – exchange name / ID.

api_key / api_secret / passphrase (if needed).

testnet – true for paper-trading, false for live.

Risk settings

max_leverage

position_size_pct

max_daily_loss_pct, etc.

Never commit config.json with real keys back to GitHub.

3. Start the Stack
Use the helper script (first run builds the images):

chmod +x start.sh

# Build and start
./start.sh start --build
This will internally run docker compose and start the NOFX service.

To stop or restart:

# Stop containers
./start.sh stop

# Start again (no rebuild)
./start.sh start
4. Access the Web UI
By default (see docker-compose.yml) the backend is exposed on:

http://<your-server-ip>:8080
If you changed NOFX_BACKEND_PORT in your environment, open that port instead.

Basic Usage
Open the dashboard in your browser.

Complete the setup wizard (if available) or:

Paste your AI API key and endpoint.

Paste your exchange API key/secret.

Select testnet / paper mode.

Edit the AI Prompt / Strategy

Describe how the AI should trade (trend / scalping / grid).

Define the timeframe, assets, max positions and risk rules.

Start AI Trading

Begin in paper mode.

Watch the log panel to see:

AI analysis of the market.

Proposed orders and risk parameters.

Verify orders on the exchange.

Iterate

Adjust the prompt, risk settings, or markets.

Review logs and results; refine your instructions.

Development (Optional)
If you want to modify the code:

# after editing the source
./start.sh rebuild   # or ./start.sh start --build
You can also use the raw Docker Compose commands:

docker compose up -d --build
docker compose logs -f
docker compose down
Security & Disclaimer
Never share your API keys. Keep config.json private and out of version control.

Start on testnet / demo with the smallest sizes possible.

This software provides tools for automation, not financial advice.

You are fully responsible for all trades and losses that may result from using NOFX.

License
This is an early dev version.
See the repository’s LICENSE file (or contact the author) for current licensing and usage terms.
