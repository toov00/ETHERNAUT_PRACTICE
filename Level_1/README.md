# Level 1: Fallback

Things are getting more interesting! Now, there's a full smart contract to work with, and the goal is to claim ownership by making `owner = msg.sender`.

There are a few places where ownership gets set: `constructor()`, `contribute()`, and a `receive()` fallback. Since the constructor only runs at deployment, that's off the table. That leaves `contribute()` and `receive()`.

The `contribute()` route is impractical as it requires `contributions[msg.sender] > contributions[owner]`, but the owner starts with 1000 ETH in contributions and each call is capped at 0.001 ETH. Way too many transactions!

The `receive()` fallback is the easier path. It only checks `msg.value > 0 && contributions[msg.sender] > 0` before handing over ownership. So the approach is simple: make a small contribution first, then send any amount of ETH directly to the contract to trigger `receive()` and claim ownership.
