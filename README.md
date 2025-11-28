# NOFX – AI-Powered Automated Trading System (Initial Version)

NOFX is an AI-driven automated trading framework designed for futures/spot trading, trend detection, high-frequency execution, and intelligent trading decisions.  
This repository contains the **initial development version** packaged as `nofx-dev.zip`.  
Below is the quick start guide and full usage documentation.

---

## 📦 1. Download & Extract

Download the project files from this repository:

nofx-dev.zip


Unzip it and you will see:

api/
trader/
config/
docker/
scripts/
market/
prompts/
docker-compose.yml
...


---

## 🐳 2. Requirements

Before running NOFX, install:

- Docker 24+
- Docker Compose v2
- Minimum 4GB RAM
- Linux / Windows / macOS supported

Recommended environment:

- Ubuntu 22.04
- 2 CPU cores / 4GB RAM

---

## ⚙️ 3. Configuration

Open the project directory:

cd nofx-dev/


Edit your configuration file:

config/config.json


Insert your exchange & AI API keys:

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
| Field      | Description                                   |
| ---------- | --------------------------------------------- |
| exchange   | Trading exchange: binance / okx / bybit       |
| apiKey     | API key from your exchange                    |
| secretKey  | Secret key from your exchange                 |
| symbol     | Trading pair (example: BTCUSDT)               |
| aiProvider | AI model provider: openai / claude / deepseek |
| aiApiKey   | API key for the AI model                      |
⚠ Important:
Use demo / sandbox API keys for safety.
🚀 4. Start NOFX

Run the system using Docker:
docker compose up -d --build
| Service         | Description                     |
| --------------- | ------------------------------- |
| nofx-backend    | Main backend and trading engine |
| nofx-db         | Database for logs and positions |
| nofx-web (opt.) | Web gateway / API layer         |

Check logs:

docker logs -f nofx-backend

Expected successful output:

NOFX system started successfully
AI engine online
Exchange connection OK

🔥 5. How NOFX Works

NOFX automatically executes:

✔ 1. Market Analysis

Fetches candles, volatility, volume, market structure, trends, etc.

✔ 2. AI Trading Decisions

Example instructions:

BUY(BTCUSDT, 0.01)
STOPLOSS(61800)
TAKEPROFIT(63100)

✔ 3. Automated Order Execution

Orders are sent to your exchange in real time.

✔ 4. Risk Management

Stop loss

Take profit

Trailing stop

Position validation

✔ 5. Logging & Data Storage

Stored inside the database for future analytics.

📊 6. Monitoring Live Trades

Use:
docker logs -f nofx-backend
Example log output:
[AI] Market trend: bullish
[Trade] Executing LONG order 0.01 BTCUSDT
[Risk] Applied stop loss at 61800
[System] Position opened successfully

🛠 7. Folder Structure
api/            → Backend API services  
auth/           → Authentication & token management  
trader/         → Trading engine  
market/         → Market data collector  
config/         → Configuration files  
docker/         → Docker environment  
scripts/        → Helper scripts  
prompts/        → AI prompt templates  
logs/           → System logs (generated)  

❓ 8. FAQ
Q1: AI model fails or returns errors?

Check aiApiKey and provider name.

Q2: Orders are not executed?

Possible reasons:

Wrong API permissions

Exchange requires IP whitelisting

Insufficient balance

Trading pair not enabled for futures

Q3: Docker crashes or fails to start?

Restart with:
docker compose down
docker compose up -d

🌟 9. Future Updates

Planned improvements:

Web dashboard UI

Grid trading (spot/futures)

Smart strategy optimizer

Multi-account mode

Deeper AI integration

More supported exchanges

🤝 10. Contribution

Pull Requests and Issues are welcome.
You may modify or extend NOFX based on your own trading needs.
📬 
