name: alpha-hunter

description: >
  Discovers early crypto alpha by combining smart money behavior,
  liquidity growth, deployer patterns, and social acceleration —
  while filtering out scams using Rug Detector and Wallet Intelligence.

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
    description: Tokens filtered out due to rug risk or weak wallet behavior

logic:
  steps:
    - Scan new token deployments and liquidity additions
    - Track deployer wallets and early funding sources
    - Detect clusters of early buyers
    - Call Rug Detector for each token
    - Reject tokens with risk_score > 50 or rug_type != "safe"
    - For remaining tokens, call Wallet Intelligence on early buyers
    - Reject tokens where average wallet_score < 70
    - Measure liquidity growth, volume acceleration, and holder increase
    - Rank tokens using weighted alpha score

alpha_factors:
  smart_money_score: 0.30
  liquidity_growth: 0.20
  rug_safety: 0.20
  deployer_reputation: 0.10
  social_velocity: 0.10
  holder_growth: 0.10

thresholds:
  ignore: rug OR wallet_score < 70 OR score < 30
  watch: score 30–60 AND rug_safe AND wallet_score >= 70
  strong: score 60–80 AND rug_safe AND wallet_score >= 80
  ape: >80 AND rug_safe AND wallet_score >= 85
  
