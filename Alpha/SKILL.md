name: alpha-hunter

description: >
  Discovers early crypto alpha by detecting pre-pump wallet behavior,
  deployer patterns, liquidity events, and social acceleration before
  tokens trend publicly.

inputs:
  chain:
    type: string
    enum: [eth, base, sol]

  risk_profile:
    type: string
    enum: [safe, degen]

outputs:
  opportunities:
    type: list
    description: Ranked list of high-probability alpha tokens

  confidence:
    type: number
    description: 0–100 confidence score for the overall list

  signals:
    type: list
    description: Human-readable reasons each token was selected

  rejected:
    type: list
    description: Tokens filtered out by rug risk or weak momentum

logic:
  steps:
    - Scan new token deployments and liquidity additions
    - Track deployer and early wallet funding sources
    - Detect clusters of smart wallets accumulating
    - Measure volume acceleration and holder growth
    - Cross-check every candidate against Rug Detector
    - Rank tokens using weighted alpha score

alpha_factors:
  smart_money_inflow: 0.30
  deployer_reputation: 0.15
  liquidity_growth: 0.20
  social_velocity: 0.15
  holder_growth: 0.10
  rug_safety: 0.10

thresholds:
  ignore: <30
  watch: 30–60
  strong: 60–80
  ape: >80
  
