# Level 7: Force

This one was surprising as the contract is completely empty! The higher difficulty rating had me worried, but the solution turned out to be quite elegant.

The goal here isn't to obtain control, but rather, to get ETH into a contract that has no `receive()`, no `fallback()`, and no payable functions. Direct transfers via the console just revert.

The trick is `selfdestruct`. When a contract self-destructs, it forcibly sends its remaining ETH to a specified address—and the target has no way to refuse it. No payable functions required.

So the solution is to deploy a simple contract with some ETH, then call `selfdestruct(targetAddress)`. Even though `selfdestruct` is deprecated (it no longer deletes contract code post-Dencun), it still exists and can still forcibly transfer ETH.

All in all, lesson learnt: a contract can never truly reject all incoming ETH. `selfdestruct` bypasses all the usual checks.
