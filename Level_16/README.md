# Level 16: Preservation

Tricky! The exploit works in two stages, both using the original contract's `setFirstTime()` function. The first call overwrites timeZone1Library (slot 0) with my attacking contract's address, and this happens because the legitimate library's `setTime()` writes to slot 0, and `delegatecall` means it writes to Preservation's storage, not its own. The second call then routes the `delegatecall` to my malicious contract instead, allowing me to overwrite the owner variable directly.

Other things to note:

1. When `delegatecall` is used, `msg.sender` and `msg.value` remain unchanged from the original call, storage operations affect the calling contract rather than the called contract, and this still refers to the calling contract. Essentially, you're borrowing someone else's code to run against your own state.
