# Level 23: Puzzle Wallet

Back to proxy vulnerabilities! This one has a pretty high level of difficulty as it involves many different steps and considerations. 

Things to know:
1. Upgradeable Proxies: Allows for the target contract to be updated, simply by updating the address in the proxy contract (specificially, the storage that holds the target contract's address).
2. Multicalls: Allows for the bundling of multiple function calls into a single transaction, leading to a reduction in gas fees. This also ensures sequential execution of the calls, thus preventing stale data / operations.
