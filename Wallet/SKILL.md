name: wallet-tracker
description: >
  Tracks smart money wallets to detect accumulation, distribution,
  insider activity, and early entries before price movements.

inputs:
  wallet:
    type: string
    description: Wallet address to analyze

  chain:
    type: string
    enum: [eth, base, sol]
    description: Blockchain of the wallet

  lookback_days:
    type: number
    description: How many days of activity to analyze

outputs:
  wallet_score:
    type: number
    description: 0–100 score of how profitable and early this wallet is

  activity:
    type: list
    description: Recent significant transactions

  signals:
    type: list
    description: Detected patterns like accumulation, sniping, or exit
    
