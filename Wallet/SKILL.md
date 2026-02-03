name: wallet-intelligence

description: >
  Identifies and scores smart money wallets by analyzing trading performance,
  early entry behavior, developer links, and historical profitability to
  determine which wallets should be followed or ignored.

inputs:
  wallet:
    type: string
    description: Wallet address to analyze
  chain:
    type: string
    enum: [eth, base, sol]
  lookback_days:
    type: number
    description: How many days of wallet history to analyze

outputs:
  wallet_score:
    type: number
    description: 0–100 score of how intelligent and profitable this wallet is

  wallet_type:
    type: string
    description: smart_money, insider, dev_wallet, sniper, bot, or retail

  roi:
    type: number
    description: Historical return on investment %

  win_rate:
    type: number
    description: % of profitable trades

  avg_entry_time:
    type: number
    description: How early this wallet buys after token deployment (minutes)

  signals:
    type: list
    description: Detected behavior patterns

  linked_wallets:
    type: list
    description: Wallets frequently trading together

logic_steps:
  - Analyze trade history and PnL
  - Detect early entry vs late FOMO
  - Identify developer funding patterns
  - Detect coordinated wallets
  - Classify wallet behavior
  - Assign intelligence score

weights:
  roi: 0.30
  win_rate: 0.20
  entry_speed: 0.20
  insider_links: 0.15
  rug_avoidance: 0.15

thresholds:
  smart_money: >80
  watchlist: 60–80
  ignore: <60
  
