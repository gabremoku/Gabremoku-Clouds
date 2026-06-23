# Gabremoku Clouds with Reversion Bubbles

> A volume-weighted equilibrium cloud system with adaptive Kumo, projected equilibrium, squeeze detection, and mean-reversion bubble signals — all in one overlay indicator for TradingView.

[![TradingView](https://img.shields.io/badge/TradingView-Published-blue?logo=tradingview)](https://www.tradingview.com/script/XTAVGPWK-Gabremoku-Clouds/)
[![Pine Script](https://img.shields.io/badge/Pine%20Script-v6-4CAF50)](https://www.tradingview.com/pine-script-docs/en/v6/Introduction.html)
[![License: MPL 2.0](https://img.shields.io/badge/License-MPL%202.0-brightgreen.svg)](https://opensource.org/licenses/MPL-2.0)

---

## Overview

**Gabremoku Clouds** is a comprehensive market-state indicator built on volume-weighted price mechanics. Rather than treating all price action equally, every calculation is anchored to actual traded volume, giving you a more accurate picture of where the market truly agrees on value.

The indicator blends several complementary layers:

| Layer | What it shows |
|---|---|
| **VWEB Cloud** | Volume-Weighted Equilibrium Band — the core cloud showing fair value and its spread |
| **Bubble Bands** | Extended bands for mean-reversion setups at statistical extremes |
| **Adaptive Kumo** | A volume-adjusted Ichimoku cloud projected forward for trend context |
| **Projected Equilibrium** | EMA-smoothed slope projection of where equilibrium is heading |
| **Squeeze Detection** | Identifies low-volatility compression before explosive moves |
| **Dashboard** | Real-time panel summarising all active states at a glance |

---

## How It Works

### Core Concept: VWEB (Volume-Weighted Equilibrium Band)

The equilibrium line is a **Volume-Weighted Average Price (VWAP)** calculated over a rolling window, not a session. The cloud width uses **VWAS** (Volume-Weighted Average Spread), which measures typical bar range weighted by volume — a natural, market-driven measure of volatility.

```
Equilibrium = Σ(Volume × Typical Price) / Σ(Volume)
VWAS        = Σ(Volume × (High − Low))  / Σ(Volume)
Cloud Upper = Equilibrium + Multiplier × VWAS
Cloud Lower = Equilibrium − Multiplier × VWAS
```

### Market States

The indicator classifies price action into six states:

- **Accepted Above** — price broke above the cloud with high volume (bullish)
- **Accepted Below** — price broke below the cloud with high volume (bearish)
- **Bull Bias** — price above equilibrium with rising slope
- **Bear Bias** — price below equilibrium with falling slope
- **Squeeze** — VWAS at a multi-bar minimum, compression imminent
- **Neutral** — no strong directional conviction

### Bubble Bands & Reversion Signals

Bubble bands extend beyond the main cloud using a separate VWAS multiplier. When price reaches these outer bands in a low-slope (contraction) regime, reversion signals fire:

- **Touch mode** — signals when price reaches the band
- **Reentry mode** — signals when price re-enters the band after piercing it (higher confidence)

A **cooldown** parameter prevents signal clustering.

### Adaptive Kumo

A standard Ichimoku Kumo re-engineered with volume weighting. Span A is derived from short and long VWEP (Volume-Weighted Equilibrium Price) averages. Span B uses the classic midpoint of the highest high / lowest low. The cloud is shifted forward, providing a structural support/resistance outlook.

### Projected Equilibrium

The indicator projects where equilibrium is likely to be N bars ahead by:
1. Smoothing equilibrium with an EMA
2. Computing the slope per bar
3. Smoothing the slope
4. Extrapolating forward with a damping factor

---

## Installation

1. Open [TradingView](https://www.tradingview.com) and navigate to any chart.
2. Click **Indicators** (the beaker icon in the top toolbar).
3. Search for **"Gabremoku Clouds"** in the Public Library.
4. Click to add it to your chart.

Alternatively, use the direct link:

**[Open Gabremoku Clouds on TradingView](https://www.tradingview.com/script/XTAVGPWK-Gabremoku-Clouds/)**

---

## Settings Reference

### Core
| Parameter | Default | Description |
|---|---|---|
| Source | Close | Price source for positioning logic |
| Equilibrium Period | 26 | Rolling window for VWAP/VWAS calculation |
| Cloud Multiplier | 1.5 | How wide the cloud extends from equilibrium |
| Slope Length | 3 | Bars used to determine equilibrium direction |

### Volume
| Parameter | Default | Description |
|---|---|---|
| Volume Average Period | 20 | SMA period for the volume baseline |
| High Volume Threshold | 1.5× | Volume/avg ratio to classify as "high volume" |
| Low Volume Threshold | 0.7× | Volume/avg ratio to classify as "low volume" |
| Volume Velocity Lookback | 3 | Bars to measure volume acceleration/deceleration |

### Bubble Bands
| Parameter | Default | Description |
|---|---|---|
| Bubble Trigger Mode | Reentry | "Touch" fires on contact; "Reentry" fires on close back inside |
| Bubble Band Multiplier | 2.0× | VWAS multiple defining the outer bands |
| Flat Slope Threshold | 2.5 | Max slope (relative to VWAS) to allow bubble signals |
| Bubble Cooldown Bars | 5 | Minimum bars between consecutive signals |
| Use Kumo Direction Filter | true | Only long bubbles when Kumo is bullish, and vice versa |
| Only in Contraction Regime | true | Restrict bubbles to low-slope environments |

### Adaptive Kumo
| Parameter | Default | Description |
|---|---|---|
| Kumo Shift Forward | 13 | Bars to project the Kumo into the future |
| Span A Short Period | 9 | VWEP short-term window |
| Span A Long Period | 26 | VWEP long-term window |
| Span B Wide Period | 52 | Classic high/low midpoint window |

### Projection
| Parameter | Default | Description |
|---|---|---|
| Projection Forward | 26 | Bars ahead to project equilibrium |
| Projection Damping | 0.55 | Reduces projection aggressiveness (0 = flat, 1 = full slope) |

### Signals
| Parameter | Default | Description |
|---|---|---|
| Show LONG / SHORT | true | Toggle the main directional signal labels |
| Min Confluence | 2 | Minimum confluence score (1–3) required to fire signals |

---

## Visual Guide

```
  ┌──────────────── Bubble Upper Line ─────────────────┐
  │                                                      │
  │   ┌──────────── Cloud Upper ────────────────┐       │
  │   │                                          │       │
  │   │         (Accepted Above zone)            │       │
  │   │                                          │       │
  │   ├──────────── Equilibrium ────────────────┤       │
  │   │                                          │       │
  │   │         (Accepted Below zone)            │       │
  │   │                                          │       │
  │   └──────────── Cloud Lower ────────────────┘       │
  │                                                      │
  └──────────────── Bubble Lower Line ─────────────────┘
```

**Colors (defaults):**
- Blue — bullish states
- Yellow — bearish states
- Purple — squeeze / compression
- Grey — neutral
- Green circles — long bubble signals
- Red circles — short bubble signals

---

## Dashboard

When enabled, a real-time panel displays:

| Row | Description |
|---|---|
| State | Current market state |
| Kumo | Adaptive Kumo direction |
| Projection | Projected equilibrium direction |
| Confluence | Score of agreeing signals (1–3 stars) |
| Slope | Equilibrium slope direction |
| Vol Intensity | High / Normal / Low |
| Vol Velocity | Accel / Flat / Decel |
| VWAS | Current spread value |
| Last Signal | Most recent LONG or SHORT |
| Trigger | Signal source description |
| Bubble | Current bubble signal state |
| Regime | Contraction or Expansion |

---

## File Structure

```
Gabremoku-Clouds/
├── README.md                    # This file
├── LICENSE                      # Mozilla Public License 2.0
├── .gitignore
├── indicator/
│   └── gabremoku_clouds.pine    # Full Pine Script v6 source
├── docs/
│   ├── SETTINGS.md              # Detailed parameter documentation
│   └── CHANGELOG.md             # Version history
└── examples/
    └── README.md                # Usage examples and tips
```

---

## About the Author

**Gabremoku** is an independent trader and Pine Script developer focused on volume-based market analysis.

| Platform | Link |
|---|---|
| TradingView Profile | [tradingview.com/u/Gabremoku](https://www.tradingview.com/u/Gabremoku/#published-scripts) |
| All Links | [linktr.ee/gabremoku](https://linktr.ee/gabremoku) |

Follow on TradingView to get notified of new indicators and updates.

---

## License

This indicator is published under the **[Mozilla Public License 2.0](LICENSE)**.

You are free to use, modify, and distribute this code under the terms of the MPL 2.0. Attribution to the original author (Gabremoku) is required when redistributing.

---

## Contributing

Feedback, bug reports, and suggestions are welcome via GitHub Issues.

If you want to contribute improvements:
1. Fork the repository
2. Create a feature branch (`git checkout -b feature/my-improvement`)
3. Commit your changes
4. Open a Pull Request with a clear description

Please keep contributions focused on bug fixes or well-reasoned logic improvements. Visual/cosmetic PRs are unlikely to be merged.

---

## Disclaimer

This indicator is provided for educational and informational purposes only. It is not financial advice. Trading involves significant risk of loss. Always do your own research and use proper risk management.
