# Level 11: Elevator

A straightforward challenge that feels more like a general programming exploit than something specific to smart contracts. The solution is to deploy an attacker contract that implements the Building interface, with `isLastFloor()` returning different values on consecutive calls to force top to become true.
