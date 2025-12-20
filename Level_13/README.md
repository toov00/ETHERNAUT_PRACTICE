# Level 13: Gatekeeper One

The most complex challenge so far! Three gates must be passed to register as an entrant.

The first gate requires `msg.sender != tx.origin`, which is straightforward as calling through an attacker contract satisfies this automatically.

The second gate is trickier, as it requires `gasleft() % 8191 == 0`. The remaining gas at the exact moment of the check must be divisible by 8191. Since the precise gas consumed before this check depends on compiler version and other factors, the simplest approach is brute-forcing, i.e., trying different gas values until one works. 

The third gate requires constructing a bytes8 key that satisfies three type-conversion conditions. The solution is to apply a bitmask to your address: `bytes8(uint64(uint160(tx.origin))) & 0xFFFFFFFF0000FFFF`. This mask zeros out bits 16-31 (satisfying the first condition), preserves the upper bits (satisfying the second), and keeps the lower 16 bits from your address (satisfying the third).

Key insight: Use low-level `.call()` instead of the contract's `enter()` function directly. Since the brute-force approach involves many failed attempts, a high-level call would revert the entire transaction on the first failure. Using `.call()` returns false on failure instead, allowing the loop to continue until a successful gas value is found.
