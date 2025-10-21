# Futures-Driven Spread-Betting Execution EA

This repository contains an **MT4 Expert Advisor (EA)** designed to execute and manage trades in a **spread-betting environment**, while being **driven by CME futures data and analysis** — specifically from the **S&P 500 E-mini (ES)** contract.  
It provides a way to apply professional, *order-flow-based futures logic* to retail execution through MT4.

---

## 🧭 Overview

The EA is intended for traders who:

- Use **Sierra Chart** or another professional futures platform for market structure and order-flow analysis.  
- Want to **execute quickly** through a retail broker (such as IG) without calculating position size or risk manually.  
- Prefer **mechanical execution and management** once a trade idea is formed.

It acts as a **bridge** — analysis and trade ideas are derived from CME futures data, while actual orders are executed on a **spread-betting instrument** (e.g., `SPX500(€)` in MT4).  
This allows futures-style trade management — defined risk, scaled exits, normalized tracking — within a simplified execution workflow.

---

## 💡 Why This Approach

**Analysis on futures (Sierra Chart), execution via spread-betting (MT4).**  
Trade decisions are based on the *real futures market*, not just price-based indicators.

- **True order-flow context:**  
  Sierra Chart provides **market depth (DOM)** and **actual traded orders**, showing genuine liquidity behavior and aggressive participation rather than simple price ticks.  
  This reveals *intent* and *imbalance* — critical for timing high-quality entries.

- **Probability-based structure:**  
  Daily, weekly, and monthly **volume distributions** (market profiles) define where price is statistically likely or unlikely to trade, replacing arbitrary technical “levels” with actual market-derived structure.

- **VWAP as an evolving probability distribution:**  
  The **VWAP** and its standard deviations are treated as a **real-time evolving probability curve**, offering context for balance, imbalance, and mean reversion during the session.

- **High-conviction setups:**  
  Combining order-flow aggression, absorption, and liquidity shifts with VWAP and profile structure creates **data-backed, repeatable setups** rather than subjective chart patterns.

- **Separation of analysis and execution:**  
  All trade ideas and bias are derived from **CME ES futures**, while **execution** takes place on a spread-betting product (e.g., IG’s `SPX500(€)`).  
  This isolates the analytical edge from MT4’s limitations.

- **Immediate, low-friction execution:**  
  The EA allows for **instant market entry** when a futures-based setup triggers — no manual risk or size calculation required in the moment.  
  Once in, levels can be adjusted visually on the chart while the EA automatically manages SL/TP spacing, partial exits, and normalized PnL tracking.

> In short: this setup uses **futures for information and probability**, and **spread-betting for speed and flexibility** — enabling data-driven analysis with streamlined execution.

---

## ⚙️ Core Features

- **Single position management:**  
  One active position per symbol/side — keeps execution clean and intentional.

- **Adaptive order handling:**  
  Recomputes stop distances per attempt and retries transient order errors, accommodating IG’s dynamic minimum-stop rules.

- **Multi-stage take-profit system:**  
  Each “contract” represents one TP stage (e.g., 2 = two-stage exit).  
  Equal spacing between stages; lines can be manually dragged to adjust targets.

- **Dynamic TP visualization:**  
  Draws horizontal lines (`TP_Line_#`) for each stage and updates them as trades progress.

- **Normalized performance tracking:**  
  Calculates “Locked In” profit in normalized points, ensuring consistency across partial closes.

- **On-chart information panel:**  
  Displays:
  - Remaining size (%)
  - Locked-in points (normalized)
  - Stop distance and projected outcome if hit
  - Next TP stage distance, % to close, and points locked

- **Error-resilient design:**  
  Handles common broker errors (`129`, `136`, `138`, etc.) gracefully, cleans up objects, and unloads automatically after the final close.

---

## 🧪 Tested Environment

| Component | Details |
|------------|----------|
| **Broker** | IG |
| **Symbol** | `SPX500(€)` |
| **Execution Type** | Spread-betting |
| **Pricing** | 1 point = 1.0 price unit |
| **Digits** | 1 decimal place (`MODE_POINT = 0.1`) |
| **Dynamic STOPLEVEL** | Typically ~5.0 points for small size; increases with position size |
| **Lot Step / Min Lot** | 0.1 |

---

## 🚀 Usage

1. **Attach** the EA to your target chart (e.g., `SPX500(€)`).
2. **Configure Inputs:**
   - `BUY_SELL` → Choose `Buy` or `Sell`
   - `Contracts` → Number of TP stages (each ≈ 1% risk)
   - `DistancePts` → Distance in chart points for SL and TP spacing
3. **Run the EA:**  
   It opens a market position and draws all TP lines automatically.
4. **Adjust Levels:**  
   Drag TP lines or modify SL/TP in MT4; the EA honors all changes.
5. **Automatic Management:**  
   Partial closes trigger as price hits each TP; the EA tracks locked-in profit and updates the panel.
6. **Completion:**  
   When all stages are closed, the EA removes its TP lines and unloads.

---

## 🧱 Design Notes

- Manages **one trade per symbol/side** for simplicity and precision.  
- Uses **Global Variables** (`EA_INIT_LOTS_x`, `EA_NEXT_STAGE_x`, etc.) to maintain state across partial closes.  
- Leaves the **info panel visible** after finishing, showing final normalized performance.  
- Cleans up all chart objects (`TP_Line_*`) after completion.

---

## ⚠️ Limitations

- **Single-position model:**  
  The EA is not designed to manage multiple simultaneous trades on the same symbol.
- **Not a signal generator:**  
  Trade entries are triggered manually based on futures-derived setups, not by MT4 indicators.
- **Broker restrictions apply:**  
  Dynamic stop distances and size-dependent minimums still govern execution.
- **Environment mismatch:**  
  Futures and spread-betting instruments differ slightly in price, spread, and tick precision.

---

## 🧠 Summary

This EA is designed as a **futures-informed execution tool** — not a signal generator.  
It allows a trader to act instantly when order-flow conviction appears, while delegating the mechanical work of execution, scaling, and PnL tracking to the platform.

**Futures provide the information.**  
**The EA handles the execution.**

---
