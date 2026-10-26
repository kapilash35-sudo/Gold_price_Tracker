# LankaGold Analytics 🪙
### Sri Lanka Gold Price Intelligence, 100-Day Historical Analysis & Real-Time Live Tracker

[![Deploy with Vercel](https://vercel.com/button)](https://vercel.com/new)
[![License: MIT](https://img.shields.io/badge/License-MIT-amber.svg)](LICENSE)
[![Platform](https://img.shields.io/badge/Platform-Vercel%20%7C%20Localhost-black.svg)](#deployment--hosting)
[![Source](https://img.shields.io/badge/Official%20Source-CMBGOLD%20(cmbgold.lk)-orange.svg)](https://cmbgold.lk)

**LankaGold Analytics** is an ultra-premium, real-time gold market tracking and quantitative intelligence web application designed specifically for the Sri Lankan gold and jewellery market (Colombo Sea Street & CMB Gold benchmark).

It tracks **24 Karat pure gold**, **22 Karat jewellery gold**, and **1 Sovereign (8g Pawn)** rates with automated live scraping from [cmbgold.lk](https://cmbgold.lk/), provides an interactive **100-Day historical chart with moving averages (SMA 7 & 30)**, dynamic day-by-day continuous history logging, and a **14-day predictive trend forecast**.

---

## 🌟 Key Features

### 1. ⚡ Live CMB Gold Scraping & Real-Time Sync
- **Live Spot Ticker**: Scrapes current 24K per-gram, 22K per-gram, and 24K Sovereign selling and buying prices directly from [cmbgold.lk](https://cmbgold.lk/).
- **45-Second Auto-Polling**: Continuously syncs live prices in the background with a visual countdown timer (`Live: 45s`).
- **One-Click Manual Refresh**: Interactive sync button with micro-animations to instantly refresh live rates on demand.
- **Fail-Safe Multi-Tier Fallback**: Ensures the application and chart never crash if the scraper encounters a temporary network timeout or Cloudflare challenge.

### 2. 📅 Dynamic Date Progression & Persistent Daily History
- **Never Stuck in the Past**: Dynamically adapts to the current calendar date (`new Date()`). The historical timeline automatically advances every single day without manual code updates.
- **Continuous Daily Tracking on Vercel**: Saves daily closing prices to `localStorage` (`lankagold_daily_history`). Each day you visit the application, today's price is recorded into the permanent timeline.
- **Local JSON Backup**: When running locally via Python, prices are also appended to [gold_history.json](file:///home/kapi/Documents/gold_project/gold_history.json).

### 3. 📈 Interactive 100-Day Chart & Trend Analysis
- **Chart.js Powered Line Visualizer**: Smooth gold-gradient area chart with responsive hover tooltips and dynamic indicators.
- **Moving Average Overlays**:
  - **SMA 7**: 7-day Simple Moving Average for short-term momentum.
  - **SMA 30**: 30-day Simple Moving Average for macro baseline trend and support levels.
- **Multi-Karat & Timeframe Switchers**:
  - Karats: 24K Pure Gold, 22K Jewellery Gold, 1 Sovereign (8g Pawn).
  - Timeframes: 7 Days, 30 Days, 100 Days, and +14-Day Forecast.
- **Key Statistics Dashboard**: Automatically calculates 100-Day All-Time High, 100-Day Low, Period Average, and Net Return Percentage.

### 4. 🔮 14-Day Forward Quantitative Forecast
- Mathematical support-bounce predictive model that projects expected price movements over the next 14 days based on recent market pullbacks, consolidation ranges, and technical momentum.
- Indicated clearly on the chart as a distinct cyan dashed projection line.

### 5. 🎚️ 100-Day Timeline Date Scrubber
- An interactive horizontal slider allowing users to inspect the exact gold price, midnight close, today vs past difference, and ROI percentage for any of the past 100 days.

### 6. 🧮 Smart Jewellery & Bullion Calculator
- Real-time conversion across units:
  - **Grams (g)**
  - **Pawns / Sovereigns (1 Sovereign = 8.00 grams)**
  - **Tolas (1 Tola = 11.6638 grams)**
- Karat selection: 24K, 22K, 21K, 18K.
- Toggleable making & wastage charges (standard 6%).
- Live dual currency calculation: **LKR** and approximate **USD** value.

### 7. 🎨 Ultra-Premium Luxury Dark UI
- Designed with obsidian black (`#07090E`), deep navy glass cards, ambient radial gold glows, and typography powered by **Outfit** and **Plus Jakarta Sans**.

---

## 🏗️ Architecture & Project Structure

```bash
gold_project/
├── api/
│   └── cmb-live.js         # Vercel Serverless Function (Node.js edge scraper)
├── app.js                  # Core Frontend Engine & State Management
├── index.html              # Modern Semantic HTML5 Application Structure
├── index.css               # Luxury Dark Gold CSS Design System
├── server.py               # Local Python Development Server & JSON Logger
├── gold_history.json       # Local Persistent Storage for Daily Price Logging
├── vercel.json             # Vercel Deployment & Route Rewrites Configuration
└── README.md               # Complete Project Documentation
```

---

## 🚀 Deployment & Hosting

### Option 1: Deploy on Vercel (Recommended)

This project is zero-config and production-ready for **Vercel** serverless hosting.

#### Via GitHub:
1. Initialize a git repository in this folder:
   ```bash
   git init
   git add .
   git commit -m "feat: initial commit for LankaGold Analytics"
   ```
2. Create a new repository on [GitHub](https://github.com) and push the code:
   ```bash
   git remote add origin https://github.com/<your-username>/<your-repo-name>.git
   git branch -M main
   git push -u origin main
   ```
3. Log in to [vercel.com](https://vercel.com), click **"Add New Project"**, select your GitHub repository, and click **"Deploy"**.
4. Vercel will automatically configure the static assets and the serverless endpoint at `https://<your-project>.vercel.app/api/cmb-live`.

#### Via Vercel CLI:
Install Vercel CLI and run deploy directly from your terminal:
```bash
npx vercel
```
Follow the interactive prompts (select default settings by pressing Enter).

---

### Option 2: Run Locally (Python Server)

To run the application locally on your computer:

```bash
# Start local server
python3 server.py
```

Open your browser and navigate to:
```
http://localhost:3000
```

- Web UI: `http://localhost:3000/`
- Live CMB Gold API: `http://localhost:3000/api/cmb-live`
- Local History API: `http://localhost:3000/api/history`

---

## 📡 API Reference

### `GET /api/cmb-live`
Scrapes the live 24KT and Sovereign rates from [cmbgold.lk](https://cmbgold.lk/).

#### Success Response (`200 OK`):
```json
{
  "source": "CMBGOLD (cmbgold.lk)",
  "status": "success",
  "price_gram_24k": 44000.00,
  "price_gram_22k": 40333.33,
  "price_pawn_24k_sell": 352000.00,
  "price_pawn_24k_buy": 359040.00,
  "price_gram_24k_buy": 44880.00,
  "timestamp": "2026-10-26T12:29:22.000Z",
  "updated_at": "26 Oct 2026 • Live CMB Gold Feed"
}
```

#### Fallback Response (`200 OK`):
If external connection fails or times out, the server gracefully returns calibrated Colombo market benchmarks without throwing a 500 error:
```json
{
  "source": "CMBGOLD (cmbgold.lk - Cached Benchmark)",
  "status": "fallback",
  "error": "Scrape restriction or timeout",
  "price_gram_24k": 44000.00,
  "price_gram_22k": 40333.33,
  "price_pawn_24k_sell": 352000.00,
  "price_pawn_24k_buy": 359040.00,
  "price_gram_24k_buy": 44880.00,
  "timestamp": "2026-10-26T12:29:22.000Z",
  "updated_at": "Today • CMB Gold Official Benchmark"
}
```

---

## 💡 How Continuous Daily Tracking Works

Because Vercel runs on a serverless, stateless architecture, traditional servers that write to local disk cannot keep state across cold restarts. **LankaGold Analytics** solves this with a two-tiered system:

1. **Client-Side Persistence (`localStorage`)**:
   - The key `lankagold_daily_history` stores verified closing rates by date (`YYYY-MM-DD`).
   - Every day you visit your deployed site on Vercel, the app checks if today's date exists. If not, it logs today's live rate.
   - When the chart generates, it seamlessly pulls all logged days up to the current day.
2. **Dynamic Day Generation**:
   - The timeline calculates backwards 99 days from `new Date()` (Today), and projects 14 days forward.
   - Verified anchor dates (such as the Oct 21 all-time peak of 45,232 LKR, Oct 24 pullback to 44,375 LKR, and Oct 26 consolidation at 44,000 LKR) are permanently pinned in historical series.

---

## 📐 Formulas & Market Standards

| Standard | Calculation / Purity | Sri Lanka Market Application |
| :--- | :--- | :--- |
| **24 Karat** | $1.00 \times \text{Spot Rate}$ | 99.9% pure bullion gold / biscuit rate |
| **22 Karat** | $\text{Spot Rate} \times \frac{22}{24}$ | 91.6% standard hallmark jewellery gold |
| **1 Sovereign (Pawn)** | $8.00\text{g} \times \text{Rate per Gram}$ | Traditional Sri Lankan jewellery weight |
| **1 Tola** | $11.6638\text{g} \times \text{Rate per Gram}$ | Subcontinental bullion trading unit |
| **Wastage / Making** | $\text{Subtotal} \times 6\%$ | Average goldsmith crafting allowance |

---

## 🛠️ Configuration & API Settings

Click the **"Live Hub"** button in the navbar to open the API settings modal:
- **GoldAPI.io Key (Optional)**: If you possess a free key from [goldapi.io](https://goldapi.io), input it here to sync global London bullion spot rates ($XAU/USD$ and $XAU/LKR$).
- **Currency Exchange Rate**: Automatically fetches live USD/LKR foreign exchange rates via Open Exchange Rates (`https://open.er-api.com/v6/latest/USD`) to compute accurate CBSL rupee parities.

---

## 📄 License
This project is open-source under the [MIT License](LICENSE).
Feel free to customize, host, and integrate for personal or commercial gold tracking.
