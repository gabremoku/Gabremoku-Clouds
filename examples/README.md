# Usage Examples & Tips

Practical guidance for getting the most out of Gabremoku Clouds.

---

## Recommended Starting Configurations

### Swing Trading (Daily / 4H)

Focus on structural context. The Kumo and Projection are especially useful at higher timeframes.

```
Equilibrium Period:    26
Cloud Multiplier:     1.5
Bubble Band Mult:     2.0
Bubble Trigger Mode:  Reentry
Min Confluence:       2
Show Adaptive Kumo:   true
Kumo Shift Forward:   13
Show Projection:      true
Projection Forward:   26
Projection Damping:   0.55
```

### Intraday Scalping (15m / 5m)

Tighten the period, lower the cooldown, and keep signals simple.

```
Equilibrium Period:    13
Cloud Multiplier:     1.2
Bubble Band Mult:     1.8
Bubble Trigger Mode:  Touch
Bubble Cooldown:      3
Min Confluence:       1
Show Adaptive Kumo:   false
Show Projection:      false
```

### Mean Reversion Focus

Maximise bubble signal quality by tightening filters.

```
Bubble Trigger Mode:    Reentry
Only in Contraction:    true
Use Kumo Filter:        true
Min Confluence:         2
Flat Slope Threshold:   2.0
Bubble Cooldown:        7
```

---

## Reading the Dashboard

The dashboard is the fastest way to assess current conditions at a glance.

**Example — High-confidence long setup:**
```
State:        Bull Bias
Kumo:         Bullish
Projection:   Upward
Confluence:   ★★★ Full
Slope:        Rising
Vol Intensity: High
Regime:       Contraction
```
All three confluence inputs agree, volume is elevated, and the regime supports bubble signals. A Bubble Lower Line touch in this context would be a strong long candidate.

**Example — Squeeze about to break:**
```
State:       Squeeze
Kumo:        Bullish
Projection:  Upward
Confluence:  ★★★ Full
Slope:       Flat
Vol Intensity: Low
```
Low volume squeeze with bullish structural alignment. Watch for the squeeze to release with a volume spike upward.

---

## Tips

**Layering timeframes**
Load the indicator on a higher timeframe (e.g. Daily) and note the State and Kumo direction. Then switch to your trading timeframe (e.g. 1H) and only take signals aligned with the higher timeframe bias.

**Bubble signals in trending markets**
Disable "Only in Contraction Regime" if you want to catch pullback entries during trends. The Kumo filter still helps avoid counter-trend trades.

**Projection as a target**
When price is inside the cloud and the Projection is bullish, the projected equilibrium level can act as a soft magnet / target for the next move.

**Squeeze + Kumo alignment**
When a squeeze forms and the Kumo is already shifted into a bullish or bearish position ahead, the eventual breakout is more likely to follow that direction.

**Adjusting cloud width**
If price is frequently outside the cloud on your timeframe/instrument, increase the Cloud Multiplier. If price never touches the edges, decrease it. The goal is for the cloud to act as meaningful support/resistance.

**Dashboard position**
Move the dashboard to whichever corner does not overlap with your price action at typical zoom levels. Use "Tiny" text size for dense charts.

---

## Common Pitfalls

- **Too many signals** — lower the Bubble Band Multiplier, increase the cooldown, or enable "Only in Contraction Regime".
- **Signals in the wrong direction** — ensure "Use Kumo Filter" is enabled and the Kumo is visible to verify its direction before trading.
- **Cloud too narrow or too wide** — tune the Cloud Multiplier and Equilibrium Period together; the period affects how reactive VWAS is to recent volatility.
- **Projection whipsawing** — increase Projection Slope Smoothing or Projection Smoothing Length, or reduce Projection Damping.
