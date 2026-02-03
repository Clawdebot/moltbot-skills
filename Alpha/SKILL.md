name: alpha-hunter

description: >
  Discovers early crypto alpha by detecting pre-pump wallet behavior,
  deployer patterns, liquidity events, and social acceleration —
  while filtering out scams using Rug Detector.

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
    description: Tokens filtered out due to rug risk or weak momentum

logic:
  steps:
    - Scan new token deployments and liquidity additions
    - Track deployer wallets and early funding sources
    - Detect clusters of smart wallets accumulating
    - Measure volume acceleration and holder growth
    - Call Rug Detector for every candidate token
    - Reject any token with risk_score > 50 or rug_type != "safe"
    - Rank remaining tokens using weighted alpha score

alpha_factors:
  smart_money_inflow: 0.25
  liquidity_growth: 0.20
  rug_safety: 0.20
  deployer_reputation: 0.15
  social_velocity: 0.10
  holder_growth: 0.10

thresholds:
  ignore: rug OR score < 30
  watch: score 30–60 AND rug_safe
  strong: score 60–80 AND rug_safe
  ape: >80 AND rug_safe AND smart_wallets_detected
