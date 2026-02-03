name: rug-detector

description: >
  Detects rug pulls, honeypots, insider dumps, and developer exit scams
  by analyzing contract permissions, wallet behavior, liquidity flows,
  and onchain transaction patterns in real time.

inputs:
  token:
    type: string
    description: Token contract address

  chain:
    type: string
    enum: [eth, base, sol]
    description: Blockchain network

outputs:
  risk_score:
    type: number
    description: 0–100 probability the token is malicious

  rug_type:
    type: string
    description: honeypot, soft_rug, hard_rug, dev_dump, insider_dump, or safe

  confidence:
    type: number
    description: Confidence level (0–1) of the classification

  signals:
    type: list
    description: Human-readable warning signals

  flagged_wallets:
    type: list
    description: Wallets linked to developer, insiders, or known scam clusters

  liquidity_status:
    type: object
    description: Current and historical LP state
    fields:
      locked: boolean
      lock_duration: string
      lp_provider: string
      lp_removed_pct: number

  contract_risk:
    type: object
    description: Smart-contract level danger signals
    fields:
      mintable: boolean
      blacklistable: boolean
      pausable: boolean
      owner_renounced: boolean
      tax_modifiable: boolean

logic:
  steps:
    - Verify contract bytecode and proxy patterns
    - Detect mint, blacklist, tax, and owner-privileged functions
    - Analyze top holder concentration and insider wallets
    - Track liquidity add/remove events
    - Monitor developer wallet behavior
    - Detect honeypot and sell-tax traps
    - Compare against known scam wallet clusters
    - Compute risk score using weighted signals

risk_weights:
  liquidity_removed: 0.30
  dev_wallet_selling: 0.20
  mint_function_present: 0.15
  blacklist_or_pause: 0.15
  honeypot_tax: 0.10
  insider_cluster: 0.10

thresholds:
  safe: <20
  caution: 20–50
  danger: 50–80
  rug: >80
  
