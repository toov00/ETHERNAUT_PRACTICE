# Level 21: Dex 

The vulnerability lies in price manipulation through a flawed calculation of token prices. The calculation is done based on current token reserves, and not some constant product formula like with Uniswap! The user (me!) is, thus able to get more and more tokens by taking advantage of the differing ratios through alternating swaps, ultimately leading to the drainage of a particular token! 

Side Note:

1. There isn't any slippage protection via `require(swapAmount >= minAmountOut, "Slippage too high!");`, which should typically be in place in case of secure, proper DEX.
