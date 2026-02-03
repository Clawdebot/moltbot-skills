name: shadow-trader

description: >
  Produces real-time trading signals using Alpha Hunter,
  Rug Detector, Wallet Intelligence, and the learned model
  from paper trading performance. No capital is used.

inputs:
  chain:
    type: string
    enum: [eth, base, sol]

outputs:
  signals:
    type: list
    description: Real-time BUY, HOLD, or AVOID signals

  confidence:
    type: number
    description: 0–100 confidence score for each signal

logic:
  steps:
    - Scan new tokens and momentum using Alpha Hunter
    - Filter out tokens using Rug Detector
    - Score wallets using Wallet Intelligence
    - Apply performance.json learned weights
    - Rank opportunities
    - Output top signals as BUY, HOLD, or AVOID
    - Publish signals to signals.json
    
