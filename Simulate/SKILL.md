name: paper-trader

description: >
  Simulates real crypto trading using signals from Alpha Hunter,
  Rug Detector, and Wallet Intelligence to build a verifiable track record
  before risking real capital.

inputs:
  chain:
    type: string
    enum: [eth, base, sol]
    description: Blockchain network
  risk_profile:
    type: string
    enum: [safe, degen]
    description: Trading risk level

outputs:
  trades:
    type: list
    description: Executed simulated trades
  capital:
    type: number
    description: Current paper capital
  pnl:
    type: number
    description: Profit or loss %
  win_rate:
    type: number
    description: Percentage of winning trades
  drawdown:
    type: number
    description: Max capital drop
  positions:
    type: list
    description: Currently open positions

logic:
  steps:
    - Fetch alpha candidates from Alpha Hunter
    - Remove tokens flagged by Rug Detector
    - Remove tokens where Wallet Intelligence score < 70
    - Allocate capital based on confidence and risk profile
    - Simulate buy at current price
    - Track price changes
    - Close trade when:
        - Take profit reached
        - Stop loss hit
        - Rug risk spikes
    - Log trade to trades.json
    - Update capital, PnL, win rate, drawdown

risk_rules:
  safe:
    max_per_trade: 5%
    stop_loss: 10%
    take_profit: 25%
  degen:
    max_per_trade: 15%
    stop_loss: 25%
    take_profit: 100%
    
