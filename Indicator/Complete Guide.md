# 📊 Multi-Indicator Confluence System - Complete Guide
## Comprehensive Report of All Indicators Used in V1 & V4

---

# Table of Contents

1. [Overview](#overview)
2. [VWAP - Volume Weighted Average Price](#1-vwap---volume-weighted-average-price)
3. [CPR - Central Pivot Range](#2-cpr---central-pivot-range)
4. [EMA - Exponential Moving Average](#3-ema---exponential-moving-average)
5. [Supertrend](#4-supertrend)
6. [RSI - Relative Strength Index](#5-rsi---relative-strength-index)
7. [MACD - Moving Average Convergence Divergence](#6-macd---moving-average-convergence-divergence)
8. [Stochastic Oscillator](#7-stochastic-oscillator)
9. [ADX - Average Directional Index](#8-adx---average-directional-index)
10. [Volume Analysis](#9-volume-analysis)
11. [Bollinger Bands](#10-bollinger-bands)
12. [Parabolic SAR](#11-parabolic-sar)
13. [ATR - Average True Range](#12-atr---average-true-range)
14. [Signal Types Explained](#signal-types-explained)
15. [Confluence Scoring System](#confluence-scoring-system)
16. [Quick Reference Cheat Sheet](#quick-reference-cheat-sheet)

---

# Overview

This indicator system combines **12+ technical indicators** to generate high-probability trading signals for Nifty 50 and Sensex options trading. The system calculates a **confluence score** based on how many indicators agree on the direction.

## Signal Types in V4

| Signal Type | Color | Purpose | Target |
|-------------|-------|---------|--------|
| **TREND CALL** | 🟢 Green | Major uptrend confirmed | 50-200 points |
| **TREND PUT** | 🔴 Red | Major downtrend confirmed | 50-200 points |
| **SCALP CALL** | 🔵 Cyan | Quick bounce/reversal up | 20-50 points |
| **SCALP PUT** | 🟣 Magenta | Quick drop/reversal down | 20-50 points |
| **⚠️ STOP** | 🟠 Orange | Exit signal - trade going wrong | - |
| **✓ TARGET HIT** | 🟢 Green | Profit target reached | - |

---

# 1. VWAP - Volume Weighted Average Price

## What is VWAP?

VWAP (Volume Weighted Average Price) is the **average price** a stock has traded at throughout the day, weighted by **volume**. It's considered the "fair price" for the day.

## Formula

```
VWAP = Cumulative(Price × Volume) / Cumulative(Volume)

Where Price = (High + Low + Close) / 3
```

## How to Read VWAP

| Condition | Meaning | Signal |
|-----------|---------|--------|
| **Price > VWAP** | Buyers are in control, bullish sentiment | ✅ BULLISH - Favor CALL |
| **Price < VWAP** | Sellers are in control, bearish sentiment | ❌ BEARISH - Favor PUT |
| **Price = VWAP** | Fair value, no clear direction | ➖ NEUTRAL |

## Visual Representation

```
BULLISH: Price trading ABOVE VWAP
─────────────────────────────────────
         ████ Price
        ██
       ██
══════════════════════════════════════  ← VWAP Line (Blue)
    Support zone


BEARISH: Price trading BELOW VWAP
─────────────────────────────────────
    Resistance zone
══════════════════════════════════════  ← VWAP Line (Blue)
       ██
        ██
         ████ Price
```

## VWAP Trading Rules

1. **Institutional traders** use VWAP as benchmark - they buy below VWAP, sell above
2. **Intraday only** - VWAP resets every day at market open
3. **Strong support/resistance** - Price often bounces off VWAP
4. **Trend confirmation** - Sustained trading above/below VWAP confirms trend

## In Our Script

- **+3 points for CALL** when price > VWAP
- **+3 points for PUT** when price < VWAP
- Displayed as **blue line** on chart

---

# 2. CPR - Central Pivot Range

## What is CPR?

CPR (Central Pivot Range) consists of three levels calculated from **previous day's High, Low, Close**. It predicts potential support/resistance zones for the current day.

## Formula

```
Pivot Point (PP) = (Previous High + Previous Low + Previous Close) / 3
Bottom Central (BC) = (Previous High + Previous Low) / 2
Top Central (TC) = (PP - BC) + PP

Support Levels:
S1 = (2 × PP) - Previous High
S2 = PP - (Previous High - Previous Low)
S3 = Previous Low - 2 × (Previous High - PP)

Resistance Levels:
R1 = (2 × PP) - Previous Low
R2 = PP + (Previous High - Previous Low)
R3 = Previous High + 2 × (PP - Previous Low)
```

## How to Read CPR

| Condition | Meaning | Signal |
|-----------|---------|--------|
| **Price > TC** | Strong bullish, above resistance | ✅ STRONG BULLISH |
| **Price between PP and TC** | Mild bullish | ✅ BULLISH |
| **Price between BC and PP** | Mild bearish | ❌ BEARISH |
| **Price < BC** | Strong bearish, below support | ❌ STRONG BEARISH |

## CPR Width Analysis

```
CPR Width % = ((TC - BC) / PP) × 100

Narrow CPR (< 0.1%): Trending day expected - TRADE BREAKOUTS
Wide CPR (> 0.3%): Sideways day expected - TRADE REVERSALS
```

## Visual Representation

```
                          R3 ─────────── (Resistance 3)
                          R2 ─────────── (Resistance 2)
                          R1 ─────────── (Resistance 1)
BULLISH ZONE ↑           
                          TC ═══════════ (Top Central) - Orange
                          PP ─────────── (Pivot Point) - Yellow
                          BC ═══════════ (Bottom Central) - Orange
BEARISH ZONE ↓
                          S1 ─────────── (Support 1)
                          S2 ─────────── (Support 2)
                          S3 ─────────── (Support 3)
```

## CPR Trading Rules

1. **Price > TC** = Look for CALL opportunities
2. **Price < BC** = Look for PUT opportunities
3. **Price in CPR range** = Wait for breakout
4. **Narrow CPR** = Expect big move, trade with trend
5. **Wide CPR** = Expect range-bound, trade reversals

## In Our Script

- **+3 points for CALL** when price > TC
- **+3 points for PUT** when price < BC
- Displayed as **yellow/orange lines** on chart

---

# 3. EMA - Exponential Moving Average

## What is EMA?

EMA (Exponential Moving Average) is a type of moving average that gives **more weight to recent prices**, making it more responsive to new information than a Simple Moving Average (SMA).

## Formula

```
EMA = (Current Price × Multiplier) + (Previous EMA × (1 - Multiplier))

Where Multiplier = 2 / (Period + 1)

For 9 EMA: Multiplier = 2 / (9 + 1) = 0.2
For 21 EMA: Multiplier = 2 / (21 + 1) = 0.0909
For 50 EMA: Multiplier = 2 / (50 + 1) = 0.0392
```

## Three EMAs Used

| EMA | Period | Color | Purpose |
|-----|--------|-------|---------|
| **Fast EMA** | 9 | 🟢 Green | Short-term trend, quick signals |
| **Medium EMA** | 21 | 🔵 Blue | Medium-term trend |
| **Slow EMA** | 50 | 🟠 Orange | Long-term trend, major support/resistance |

## EMA Stack - Trend Identification

```
BULLISH STACK (Strong Uptrend):
9 EMA > 21 EMA > 50 EMA

         9 EMA  ════════════════════ (Green - Top)
        21 EMA ════════════════════ (Blue - Middle)
       50 EMA ════════════════════ (Orange - Bottom)
      Price rising ↗


BEARISH STACK (Strong Downtrend):
9 EMA < 21 EMA < 50 EMA

       50 EMA ════════════════════ (Orange - Top)
        21 EMA ════════════════════ (Blue - Middle)
         9 EMA  ════════════════════ (Green - Bottom)
      Price falling ↘
```

## EMA Crossovers

| Crossover | What Happens | Signal |
|-----------|--------------|--------|
| **9 EMA crosses ABOVE 21 EMA** | Fast trend turning up | ✅ BULLISH CROSS - Buy signal |
| **9 EMA crosses BELOW 21 EMA** | Fast trend turning down | ❌ BEARISH CROSS - Sell signal |

## Visual Crossover

```
BULLISH CROSSOVER (Golden Cross):
                    ↗ 9 EMA crosses above
                   ╳
                  ↗ 21 EMA
Before: 9 < 21    After: 9 > 21
Signal: BUY CALL


BEARISH CROSSOVER (Death Cross):
Before: 9 > 21    After: 9 < 21
                  ↘ 9 EMA crosses below
                   ╳
                    ↘ 21 EMA
Signal: BUY PUT
```

## EMA Trading Rules

1. **All 3 EMAs aligned bullish** = Strong uptrend, buy CALL on dips
2. **All 3 EMAs aligned bearish** = Strong downtrend, buy PUT on rallies
3. **EMAs tangled/mixed** = No clear trend, avoid trading
4. **Price above all EMAs** = Very bullish
5. **Price below all EMAs** = Very bearish
6. **EMA acts as dynamic support/resistance**

## In Our Script

- **+3 points for CALL** when 9 > 21 > 50 (bullish stack)
- **+3 points for PUT** when 9 < 21 < 50 (bearish stack)
- **+2 bonus points** for crossover signals
- Displayed as **green, blue, orange lines** on chart

---

# 4. Supertrend

## What is Supertrend?

Supertrend is a **trend-following indicator** that plots a line above or below price based on ATR (Average True Range). It's one of the most reliable indicators for identifying trend direction.

## Formula

```
Basic Upper Band = (High + Low) / 2 + (Multiplier × ATR)
Basic Lower Band = (High + Low) / 2 - (Multiplier × ATR)

Default Settings:
- ATR Period: 10
- Multiplier: 3.0
```

## How Supertrend Works

| Condition | Line Position | Color | Meaning |
|-----------|---------------|-------|---------|
| **Uptrend** | Line BELOW price | 🟢 Green | BULLISH - Price supported |
| **Downtrend** | Line ABOVE price | 🔴 Red | BEARISH - Price resisted |

## Visual Representation

```
BULLISH SUPERTREND (Green line below price):

    ████████
   ██      ██████
  ██            ████████
 ══════════════════════════════  ← Supertrend (GREEN) - Support
 
Price stays ABOVE the green line = Uptrend continues
Buy CALL, hold until line turns red


BEARISH SUPERTREND (Red line above price):

 ══════════════════════════════  ← Supertrend (RED) - Resistance
  ██            ████████
   ██      ██████
    ████████

Price stays BELOW the red line = Downtrend continues
Buy PUT, hold until line turns green
```

## Supertrend Flip Signals (ST↑ and ST↓)

| Signal | What Happened | Meaning | Action |
|--------|---------------|---------|--------|
| **ST↑** | Line changed from RED to GREEN | Trend flipped BULLISH | Consider CALL, Exit PUT |
| **ST↓** | Line changed from GREEN to RED | Trend flipped BEARISH | Consider PUT, Exit CALL |

## Visual Flip Example

```
SUPERTREND FLIP FROM BEARISH TO BULLISH (ST↑):

══════════════════╗                    ← Red line (Bearish)
                  ║
                  ║ FLIP POINT (ST↑)
                  ║
                  ╚══════════════════  ← Green line (Bullish)
                   ████████
                  ██
                 ██  Price starts rising


SUPERTREND FLIP FROM BULLISH TO BEARISH (ST↓):

                 ██  Price starts falling
                  ██
                   ████████
                  ╔══════════════════  ← Red line (Bearish)
                  ║
                  ║ FLIP POINT (ST↓)
                  ║
══════════════════╝                    ← Green line (Bullish)
```

## Supertrend Trading Rules

1. **Green Supertrend** = Only look for CALL trades
2. **Red Supertrend** = Only look for PUT trades
3. **ST↑ (Flip to Green)** = Strong BUY signal, exit all PUT positions
4. **ST↓ (Flip to Red)** = Strong SELL signal, exit all CALL positions
5. **Supertrend as Stop Loss** = Exit when price closes beyond the line
6. **Don't trade against Supertrend** = Most important rule!

## In Our Script

- **+3 points for CALL** when Supertrend is green (bullish)
- **+3 points for PUT** when Supertrend is red (bearish)
- **+4 bonus points** for Supertrend flip (SCALP signals)
- **Triggers STOP signal** when Supertrend flips against position
- Displayed as **green/red line** on chart

---

# 5. RSI - Relative Strength Index

## What is RSI?

RSI (Relative Strength Index) measures the **speed and magnitude of price changes** to identify overbought or oversold conditions. It oscillates between 0 and 100.

## Formula

```
RSI = 100 - (100 / (1 + RS))

Where RS = Average Gain / Average Loss (over 14 periods)
```

## How to Read RSI

| RSI Value | Condition | Meaning | Signal |
|-----------|-----------|---------|--------|
| **> 70** | Overbought | Price may be too high, reversal likely | ⚠️ Caution for CALL, Good for PUT |
| **50 - 70** | Bullish | Healthy uptrend | ✅ Good for CALL |
| **30 - 50** | Bearish | Healthy downtrend | ❌ Good for PUT |
| **< 30** | Oversold | Price may be too low, bounce likely | ⚠️ Caution for PUT, Good for CALL |

## Visual RSI Levels

```
100 ─────────────────────────────
    │
 80 │  ═══════════════════════════  OVERBOUGHT ZONE (Sell Zone)
 70 │  ───────────────────────────  Overbought Line
    │
    │        ╱╲      ╱╲
 50 │  ─────╱──╲────╱──╲─────────  Neutral Line
    │      ╱    ╲  ╱    ╲
 30 │  ───────────────────────────  Oversold Line
 20 │  ═══════════════════════════  OVERSOLD ZONE (Buy Zone)
    │
  0 ─────────────────────────────
```

## RSI Trading Strategies

### Strategy 1: Overbought/Oversold
```
RSI < 30 (Oversold) → Wait for RSI to turn up → BUY CALL
RSI > 70 (Overbought) → Wait for RSI to turn down → BUY PUT
```

### Strategy 2: Trend Confirmation
```
In Uptrend: RSI staying between 40-80 = Healthy trend, continue CALL
In Downtrend: RSI staying between 20-60 = Healthy trend, continue PUT
```

## In Our Script

- **+2 points for CALL** when RSI > 50 and not overbought
- **+2 points for PUT** when RSI < 50 and not oversold
- **+3 points for SCALP CALL** when RSI < 30 (oversold bounce)
- **+3 points for SCALP PUT** when RSI > 70 (overbought reversal)
- **Background color** changes when RSI is in extreme zones

---

# 6. MACD - Moving Average Convergence Divergence

## What is MACD?

MACD shows the relationship between two EMAs of price. It helps identify trend direction, momentum, and potential reversals.

## Formula

```
MACD Line = 12 EMA - 26 EMA
Signal Line = 9 EMA of MACD Line
Histogram = MACD Line - Signal Line
```

## MACD Components

| Component | What It Shows |
|-----------|---------------|
| **MACD Line** (Blue) | Difference between fast and slow EMAs |
| **Signal Line** (Orange) | Smoothed MACD line |
| **Histogram** (Green/Red bars) | Distance between MACD and Signal |

## How to Read MACD

| Condition | Meaning | Signal |
|-----------|---------|--------|
| **MACD > Signal** | Bullish momentum | ✅ BULLISH |
| **MACD < Signal** | Bearish momentum | ❌ BEARISH |
| **MACD crosses ABOVE Signal** | Momentum turning bullish | ✅ BUY Signal |
| **MACD crosses BELOW Signal** | Momentum turning bearish | ❌ SELL Signal |
| **Histogram expanding (green)** | Bullish momentum increasing | ✅ Trend strengthening |
| **Histogram expanding (red)** | Bearish momentum increasing | ❌ Trend strengthening |

## Visual MACD

```
BULLISH MACD:
                        ╱ MACD Line (above)
                       ╱
Signal Line ──────────╳────────
                     ╱
                    ╱ Crossover = BUY

Histogram:  ▁▂▃▄▅▆▇█  (Green, expanding = Strong bullish)


BEARISH MACD:
                    ╲ MACD Line (below)
                     ╲
Signal Line ──────────╳────────
                       ╲
                        ╲ Crossover = SELL

Histogram:  █▇▆▅▄▃▂▁  (Red, expanding = Strong bearish)
```

## MACD Trading Rules

1. **MACD > Signal** = Bullish, favor CALL
2. **MACD < Signal** = Bearish, favor PUT
3. **Bullish crossover** = Strong buy signal
4. **Bearish crossover** = Strong sell signal
5. **Histogram direction** = Shows momentum strength

## In Our Script

- **+2 points for CALL** when MACD > Signal
- **+2 points for PUT** when MACD < Signal
- **+3 bonus points** for MACD crossovers
- **+1 point** when histogram is expanding in trend direction

---

# 7. Stochastic Oscillator

## What is Stochastic?

Stochastic compares the **closing price** to the **price range** over a period. It helps identify overbought/oversold conditions and momentum shifts.

## Formula

```
%K = ((Current Close - Lowest Low) / (Highest High - Lowest Low)) × 100
%D = 3-period SMA of %K
```

## How to Read Stochastic

| Condition | Meaning | Signal |
|-----------|---------|--------|
| **%K > 80** | Overbought | ⚠️ Potential reversal down |
| **%K < 20** | Oversold | ⚠️ Potential reversal up |
| **%K crosses ABOVE %D (below 20)** | Bullish momentum starting | ✅ Strong BUY |
| **%K crosses BELOW %D (above 80)** | Bearish momentum starting | ❌ Strong SELL |

## Visual Stochastic

```
100 ─────────────────────────────
 80 │══════════════════════════  OVERBOUGHT (Sell Zone)
    │     ╱╲
    │    ╱  ╲  ← %K crosses below %D here = SELL
    │   ╱    ╳
 50 │──╱──────╲─────────────────
    │ ╱        ╲
    │╱          ╳  ← %K crosses above %D here = BUY
 20 │══════════════════════════  OVERSOLD (Buy Zone)
  0 ─────────────────────────────

%K = Fast line (Blue)
%D = Slow line (Orange)
```

## In Our Script

- **+1 point for CALL** when %K > %D (bullish)
- **+1 point for PUT** when %K < %D (bearish)
- **+3 bonus points for SCALP CALL** when bullish cross in oversold zone
- **+3 bonus points for SCALP PUT** when bearish cross in overbought zone

---

# 8. ADX - Average Directional Index

## What is ADX?

ADX measures **trend strength** (not direction). It tells you HOW STRONG the trend is, regardless of whether it's up or down.

## Components

| Component | What It Shows |
|-----------|---------------|
| **ADX** (Yellow) | Trend strength (0-100) |
| **+DI** (Green) | Bullish directional movement |
| **-DI** (Red) | Bearish directional movement |

## How to Read ADX

| ADX Value | Trend Strength | Trading Action |
|-----------|----------------|----------------|
| **< 20** | Weak/No trend (Choppy) | ⚠️ AVOID trading, wait |
| **20 - 25** | Trend emerging | 👀 Watch for breakout |
| **25 - 50** | Strong trend | ✅ Trade with trend |
| **> 50** | Very strong trend | ✅ Strong trend, but may be exhausted |

## Directional Movement (+DI / -DI)

| Condition | Meaning | Signal |
|-----------|---------|--------|
| **+DI > -DI** | Buyers stronger than sellers | ✅ BULLISH direction |
| **-DI > +DI** | Sellers stronger than buyers | ❌ BEARISH direction |
| **+DI crosses above -DI** | Trend turning bullish | ✅ BUY signal |
| **-DI crosses above +DI** | Trend turning bearish | ❌ SELL signal |

## Visual ADX

```
STRONG BULLISH TREND:
ADX = 35 (Strong trend)
+DI = 30 (Green - above)
-DI = 15 (Red - below)

ADX ════════════════════════ 35
+DI ──────────────────────── 30  (Above = Bullish)
-DI ........................ 15  (Below)

Action: BUY CALL with confidence


CHOPPY MARKET (NO TREND):
ADX = 15 (Weak trend)

ADX ════════════════════════ 15
+DI ──────────────────────── 18
-DI ........................ 16

Action: AVOID TRADING, wait for ADX > 20
```

## ADX Trading Rules

1. **ADX < 20** = Choppy market, DON'T trade (-5 points penalty in our script)
2. **ADX > 25 with +DI > -DI** = Strong uptrend, BUY CALL
3. **ADX > 25 with -DI > +DI** = Strong downtrend, BUY PUT
4. **Rising ADX** = Trend strengthening
5. **Falling ADX** = Trend weakening

## In Our Script

- **+2 points for CALL** when ADX > 20 AND +DI > -DI
- **+2 points for PUT** when ADX > 20 AND -DI > +DI
- **-5 points penalty** when ADX < 20 (choppy market)
- Dashboard shows "TREND" or "WEAK" based on ADX value

---

# 9. Volume Analysis

## What is Volume?

Volume represents the **number of shares/contracts traded**. It confirms the strength of price movements.

## How to Read Volume

| Condition | Meaning | Signal |
|-----------|---------|--------|
| **High Volume + Bullish Candle** | Strong buying interest | ✅ Confirms uptrend |
| **High Volume + Bearish Candle** | Strong selling interest | ❌ Confirms downtrend |
| **Low Volume + Any Move** | Weak conviction | ⚠️ Move may not sustain |
| **Volume Spike** | Significant event | 👀 Watch for breakout/reversal |

## Volume Analysis in Our Script

```
Volume Confirmation = Current Volume > (20-period SMA × 1.2)

High Volume + Green Candle = Bullish confirmation (+2 points for CALL)
High Volume + Red Candle = Bearish confirmation (+2 points for PUT)
```

## In Our Script

- **+1 point for CALL** when high volume with bullish candle
- **+1 point for PUT** when high volume with bearish candle
- **+2 points for SCALP** when volume confirms direction

---

# 10. Bollinger Bands

## What are Bollinger Bands?

Bollinger Bands consist of a middle band (SMA) with upper and lower bands based on standard deviation. They show volatility and potential overbought/oversold levels.

## Formula

```
Middle Band = 20-period SMA
Upper Band = Middle Band + (2 × Standard Deviation)
Lower Band = Middle Band - (2 × Standard Deviation)
```

## How to Read Bollinger Bands

| Condition | Meaning | Signal |
|-----------|---------|--------|
| **Price at Upper Band** | Potentially overbought | ⚠️ Watch for reversal down |
| **Price at Lower Band** | Potentially oversold | ⚠️ Watch for reversal up |
| **Bands Squeezing** | Low volatility, breakout coming | 👀 Prepare for big move |
| **Bands Expanding** | High volatility | ✅ Trend in progress |

## Visual Bollinger Bands

```
Upper Band ═══════════════════════════════  (Red)
                    ╱╲
                   ╱  ╲  Price touching upper = Overbought
Middle Band ─────╱────╲─────────────────────  (Gray)
                ╱      ╲
               ╱        ╲  Price touching lower = Oversold
Lower Band ═══════════════════════════════  (Green)


BOLLINGER SQUEEZE (Breakout coming):
        ════════════════════
        ────────────────────  Bands come close together
        ════════════════════
        
        Then EXPAND → Big move!
```

## In Our Script

- **+1 point for CALL** when price at lower band AND RSI oversold
- **+1 point for PUT** when price at upper band AND RSI overbought
- Bollinger Squeeze detected → Alert for potential breakout

---

# 11. Parabolic SAR

## What is Parabolic SAR?

Parabolic SAR (Stop and Reverse) plots dots above or below price to indicate trend direction and potential reversal points.

## How to Read Parabolic SAR

| Condition | Meaning | Signal |
|-----------|---------|--------|
| **Dots BELOW price** | Uptrend | ✅ BULLISH |
| **Dots ABOVE price** | Downtrend | ❌ BEARISH |
| **Dots flip position** | Trend reversal | 🔄 Change direction |

## Visual Parabolic SAR

```
BULLISH (Dots below price):
        ████████████
       ██          ██
      ██            ██
 · · · · · · · · · · · ·  ← SAR Dots (below = bullish)


BEARISH (Dots above price):
 · · · · · · · · · · · ·  ← SAR Dots (above = bearish)
      ██            ██
       ██          ██
        ████████████
```

## In Our Script

- **+1 point for CALL** when SAR below price
- **+1 point for PUT** when SAR above price

---

# 12. ATR - Average True Range

## What is ATR?

ATR measures **volatility** by calculating the average range between high and low over a period. It's used for setting stop loss levels.

## Formula

```
True Range = Maximum of:
  1. Current High - Current Low
  2. |Current High - Previous Close|
  3. |Current Low - Previous Close|

ATR = 14-period average of True Range
```

## How to Use ATR

| Usage | Calculation |
|-------|-------------|
| **Stop Loss** | Entry Price - (1.5 × ATR) for CALL |
| **Stop Loss** | Entry Price + (1.5 × ATR) for PUT |
| **Target** | Entry Price + (2 × ATR) for reasonable target |
| **Volatility Check** | ATR > 1.5 × Average = High volatility, be cautious |

## In Our Script

- ATR used to calculate **Stop Loss** levels
- **+1 point** when ATR is in normal range (not too volatile)
- High volatility = Penalty applied

---

# Signal Types Explained

## V1 Signals (Original)

| Signal | When It Appears | Action |
|--------|-----------------|--------|
| **BUY CALL [score]** | CALL score > PUT score and > threshold | Buy Call Option |
| **BUY PUT [score]** | PUT score > CALL score and > threshold | Buy Put Option |

## V4 Signals (Enhanced)

### Entry Signals

| Signal | Color | When It Appears | Action |
|--------|-------|-----------------|--------|
| **TREND CALL** | 🟢 Green | Major indicators aligned bullish, score > 15 | Buy Call for swing trade |
| **TREND PUT** | 🔴 Red | Major indicators aligned bearish, score > 15 | Buy Put for swing trade |
| **SCALP CALL** | 🔵 Cyan | Momentum turning up (oversold bounce) | Buy Call for quick 30 pts |
| **SCALP PUT** | 🟣 Magenta | Momentum turning down (overbought drop) | Buy Put for quick 30 pts |

### Exit Signals

| Signal | Color | When It Appears | Action |
|--------|-------|-----------------|--------|
| **⚠️ STOP CALL - SL HIT** | 🟠 Orange | Price dropped below stop loss | Exit Call immediately |
| **⚠️ STOP CALL - ST FLIP** | 🟠 Orange | Supertrend turned bearish | Exit Call immediately |
| **⚠️ STOP CALL - REVERSAL** | 🟠 Orange | Multiple indicators turned bearish | Exit Call immediately |
| **⚠️ STOP CALL - WEAK** | 🟠 Orange | Trade not working, 2 bearish candles | Exit Call |
| **⚠️ STOP PUT - SL HIT** | 🟠 Orange | Price rose above stop loss | Exit Put immediately |
| **⚠️ STOP PUT - ST FLIP** | 🟠 Orange | Supertrend turned bullish | Exit Put immediately |
| **⚠️ STOP PUT - REVERSAL** | 🟠 Orange | Multiple indicators turned bullish | Exit Put immediately |
| **⚠️ STOP PUT - WEAK** | 🟠 Orange | Trade not working, 2 bullish candles | Exit Put |
| **✓ TARGET HIT** | 🟢 Green | Price reached profit target | Book profit! |

### Information Signals

| Signal | Meaning |
|--------|---------|
| **ST↑** | Supertrend flipped bullish (trend change) |
| **ST↓** | Supertrend flipped bearish (trend change) |

---

# Confluence Scoring System

## How Points Are Calculated

### TREND CALL Score (Max ~27 points)

| Indicator | Condition | Points |
|-----------|-----------|--------|
| VWAP | Price > VWAP | +3 |
| CPR | Price > TC | +3 |
| EMA Stack | 9 > 21 > 50 | +3 |
| MACD | MACD > Signal | +2 |
| Supertrend | Green (bullish) | +3 |
| ADX | +DI > -DI and ADX > 20 | +2 |
| RSI | RSI > 50 and not overbought | +2 |
| Stochastic | %K > %D | +1 |
| Volume | High volume + bullish candle | +1 |
| **Bonus: EMA Cross** | 9 crosses above 21 | +2 |
| **Bonus: MACD Cross** | MACD crosses above Signal | +2 |
| **Bonus: ST Flip** | Supertrend turns green | +3 |

### TREND PUT Score (Max ~27 points)

| Indicator | Condition | Points |
|-----------|-----------|--------|
| VWAP | Price < VWAP | +3 |
| CPR | Price < BC | +3 |
| EMA Stack | 9 < 21 < 50 | +3 |
| MACD | MACD < Signal | +2 |
| Supertrend | Red (bearish) | +3 |
| ADX | -DI > +DI and ADX > 20 | +2 |
| RSI | RSI < 50 and not oversold | +2 |
| Stochastic | %K < %D | +1 |
| Volume | High volume + bearish candle | +1 |
| **Bonus: EMA Cross** | 9 crosses below 21 | +2 |
| **Bonus: MACD Cross** | MACD crosses below Signal | +2 |
| **Bonus: ST Flip** | Supertrend turns red | +3 |

### SCALP CALL Score (Max ~29 points)

| Indicator | Condition | Points |
|-----------|-----------|--------|
| Fast EMA Rising | 9 EMA > 9 EMA[2] | +2 |
| RSI Rising | RSI > RSI[2] | +2 |
| MACD Hist Rising | Histogram increasing | +2 |
| Price > Fast EMA | Close > 9 EMA | +2 |
| RSI Oversold | RSI < 30 | +3 |
| Stochastic Oversold | %K < 20 | +2 |
| Stoch Bullish Cross | %K crosses above %D | +3 |
| Higher Low | Current low > previous low | +2 |
| 2 Bullish Candles | Last 2 candles green | +2 |
| Volume Confirm | High volume + green candle | +2 |
| **Bonus: ST Flip** | Supertrend turns green | +4 |
| **Bonus: MACD Cross** | MACD crosses above Signal | +3 |

### SCALP PUT Score (Max ~29 points)

| Indicator | Condition | Points |
|-----------|-----------|--------|
| Fast EMA Falling | 9 EMA < 9 EMA[2] | +2 |
| RSI Falling | RSI < RSI[2] | +2 |
| MACD Hist Falling | Histogram decreasing | +2 |
| Price < Fast EMA | Close < 9 EMA | +2 |
| RSI Overbought | RSI > 70 | +3 |
| Stochastic Overbought | %K > 80 | +2 |
| Stoch Bearish Cross | %K crosses below %D | +3 |
| Lower High | Current high < previous high | +2 |
| 2 Bearish Candles | Last 2 candles red | +2 |
| Volume Confirm | High volume + red candle | +2 |
| **Bonus: ST Flip** | Supertrend turns red | +4 |
| **Bonus: MACD Cross** | MACD crosses below Signal | +3 |

### Signal Thresholds

| Signal Type | Minimum Score Required | Additional Condition |
|-------------|------------------------|----------------------|
| TREND CALL | 15 | CALL score > PUT score + 5 |
| TREND PUT | 15 | PUT score > CALL score + 5 |
| SCALP CALL | 12 | CALL score > PUT score + 4 |
| SCALP PUT | 12 | PUT score > CALL score + 4 |

---

# Quick Reference Cheat Sheet

## Bullish Signals (Buy CALL)

```
✅ Price > VWAP (Blue line)
✅ Price > TC (Top Central Pivot - Orange)
✅ EMA Stack: 9 (Green) > 21 (Blue) > 50 (Orange)
✅ Supertrend: GREEN line below price
✅ MACD: MACD line > Signal line
✅ RSI: Between 50-70 (not overbought)
✅ ADX: > 20 with +DI > -DI
✅ Stochastic: %K > %D
```

## Bearish Signals (Buy PUT)

```
❌ Price < VWAP (Blue line)
❌ Price < BC (Bottom Central Pivot - Orange)
❌ EMA Stack: 9 (Green) < 21 (Blue) < 50 (Orange)
❌ Supertrend: RED line above price
❌ MACD: MACD line < Signal line
❌ RSI: Between 30-50 (not oversold)
❌ ADX: > 20 with -DI > +DI
❌ Stochastic: %K < %D
```

## When NOT to Trade

```
⚠️ ADX < 20 (Choppy/No trend)
⚠️ Price stuck inside CPR range
⚠️ EMAs tangled/mixed
⚠️ Low volume
⚠️ Conflicting signals (CALL and PUT scores similar)
⚠️ First 15-30 minutes of market open
⚠️ Last 30 minutes before market close
⚠️ Before major news/events
```

## Quick Decision Matrix

| VWAP | EMA | Supertrend | MACD | Action |
|------|-----|------------|------|--------|
| ✅ Above | ✅ Bullish | 🟢 Green | ✅ Bullish | **STRONG CALL** |
| ❌ Below | ❌ Bearish | 🔴 Red | ❌ Bearish | **STRONG PUT** |
| ✅ Above | ❌ Mixed | 🟢 Green | ✅ Bullish | Moderate CALL |
| ❌ Below | ❌ Mixed | 🔴 Red | ❌ Bearish | Moderate PUT |
| Any | Mixed | Flipping | Crossing | SCALP opportunity |
| Any | Mixed | Mixed | Mixed | **AVOID - Wait** |

---

# Dashboard Quick Reference

## V4 Dashboard Elements

```
═══ CONFLUENCE V4 ═══
─── TREND ───
CALL:        15    (Green if ≥15, bright if ≥20)
PUT:         8     (Red if ≥15, bright if ≥20)
─── SCALP ───
CALL:        12    (Cyan if ≥12, bright if ≥15)
PUT:         6     (Magenta if ≥12, bright if ≥15)
─── POSITION ───
Status:      IN CALL / IN PUT / FLAT
Entry:       25450.00
P&L:         +35.5 pts (Green if profit, Red if loss)
─── STATUS ───
VWAP:        ↑ (Green) or ↓ (Red)
EMA:         ↑↑ (Bullish) or ↓↓ (Bearish) or → (Mixed)
ST:          ↑ (Green) or ↓ (Red)
MACD:        ↑ (Green) or ↓ (Red)
RSI:         55 / OS (Oversold) / OB (Overbought)
ADX:         28 (Green if trending, Orange if weak)
```

---

## Summary: Using V1 and V4 Together

| Version | Best For | Signals |
|---------|----------|---------|
| **V1** | Simple trend following | BUY CALL, BUY PUT |
| **V4** | Complete trading system | TREND, SCALP, STOP, TARGET |

### Recommended Workflow

1. **Use V4** as your primary indicator
2. Look for **TREND signals** for larger moves (50+ points)
3. Look for **SCALP signals** for quick trades (30 points)
4. Always respect **STOP signals** - exit immediately
5. Book profit when **TARGET HIT** appears

---

*Document Version: 1.0*
*Last Updated: February 2025*
*For use with Multi-Confluence Indicator V1 & V4*
