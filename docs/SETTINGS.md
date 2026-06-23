# Settings Reference

Complete parameter documentation for Gabremoku Clouds with Reversion Bubbles.

---

## Core

**Source** (`close`)
The price series used for positioning logic (above/below cloud/equilibrium).

**Equilibrium Period** (`26`, range 5–200)
The rolling window in bars for computing the VWAP (equilibrium) and VWAS (spread). Shorter values = more reactive but noisier. Longer values = smoother, better for swing context.

**Cloud Multiplier** (`1.5`, range 0.5–5.0)
How many VWAS units the cloud extends above and below equilibrium. Increase for wider, less frequently tested bands. Decrease for tighter, more active bands.

**Slope Length** (`3`, range 1–20)
Bars back used to determine whether equilibrium is rising or falling. Very small values respond fast but are noisy; larger values confirm trend more reliably.

---

## Volume

**Volume Average Period** (`20`, range 5–200)
SMA period for the volume baseline. Volume is compared to this average to classify intensity.

**High Volume Threshold** (`1.5×`, range 1.0–5.0)
Volume/average ratio above which bars are marked "High Volume". Breakout/acceptance conditions require high volume.

**Low Volume Threshold** (`0.7×`, range 0.1–1.0)
Volume/average ratio below which bars are marked "Low Volume". Affects cloud transparency and general caution.

**Volume Velocity Lookback** (`3`, range 1–20)
Bars back used to compute the change in volume ratio (acceleration/deceleration).

---

## Projection

**Show Projected Equilibrium** (`false`)
Enables a forward-projected line showing where equilibrium may be heading.

**Projection Forward** (`26`, range 1–100)
How many bars ahead the projection is plotted.

**Projection Slope Length** (`5`, range 1–50)
Bars used to measure the raw slope of smoothed equilibrium.

**Projection Smoothing Length** (`13`, range 2–100)
EMA period applied to equilibrium before slope calculation. Higher = smoother projection.

**Projection Slope Smoothing** (`5`, range 1–50)
EMA period applied to the per-bar slope before projection. Reduces whipsaw.

**Projection Damping** (`0.55`, range 0.10–1.00)
Scales the projected distance. `1.0` = full slope extrapolation; `0.1` = barely deviates from current equilibrium. Tune this to taste.

---

## Adaptive Kumo

**Show Adaptive Kumo** (`false`)
Enables the forward-shifted volume-weighted cloud.

**Kumo Shift Forward** (`13`, range 1–100)
Bars the Kumo is projected into the future (like standard Ichimoku displacement).

**Span A Short Period** (`9`, range 3–50)
Short VWEP window feeding into Span A average.

**Span A Long Period** (`26`, range 10–100)
Long VWEP window feeding into Span A average.

**Span B Wide Period** (`52`, range 20–200)
Look-back for the highest/lowest typical price midpoint (Span B).

**Kumo Line Transparency** (`45`, range 0–100)
Transparency of the Span A and Span B border lines.

**Kumo Near Transparency** (`88`, range 0–100)
Base transparency for the inner (near) half of the Kumo fill. Dynamically adjusted by Kumo thickness.

**Kumo Far Transparency** (`96`, range 0–100)
Base transparency for the outer (far) half of the Kumo fill.

---

## Signals

**Show LONG / SHORT Signals** (`true`)
Toggles the `▲ L` / `▼ S` label shapes on the chart.

**Include Exhaustion Reversals** (`true`)
Enables exhaustion-based reversal logic (new extreme + far from cloud + volume decelerating).

**Include Squeeze Breakouts** (`true`)
Enables signals that fire when squeeze compression releases.

**Min Confluence to Fire (1–3)** (`2`)
Minimum number of agreeing factors (state + Kumo direction + projection direction) required before a signal fires.

---

## Bubble Bands

**Show Bubble Signals** (`true`)
Enables the bubble band engine and circle markers.

**Keep Historical Bubbles** (`true`)
When enabled, bubble markers are stored and persist on the chart (uses `label` array). When disabled, only the most recent bar's signal shows.

**Bubble Trigger Mode** (`Reentry`)
- `Touch` — fires the moment price reaches the outer band
- `Reentry` — fires when price closes back inside the band after piercing it (fewer, higher-quality signals)

**Bubble Band Multiplier** (`2.0×`, range 0.5–5.0)
VWAS multiple defining the outer bubble bands. Should be larger than the Cloud Multiplier.

**Flat Slope Threshold** (`2.5`, range 0.5–10.0)
Maximum slope (measured as absolute equilibrium change relative to VWAS) allowed for bubble signals. Keeps signals in ranging/compressing conditions.

**Bubble Cooldown Bars** (`5`, range 0–100)
Minimum bars between consecutive signals of the same direction. Prevents re-firing immediately after a signal.

**Use Kumo Direction Filter** (`true`)
Only fires long bubble signals when Kumo is bullish, and short bubble signals when Kumo is bearish. Aligns bubble signals with structural bias.

**Only in Contraction Regime** (`true`)
Restricts bubble signals to periods where equilibrium slope is below the flat slope threshold. Bubbles are mean-reversion tools; this prevents firing during trending legs.

---

## Colors

All colors are fully customisable via standard TradingView color pickers.

| Setting | Default | Purpose |
|---|---|---|
| Bull Color | Blue `rgb(47,102,255)` | Bullish states, signals, fills |
| Bear Color | Yellow `rgb(241,222,52)` | Bearish states, signals, fills |
| Neutral Color | Grey `rgb(120,120,130)` | Neutral/flat conditions |
| Squeeze Color | Purple `rgb(170,0,255)` | Squeeze state highlighting |
| Long Bubble Marker | Green `rgb(0,200,140)` | Bubble long signal circles |
| Short Bubble Marker | Red `rgb(255,82,82)` | Bubble short signal circles |
| Bubble Lower Line | Dark green `rgb(0,120,90)` | Lower bubble band line |
| Bubble Upper Line | Dark red `rgb(120,35,35)` | Upper bubble band line |

---

## Style

**Show VWEB Cloud** (`true`)
Toggle the main cloud fills and borders.

**Show VWEB Midline** (`true`)
Toggle the equilibrium midline.

**Color Bars** (`false`)
Recolors price bars according to market state.

**Midline Width** (`2`, range 1–5)
Pixel width of the equilibrium line.

**Cloud Border Width** (`1`, range 1–5)
Pixel width of the cloud upper/lower border lines.

---

## Squeeze

**Squeeze Lookback** (`50`, range 10–500)
How many bars back VWAS is normalised over for squeeze detection.

**Squeeze Threshold** (`0.15`, range 0.01–0.50)
Normalised VWAS value at or below which a squeeze is active. 0.15 means VWAS is in the bottom 15% of its recent range.

**Highlight Squeeze Background** (`false`)
Paints a faint purple background behind all candles when a squeeze is active.

---

## Exhaustion

**Exhaustion Lookback** (`20`, range 5–100)
Period for identifying new highs/lows. A bar at a 20-bar extreme can trigger exhaustion logic.

**Min Distance From Cloud** (`0.25×`, range 0.05–2.0)
Minimum distance of price from the cloud edge, expressed as a multiple of VWAS, required for exhaustion signals.

**Min Volume Deceleration** (`0.20`, range 0.05–2.0)
Minimum drop in volume velocity (volRatio change over the lookback period) required to confirm deceleration.

---

## Dashboard

**Show Dashboard** (`true`)
Enables the status table.

**Dashboard Position** (`Bottom Right`)
Corner of the chart where the table appears: Top Right / Top Left / Bottom Right / Bottom Left.

**Dashboard Text Size** (`Small`)
Font size of dashboard text: Tiny / Small / Normal.

---

## End Labels

**Show End Labels** (`true`)
Renders text labels at the rightmost bar for Kumo lines and Projected Equilibrium (when those features are enabled).

**Label Offset Bars** (`2`, range 1–20)
How many bars to the right of the last bar the labels are placed.
