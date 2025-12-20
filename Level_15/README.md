# Level 15: Naught Coin

Seems more like a level 4 difficulty than a level 3! Perhaps because I'm not familiar with ERC20 and its implementations. There are many things to take note of here.

The key vulnerability is that the `lockTokens` modifier only restricts `transfer()`, but ERC20 tokens have another way to move tokens, i.e., `transferFrom()`. Since this function isn't overridden, it has no timelock.

To exploit this, I first created and deployed an external contract that calls `transferFrom()` on the NaughtCoin contract. Using `transfer()` wouldn't work because it moves tokens from msg.sender, and the attack contract has no tokens. `transferFrom()` lets me specify the player address as the source.

Before calling the attack, I needed to approve the attack contract's address from the Ethernaut console. This is a security feature of ERC20, in which `approve()` grants permission for another address to spend your tokens. Without this step, `transferFrom()` reverts.

Other things to note:
1. `tx.origin` refers to the original transaction initiator (the player), while `msg.sender` is the immediate caller (the attack contract)
2. `approve()` sets who can spend your tokens, not who receives them! The recipient is specified in the `transferFrom()` call itself
