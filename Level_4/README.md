# Level 4: Telephone

Simple! After solving Level 3, this felt like a breeze. The goal is to call `changeOwner()` where `tx.origin == msg.sender`.

I learned something new here: tx.origin refers to the original externally owned account (EOA) that initiated the transaction, while msg.sender is the immediate caller. So if I call the provided contract's instance, which then calls `changeOwner()`, the tx.origin stays as my address but msg.sender becomes the provided contract, effectively bypassing the check.

The takeaway: don't use tx.origin for authentication. It's vulnerable to exactly this kind of proxy attack.

