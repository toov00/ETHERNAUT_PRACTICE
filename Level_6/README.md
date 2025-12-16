# Level 6: Delegate

A new vulnerability pattern: delegate call exploitation! I have seen this before but never explored it. There are a few layers to unpack.

First, the `fallback()` function. It is not a regular function, but a special handler that executes when a call doesn't match any function signature. In this contract, the fallback triggers a `delegatecall` to the Delegate contract.

The key insight: `delegatecall` executes the target's code but in the caller's storage context. So when Delegate's `pwn()` sets owner = msg.sender, it writes to slot 0. BUT, since we're in Delegation's context, that's Delegation's owner slot, not Delegate's.

To exploit this, I needed to trigger `fallback()` with the function selector for `pwn()`. I did it straight from the console:

```
// Get the function selector for pwn()
web3.utils.keccak256("pwn()").slice(0, 10)
// '0xdd365b8b'

// Send transaction with pwn() selector as data
await web3.eth.sendTransaction({
  from: player,
  to: contract.address,
  data: "0xdd365b8b"
})

```

Since no function in Delegation matches 0xdd365b8b, it falls through to `fallback()`, which delegatecalls to Delegate with that data. Delegate interprets it as a call to `pwn()`, and ownership is mine.
