# Stacks DeFi Ecosystem Overview

## Introduction

The Stacks blockchain enables DeFi applications secured by Bitcoin. This document provides an overview of the major DeFi protocols and patterns in the Stacks ecosystem.

## Key DeFi Protocols

### Arkadiko (USDA Stablecoin)
- **Type**: CDP-based stablecoin protocol
- **Token**: DIKO (governance), USDA (stablecoin)
- **Mechanism**: Over-collateralized vaults backed by STX

### ALEX (DEX and Launchpad)
- **Type**: Decentralized exchange and launchpad
- **Token**: ALEX
- **Features**: AMM, yield farming, order book, IDO launchpad

### Velar (DEX)
- **Type**: Multi-functional DEX
- **Features**: Spot trading, perpetual futures, token launchpad

### StackingDAO
- **Type**: Liquid stacking protocol
- **Token**: stSTX (liquid stacking derivative)

## Common DeFi Patterns on Stacks

### Automated Market Maker (AMM)

`clarity
(define-public (swap-x-for-y (dx uint))
  (let (
    (x (var-get reserve-x))
    (y (var-get reserve-y))
    (dy (/ (* dx y) (+ x dx)))
  )
    (try! (contract-call? .token-x transfer dx tx-sender (as-contract tx-sender) none))
    (try! (as-contract (contract-call? .token-y transfer dy tx-sender tx-sender none)))
    (var-set reserve-x (+ x dx))
    (var-set reserve-y (- y dy))
    (ok dy)
  )
)
`

## Building on Stacks DeFi

1. Install Clarinet
2. Create project: clarinet new my-defi-app
3. Add contracts: clarinet contract new my-token
4. Test locally: clarinet test
5. Deploy: clarinet deployments apply
