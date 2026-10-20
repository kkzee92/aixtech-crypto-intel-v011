# Architecture (v0.11)

```mermaid
flowchart LR
    FX["fixtures/candles_synthetic.json"] --> M["market loader"]
    M --> RG["regime.py multi-scale + Keltner + multi-TF"]
    M --> ST["strategies.py multi-factor per asset class"]
    RG --> ST
    ST --> RK["risk.py class caps + anomaly + correlation + multi-TF"]
    CS["costs.py"] --> EN["engine.py paper fill"]
    RK --> EN
    EN --> AU["security.py audit chain + redaction + rate-limit"]
    PS["posture / RBAC"] --> CLI["cli.py scan, brief, posture, backtest"]
    EN --> CLI
```

Runtime dependencies are the Python standard library. Tests inject fetchers
and never open a socket. See [security-architecture.md](security-architecture.md)
and [asset-class-strategies.md](asset-class-strategies.md).
