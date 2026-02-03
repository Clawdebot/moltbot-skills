name: alpha-hunter
description: >
  Discovers early crypto opportunities by combining
  social trends, smart money flows, and rug risk analysis.

inputs:
  chain:
    type: string
    enum: [eth, base, sol]

  risk:
    type: string
    enum: [safe, degen]

outputs:
  tokens:
    type: list
    description: Ranked alpha candidates

  signals:
    type: list
    description: Why these tokens were selected

  confidence:
    type: number
    description: 0–100 confidence score for the list
    
