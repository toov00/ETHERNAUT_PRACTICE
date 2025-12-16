# Level 3: Coin Flip

A step up from the previous levels! The goal is to win `flip()` 10 times consecutively. It seems impossible, but the "randomness" is just based on the block hash.

The solution is simply to deploy a contract that replicates the flip logic from the original contract. By calculating the result beforehand, I can call `flip()` with the correct guess every time. On-chain randomness isn't really random when the inputs are publicly visible.
