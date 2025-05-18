# Real-time Bitcoin Price Analytics with Qlik Sense

## Table of Contents

* [Project Overview](#project-overview)
* [Workflow & Architecture](#workflow--architecture)
* [Key Features](#key-features)
* [Implementation Details](#implementation-details)
* [Qlik Dashboard & Visualizations](#qlik-dashboard--visualizations)
* [Technical Stack](#technical-stack)
* [Challenges & Workarounds](#challenges--workarounds)
* [Future Improvements](#future-improvements)
* [Project Structure](#project-structure)
* [Installation Guide](#installation-guide)
* [Acknowledgments](#acknowledgments)

---

## Project Overview

This project delivers a **real-time Bitcoin price analytics and forecasting solution** by combining Python-based data ingestion, GitHub for data sync, and Qlik Sense for interactive visualization and analytics.
The goal: **Create a semi-automated pipeline that fetches, processes, and visualizes Bitcoin price data in near real time—even within the constraints of a student/free-tier Qlik Sense account.**

---

## Workflow & Architecture

### Enhanced Workflow Diagram

```mermaid
graph TD
    A[Python Script: datafetch.py fetches Bitcoin price via CoinGecko API every 10 seconds] --> B[Calculate moving averages (ma_6) and volatility (volatility_12) using Analysis.py]
    B --> C[Write outputs to CSV files: bitcoin_realtime.csv and bitcoin_analytics.csv]
    C --> D[Git automation via gitpush.py pushes updated CSVs to GitHub repository]
    D --> E[Qlik Cloud REST Connector fetches latest CSV from GitHub raw URL on demand]
    E --> F[Data Load Editor parses fields and uses now() to append current timestamp]
    F --> G[Qlik Dashboard visualizes data: Line charts, KPIs, filters, moving average, volatility tracking]
    G --> H[User explores real-time trends, summary KPIs, and live filtering within Qlik dashboard]
```

### Summary Steps

1. **datafetch.py** pulls data from CoinGecko.
2. **bitcoin\_realtime.csv** is updated with price and current timestamp.
3. **Analysis.py** calculates moving average and volatility, storing in `bitcoin_analytics.csv`.
4. **gitpush.py** syncs updated CSVs to GitHub.
5. **Qlik REST connector** points to GitHub raw URL.
6. Data is loaded into **Qlik Dashboard** with computed metrics and user interactivity.

---

## Key Features

* **Automated Bitcoin Price Data Collection** via Python & CoinGecko API
* **Data Analytics**:

  * Moving averages, rolling max/min, and volatility metrics
  * CSV-based pipeline for compatibility and GitHub versioning
* **GitHub Data Sync**:

  * Live data pushed to GitHub every few seconds via script
* **Interactive Qlik Sense Dashboard**:

  * Live charts with filters
  * KPIs for min, max, average, and current prices

---

## Implementation Details

### 1. **Python Data Fetcher (datafetch.py)**

* Hits CoinGecko API every 10 seconds
* Appends timestamped price data to `bitcoin_realtime.csv`

### 2. **Analytics Processor (Analysis.py)**

* Computes:

  * `ma_6` (6-point moving average)
  * `volatility_12` (12-point standard deviation window)
* Outputs to `bitcoin_analytics.csv`

### 3. **GitHub Automation (gitpush.py)**

* Adds, commits, and pushes all updated CSV files
* Keeps GitHub repo in sync with local updates

### 4. **Qlik Integration**

* REST connector links to public GitHub raw CSV
* Timestamp added via `now()` in Qlik Load Editor
* Final table displayed in Qlik dashboard with filters

---

## Qlik Dashboard & Visualizations

### **Live Analytics Dashboard Example**

*Live feed of Bitcoin price with analytical overlays: moving average and max tracker. KPIs below reflect volatility and extremes.*

---

## Technical Stack

* **Python 3.x**: Automation + analytics
* **CoinGecko API**: Real-time Bitcoin price
* **Pandas**: Time-series processing
* **Git & GitHub**: Versioned data sync
* **Qlik Cloud**: Data visualization + dashboard

---

## Challenges & Workarounds

### Limitations in Qlik Academic Cloud

* No built-in **data automation or reload scheduling**
* Google Drive and Sheets connectors blocked due to license tier
* Rate limiting errors from over-polling REST endpoints

### Workarounds

* Moved all automation **outside Qlik**

  * Python handles fetching + pushing
  * Qlik just reads from a static GitHub URL

---

## Future Improvements

* Add **Qlik Application Automation** if available
* Use **Docker container** to schedule tasks more robustly
* Implement **real-time webhooks** from GitHub or cloud pipeline

---

## Project Structure

```
.
├── Images/                            # Screenshots & error samples
│   ├── qlik_dashboard.png
│   ├── qlik_automation_error.png
│   └── qlik_gdrive_error.png
├── Analysis.py                       # Analytics and rolling calculations
├── bitcoin_analytics.csv             # Includes ma_6 and volatility_12
├── bitcoin_forecast.csv              # Placeholder for predictive analysis
├── bitcoin_realtime.csv              # Raw Bitcoin price log
├── datafetch.py                      # Real-time data collection from API
├── docker_bash.sh                    # Shell script for Docker bash entry
├── docker_build.sh                   # Shell script to build Docker image
├── Dockerfile                        # Build Docker container
├── gitpush.py                        # GitHub automation logic
├── QlikAnalysis_utils.py             # Shared utility functions
├── QlikAnalysis.API.json             # Qlik export
├── QlikAnalysis.export.json          # Exported configuration
├── QlikAnalysis.excel.xlsx           # Optional export format
├── Readme.md                         # Primary documentation
├── real.md                           # Backup notes
├── requirements.txt                  # Python dependencies
```

---

## Installation Guide

### **Prerequisites**

* Python 3.x
* GitHub account
* Qlik Sense Cloud login

### **Quick Setup**

```bash
git clone https://github.com/YOUR_USERNAME/bitcoin-qlik.git
cd bitcoin-qlik
pip install -r requirements.txt
python datafetch.py
python gitpush.py
```

Set Qlik REST Connector to:

```
https://raw.githubusercontent.com/YOUR_USERNAME/bitcoin-qlik/main/bitcoin_realtime.csv
```

---

## Acknowledgments

* **CoinGecko** – for open crypto pricing APIs
* **Qlik** – Academic Cloud tier access
* **GitHub** – Free open dataset hosting
* **VS Code + Docker** – Dev tooling support
