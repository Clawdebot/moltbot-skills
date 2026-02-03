name: rug-detector
description: >
  AI-powered rug pull detection system that analyzes smart contract risk,
  liquidity safety, insider wallets, and deployer behavior.

inputs:
  token:
    type: string
    description: Token contract address

  chain:
    type: string
    enum: [eth, base, sol]
    description: Blockchain of the token

outputs:
  risk_score:
    type: number
    description: 0–100, higher = more dangerous

  verdict:
    type: string
    enum: [safe, warning, scam]

  reasons:
    type: list
