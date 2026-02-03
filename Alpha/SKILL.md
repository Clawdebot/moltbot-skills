name: alpha-hunter
description: >
  AI-powered crypto alpha scanner that detects early memecoins before pumps
  using wallet flow, volume spikes, social mentions, and smart money tracking.

inputs:
  chain:
    type: string
    enum: [eth, base, sol]
    description: Blockchain to scan

  risk:
    type: string
    enum: [safe, degen]
    description: Risk tolerance for token discovery

  max_tokens:
    type: number
    description: How many alpha candidates to return

outputs:
  tokens:
    type: list
    items:
      name:
        type: string
      contract:
        type: string
      confidence:
        type: number
      signals:
        type: list
        
