# MQL4 Grid Trading EA

## Overview

This Expert Advisor (EA) implements a **dual-direction grid trading strategy** in MetaTrader 4 using MQL4. It places buy/sell orders based on an EMA crossover signal and manages position sizing using a **user-defined martingale scheme**. Positions are closed when a configurable **net profit target** is reached for either direction, accepting partial losses for overall gain.

## Features

- 🔁 **Grid trading logic** for both **Long (Buy)** and **Short (Sell)** directions
- 📊 **EMA(3,5,7)** crossover-based signal
- ⚙️ Independent settings for Buy and Sell:
  - Initial lot size
  - Max number of grid orders
  - Martingale multiplier
  - Number of repeat orders before increasing size
  - Grid spacing (in points)
  - Profit target to close all trades of one direction
- 🔄 Closes all trades in a direction once cumulative profit exceeds threshold
- 🧠 Accepts some unprofitable positions to lock in net profit

## How It Works

1. **Signal Generation**:
   - Buy signal: EMA(3) > EMA(5) > EMA(7)
   - Sell signal: EMA(3) < EMA(5) < EMA(7)

2. **Order Entry**:
   - Opens initial Buy/Sell trade if signal confirms and no active trades exist in that direction.
   - Adds new grid orders if:
     - Price moves against last order by more than configured grid distance
     - Total orders remain under `maxorder`
     - Lot size increases per user-defined `repeat` and `multiplier` logic

3. **Order Exit**:
   - Monitors net profit per direction (`profit_buy` or `profit_sell`)
   - Closes all orders in that direction when profit exceeds `close_profit_*`

## Inputs

| Parameter               | Description                                     |
|------------------------|-------------------------------------------------|
| `magic`                | Magic number to distinguish EA's orders         |
| `open_buy`             | Enable Buy trading                              |
| `lot_buy`              | Initial lot size for Buy                        |
| `maxorder_buy`         | Max number of Buy orders                        |
| `mul_buy`              | Martingale multiplier for Buy                   |
| `repeat_buy`           | Number of repeats before lot increase (Buy)     |
| `grid_buy`             | Distance (points) between Buy grid orders       |
| `close_profit_buy`     | Close all Buy orders if total profit ≥ this     |
| `open_sell`            | Enable Sell trading                             |
| `lot_sell`             | Initial lot size for Sell                       |
| `maxorder_sell`        | Max number of Sell orders                       |
| `mul_sell`             | Martingale multiplier for Sell                  |
| `repeat_sell`          | Number of repeats before lot increase (Sell)    |
| `grid_sell`            | Distance (points) between Sell grid orders      |
| `close_profit_sell`    | Close all Sell orders if total profit ≥ this    |

## Installation

1. Copy the `.mq4` file into your **MetaTrader 4/Experts/** folder.
2. Restart MetaTrader or refresh the Navigator pane.
3. Attach the EA to any chart (recommend 1H or 15M).
4. Set your input parameters and enable AutoTrading.

## Disclaimer

Use at your own risk. Grid and martingale strategies involve significant risk, especially during trending markets. Always test on demo accounts before deploying on live accounts.

