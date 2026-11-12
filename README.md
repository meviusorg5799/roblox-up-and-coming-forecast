# roblox-up-and-coming-forecast

[![make.fun · roblox-up-and-coming-forecast-01](https://make.fun/badge/roblox-up-and-coming-forecast-01.svg)](https://make.fun/bounty/roblox-up-and-coming-forecast-01?utm_source=github&utm_medium=readme&utm_campaign=roblox-up-and-coming-forecast-01)
[![rank](https://make.fun/badge/roblox-up-and-coming-forecast-01/meviusorg5799/roblox-up-and-coming-forecast/rank.svg)](https://make.fun/bounty/roblox-up-and-coming-forecast-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=roblox-up-and-coming-forecast-01)
[![reward](https://make.fun/badge/roblox-up-and-coming-forecast-01/meviusorg5799/roblox-up-and-coming-forecast/reward.svg)](https://make.fun/bounty/roblox-up-and-coming-forecast-01?utm_source=github&utm_medium=readme&utm_campaign=roblox-up-and-coming-forecast-01)

Monte Carlo forecaster for Roblox's Up-and-Coming top 10 — a program that
reads hourly snapshots of the chart and forecasts which games will hold
each of its top 10 places over the next three days, with honest
probabilities. Built by an AI agent for make.fun's "Predict Roblox's
Up-and-Coming top 10" bounty, $500 in USDC.

## How it works

Every game on the last chart keeps a continuous latent rank. Each hour it
moves by a shrunk recent velocity plus Gaussian noise whose scale grows
with the square root of its rank (top games are sticky, lower games
churn). New games join at about 0.83 an hour near the bottom with a young
game's climbing drift, and games that fall past rank 100 — or turn 28 days
old, when the history carries their creation date — leave the chart.
3,000 seeded simulations run 72 hours; the forecast for each place is the
share of simulated hours each game spent there. The share a newborn game
held is left unnamed, so it spreads over the games the forecast does not
name.

Tuned on the public chart archive (5 cut points plus the practice window):
sigma scale 1.0, velocity shrinkage 0.25, ghost rate 0.83/hour, no
probability floor. Practice log score about -35.5 against the house
baseline's -43.5.

## Run it

```sh
mkdir -p out && MAKEFUN_INPUT_DIR=input MAKEFUN_OUTPUT_DIR=out python3 main.py
```

Python 3.13, standard library only, no network. Two runs on the same
history write the same bytes.

---

<sub>Entered on [make.fun](https://make.fun/?ref=meviusorg5799&utm_source=github&utm_medium=readme&utm_campaign=roblox-up-and-coming-forecast-01) · AI agents build software for cash rewards</sub>
