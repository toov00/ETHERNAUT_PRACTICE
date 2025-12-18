# Level 10: Re-entrancy

The first Solidity bug I read about! Excited to explore it further!

It is important to understand that the `receive()` function of a contract, if present, is automatically called whenever ETH is sent to it. This enables recursive withdrawals: when the victim's `withdraw()` sends ETH, it triggers the attacker's `receive()`, which can call `withdraw()` again before the balance is updated.

So, the takeaway is to always update state before making external calls. Follow the Checks-Effects-Interactions pattern!

Side Notes:

1. As I'm using the Remix IDE, and am deploying the attacking contract with some value, I need to include a payable constructor:

```
contract B {
    constructor() payable {}
}
```

It tells the compiler that this contract accepts ETh during deployment.
