# Level 9: King

The most difficult one so far! The goal is to become king and prevent anyone (including Ethernaut) from reclaiming kingship.

How the King contract works:

1. Send more Ether than the current prize , and you become the new king
2. The contract then pays the previous king via payable(king).transfer(msg.value)

The vulnerability, of which I had some trouble finding, is in `transfer()`! Specifically, `transfer()` reverts if the recipient can't accept Ether. So if I become king using a contract without a `receive()` or `fallback()` function, any attempt to dethrone me will fail as the payment to my contract reverts, which reverts the entire transaction.

Takeaway: Never assume Ether transfers will succeed. Use pull payments instead of push payments to avoid denial-of-service vulnerabilities.
