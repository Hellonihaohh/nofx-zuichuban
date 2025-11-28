# NOFX – AI Automated Trading System (Early Version)

NOFX is an AI-driven automated trading framework designed for futures/spot trading, high-frequency execution, and intelligent decision-making.  
This repository contains the **initial development version**, packaged inside `nofx-dev.zip`.

This document explains how to install, configure, and use NOFX from scratch.

---

# 📦 1. Download the Project

This repository includes:

nofx-dev.zip

yaml
复制代码

Download it, unzip it, and you will see:

api/
trader/
config/
docker/
scripts/
market/
prompts/
docker-compose.yml
...

yaml
复制代码

These are the full project files required to run NOFX.

---

# 🐳 2. Requirements

To run NOFX, the following are required:

- **Docker 24+**
- **Docker Compose v2**
- At least **4GB RAM**
- Linux / Windows / macOS supported

Recommended server:

- 2 CPU cores / 4GB RAM  
- Ubuntu 22.04 LTS

---

# ⚙️ 3. Configure NOFX

After unzipping, open the root project folder:

cd nofx-dev/

css
复制代码

Find the main configuration file:

config/config.json

csharp
复制代码

Edit it with your own API keys:

```json
{
  "exchange": "binance",
  "apiKey": "YOUR_API_KEY",
  "secretKey": "YOUR_SECRET_KEY",
  "password": "",
  "symbol": "BTCUSDT",
  "aiProvider": "openai",
  "aiApiKey": "YOUR_AI_API_KEY"
}
Field explanation:
Field	Description
exchange	Trading exchange: binance / okx / bybit
apiKey	API key from your exchange
secretKey	Secret key from your exchange
symbol	Trading pair (ex: BTCUSDT)
aiProvider	AI model provider: openai / claude / deepseek
aiApiKey	API key for the AI model

⚠️ Important:
Use demo/sandbox API keys for safety.

🚀 4. Start NOFX
Run the system using Docker:

bash
复制代码
docker compose up -d --build
This starts several services:

Service	Description
nofx-backend	Main backend and trading engine
nofx-db	Database for logs and positions
nofx-web (opt.)	API gateway or web layer

Check logs:

bash
复制代码
docker logs -f nofx-backend
If you see:

pgsql
复制代码
NOFX system started successfully
AI engine online
Exchange connection OK
It is running correctly.

🔥 5. How NOFX Works
NOFX automatically performs:

✔ 1. Market Analysis
Fetches candles, volatility, volume, indicators, order flow, etc.

✔ 2. AI Decision Making
AI generates actionable instructions like:

scss
复制代码
BUY(BTCUSDT, 0.01)
STOPLOSS(61800)
TAKEPROFIT(63100)
✔ 3. Automated Order Execution
Orders are placed through exchange API.

✔ 4. Risk Control
Stop loss, take profit, trailing stop and position monitoring.

✔ 5. State Logging
All activity is stored in the database.

📊 6. Monitoring Trades
To watch real-time trading activity:

bash
复制代码
docker logs -f nofx-backend
Example log output:

csharp
复制代码
[AI] Market trend detected: bullish
[Trade] Long BTCUSDT 0.01
[Risk] Stop loss placed at 61800
[System] Position opened successfully
🛠 7. Project Directory Structure
pgsql
复制代码
api/           → Backend API services
auth/          → Authentication and token logic
trader/        → Trading engine & order executor
market/        → Market data collectors
config/        → Main configuration files
docker/        → Docker deployment files
scripts/       → Utility scripts
prompts/       → AI prompt templates
logs/          → System & trade logs (generated after running)
❓ 8. FAQ
Q1: AI model returns errors?
Check if your aiApiKey is valid and not expired.

Q2: Orders cannot be placed?
Possible reasons:

API key missing trading permission

Exchange requires IP whitelisting (common on OKX)

Not enough balance

Trading pair unavailable on the selected exchange

Q3: Docker fails to start?
Restart with:

bash
复制代码
docker compose down
docker compose up -d
🌟 9. Upcoming Features
Future improvements planned:

UI dashboard (web version)

Spot & futures grid trading

Strategy optimizer powered by AI

Multi-account support

Automatic risk management upgrades

Exchange support expansion

🤝 10. Contribution
Pull requests and issues are welcome.
You may modify or extend the system based on your needs.
