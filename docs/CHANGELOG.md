# Changelog

All notable changes to Gabremoku Clouds will be documented here.

---

## [1.0.0] — Initial Release

### Added
- VWEB (Volume-Weighted Equilibrium Band) cloud with gradient fills
- VWAS-based dynamic spread calculation
- Six market states: Accepted Above, Accepted Below, Bull Bias, Bear Bias, Squeeze, Neutral
- Volume regime classification (High / Normal / Low) with velocity tracking
- Squeeze detection via normalised VWAS percentile
- Bubble Band engine with Touch and Reentry trigger modes
- Cooldown system to prevent signal clustering
- Kumo direction filter and contraction regime filter for bubbles
- Adaptive Kumo (volume-weighted Ichimoku) with forward projection and gradient fill
- Projected Equilibrium with EMA smoothing, slope smoothing, and damping
- Confluence scoring (1–3 stars) across state, Kumo, and projection
- LONG / SHORT directional signal labels
- Exhaustion reversal detection (new extreme + distance + volume decel)
- Squeeze breakout signal support
- Real-time dashboard with 12 rows of state information
- End labels for Kumo lines and projected equilibrium
- Bar coloring mode
- Squeeze background highlight
- Fully customisable color palette for all elements
- Projection color palette independent from main palette
