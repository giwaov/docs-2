# Clarity Language Tips and Best Practices

## Overview

Clarity is the smart contract language for the Stacks blockchain. Unlike most smart contract languages, Clarity is decidable.

## Key Language Features

### 1. No Reentrancy By Design

Clarity prevents reentrancy attacks at the language level with no dynamic dispatch and clear analyzable call graphs.

### 2. Safe Arithmetic

All arithmetic operations are checked for overflow.

### 3. Response Types

`clarity
(define-public (transfer (amount uint) (to principal))
  (begin
    (asserts! (> amount u0) (err u100))
    (asserts! (not (is-eq tx-sender to)) (err u101))
    (ft-transfer? my-token amount tx-sender to)
  )
)
`

## Common Patterns

### Map with Default Values

`clarity
(define-map balances principal uint)

(define-read-only (get-balance (account principal))
  (default-to u0 (map-get? balances account))
)
`

### Iterating with Fold

`clarity
(define-private (sum-reducer (item uint) (acc uint))
  (+ item acc)
)

(define-read-only (sum-list (items (list 100 uint)))
  (fold sum-reducer items u0)
)
`

### Time-Based Logic

`clarity
(define-data-var unlock-height uint u0)

(define-public (lock-tokens (amount uint) (lock-blocks uint))
  (begin
    (var-set unlock-height (+ block-height lock-blocks))
    (ok true)
  )
)
`

## Testing with Clarinet

Use clarinet test for unit tests and clarinet check for static analysis.
