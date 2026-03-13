# Reinforcement Learning Trading Bot

A reinforcement learning based Forex trading bot that trains and evaluates a PPO (Proximal Policy Optimization) agent in a custom trading environment.

## Overview

This project learns trading behavior from historical EURUSD OHLCV data. It includes:
- Feature engineering with technical indicators
- A custom Gym-style trading environment
- PPO training with checkpointing
- Out-of-sample evaluation and equity curve plotting
- Trade history export during testing

## Features

- Custom Forex environment with spread, slippage, TP/SL options, and reward shaping
- PPO agent training via `stable-baselines3`
- Train/test split workflow
- Automatic checkpoint saving during training
- Best-model selection using out-of-sample final equity
- Evaluation plots and CSV trade export

## Project Structure

```text
Reinforcement Learning Trading Bot/
├─ README.md
├─ .gitignore
├─ ReinforcementTrading_Part_1/
│  ├─ indicators.py
│  ├─ trading_env.py
│  ├─ train_agent.py
│  ├─ test_agent.py
│  ├─ Requirements.txt
│  └─ data/
│     ├─ EURUSD_Candlestick_1_Hour_BID_01.07.2020-15.07.2023.csv
│     └─ test_EURUSD_Candlestick_1_Hour_BID_20.02.2023-22.02.2025.csv
└─ venv/
```

## Installation (Windows PowerShell)

1. Move to the project folder:

```powershell
cd "d:\Reinforcement Learning Trading Bot\ReinforcementTrading_Part_1"
```

2. Create a virtual environment:

```powershell
py -m venv venv
```

3. Activate it:

```powershell
.\venv\Scripts\Activate.ps1
```

4. Install dependencies:

```powershell
pip install -r Requirements.txt
```

## Usage

### 1) Train the agent

```powershell
python train_agent.py
```

Training script behavior:
- Loads and preprocesses market data
- Splits data into train/test segments
- Trains PPO and saves checkpoints under `./checkpoints`
- Selects best model by out-of-sample final equity
- Saves best model as `model_eurusd_best.zip`
- Plots in-sample and out-of-sample equity curves

### 2) Evaluate the trained agent

```powershell
python test_agent.py
```

Test script behavior:
- Loads `model_eurusd_best.zip`
- Runs one full evaluation episode
- Saves closed trades to `trade_history_output.csv` (if any)
- Displays equity curve

## Configuration

Tune these parameters directly in scripts:

- Data path (`file_path`) in `train_agent.py` and `test_agent.py`
- Stop-loss / take-profit options (`SL_OPTS`, `TP_OPTS`)
- Observation window (`WIN`)
- Environment frictions:
  - `spread_pips`
  - `commission_pips`
  - `max_slippage_pips`
- Reward shaping:
  - `hold_reward_weight`
  - `open_penalty_pips`
  - `time_penalty_pips`
  - `unrealized_delta_weight`
- Training timesteps (`total_timesteps`) in `train_agent.py`

Important: Keep environment parameters aligned between training and testing for consistent results.

## Outputs

Common generated artifacts:
- `checkpoints/` (intermediate PPO checkpoints)
- `model_eurusd_best.zip` (best selected model)
- `trade_history_output.csv` (closed trades from test run)

## Contributing

1. Fork the repository
2. Create a feature branch
3. Commit your changes
4. Open a pull request

## License

Add your preferred license file (for example, MIT) and update this section.
