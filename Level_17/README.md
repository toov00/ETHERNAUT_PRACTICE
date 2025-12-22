# Level 17: Magic Number

This level was really difficult for me as I am not familiar with the underlying concepts, i.e., Solidity opcodes and writing contracts directly in bytecode. The challenge requires writing a contract in raw bytecode that returns the number "42", then passing its address to the `setSolver()` function.

I had to carefully trace through different opcodes to understand what was needed. One important distinction is between initialization and runtime bytecode. The initialization code runs during contract deployment and is responsible for copying the runtime code into memory and returning it to the EVM. The runtime code is what actually executes when the contract is called afterward. Additionally, deploying bytecode via `web3.eth.sendTransaction` with a receiver address of 0x0 triggers contract creation.
