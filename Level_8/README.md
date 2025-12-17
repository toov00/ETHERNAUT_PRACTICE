# Level 8: Vault

Fun one! Finally got to apply storage layout knowledge in practice.

At first it seemed impossible as the `unlock()` function requires the correct password, but password is a private variable with no getter. BUT, "private" in Solidity only means other contracts can't read it directly. The data is still stored on-chain and publicly accessible.

The solution is, therefore, to read the raw storage. Since locked (a bool) is in slot 0 and password (a bytes32) is in slot 1, issuing the following command would give the password in hex, which I passed to `unlock()`. Done! 

```
await web3.eth.getStorageAt(contract.address, 1);
```

The takeaway: never store sensitive data on-chain, even in private variables. Everything on the blockchain is readable.
 
