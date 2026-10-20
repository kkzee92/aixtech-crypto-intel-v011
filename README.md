# AIxTech crypto intel v0.11: paper-only trading information system

Further advanced research harness for automated cryptocurrency **information** and paper strategy evaluation.
Builds on [kkzee92/aixtech-crypto-intel-v10](https://github.com/kkzee92/aixtech-crypto-intel-v10) and prior versions including the original [zeekiankok92/aixtech-crypto-intel](https://github.com/zeekiankok92/aixtech-crypto-intel).

It does not place live orders, does not store exchange secrets, and is not financial advice.

![Python](https://img.shields.io/badge/python-3.10%2B-blue)
![version](https://img.shields.io/badge/version-0.11.0-blue)
![mode](https://img.shields.io/badge/execution-paper%20only-orange)
![Licence](https://img.shields.io/badge/licence-MIT-green)

## Enhancements in v0.11

- Keltner Channel proxies (ATR-based) for volatility-adjusted breakouts and mean-reversion across classes.
- Volume-weighted momentum and multi-timeframe alignment checks (short/medium/long proxies).
- Portfolio-level correlation gate simulation in risk module (penalizes high-corr signals).
- Refined adaptive sizing with multi-factor confluence scoring.
- Expanded secret redaction including private keys, JWTs, connection strings, and seed-like patterns.
- Rate-limit and input-sanitization simulation in security controls.
- Updated architecture and strategy docs.

See [docs/asset-class-strategies.md](docs/asset-class-strategies.md) and [docs/security-architecture.md](docs/security-architecture.md).

## What it does

- Eight asset classes with advanced multi-factor research rules incorporating Keltner, VW-momentum, multi-TF, StochRSI, and cloud proxies.
- Multi-scale regime + volatility tier + anomaly scoring + correlation awareness.
- Signals with EMA, MACD, Bollinger, Keltner, ADX, VWAP, then multi-gate risk including portfolio correlation.
- Paper-only backtests with class costs; enhanced hash-chained audit and zero-trust controls.
- Synthetic candles only. No network by default.

| Asset class | Enhanced research rule (v0.11) | Risk cap (base) | Cost |
|---|---|---|---|
| Major | Multi-EMA + MACD + Keltner + Bollinger + ADX + VWAP + multi-TF + StochRSI + cloud; stand aside stress/high-vol/anomaly/high-corr | 8% | 8 bps |
| Large-cap alt | Volume + multi-momentum + Keltner upper + MACD + Bollinger + VWAP confirmation | 4% | 14 bps |
| Stablecoin | Adaptive peg + multi-stat (z, consecutive, skew, Keltner width) alerts only | 0% | n/a |
| DeFi | Calm multi-scale + Keltner/channel + momentum + cloud + low anomaly + multi-TF | 2% | 22 bps |
| Meme | Qualified burst with volume profile, Keltner not extreme, StochRSI, consistency | 0.5% | 45 bps |
| L2 | Multi-period RS + relative volume + correlation + multi-TF vs benchmark | 3% | 16 bps |
| RWA | Slow multi-scale low-vol trend with Keltner, cloud, adaptive gap, momentum | 2% | 12 bps |
| Perpetual | Funding carry with adaptive drift, Keltner stability, consistency, non-stress | 2% | 10 bps |

## Run

```bash
python3 -m venv .venv && source .venv/bin/activate
pip install -r requirements-dev.txt
python scripts/make_fixtures.py
PYTHONPATH=src python -m crypto_intel scan fixtures/candles_synthetic.json
PYTHONPATH=src python -m crypto_intel brief fixtures/candles_synthetic.json
PYTHONPATH=src python -m crypto_intel posture fixtures/candles_synthetic.json
```

## Controls

Paper-only. No live credentials. Class caps, adaptive confidence and sizing, kill switch, drawdown, statistical anomaly + correlation + multi-TF gates, hash-chained audit, expanded redaction, PDPA tripwire, gitleaks. Zero-trust research design with rate-limit simulation.

## Honesty

No live exchange connector. Scores describe synthetic fixtures. Not investment, legal, or compliance advice. Research only.
