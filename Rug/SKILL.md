name: rug-detector
description: >
  Detects rug pulls, honeypots, insider dumps, and developer exit patterns
  by analyzing token behavior, wallet flows, and liquidity changes.

inputs:
  token:
    type: string
    description: Token contract address

  chain:
    type: string
    enum: [eth, base, sol]

outputs:
  risk_score:
    type: number
    description: 0–100 probability the token is a rug or scam

  rug_type:
    type: string
    description: honeypot, soft rug, hard rug, insider dump, or safe

  signals:
    type: list
    description: Detected warning signs

  wallets_flagged:
    type: list
    description: Wallets linked to suspicious activity

  liquidity_events:
    type: list
    description: LP add/remove, drains, or locks
    
