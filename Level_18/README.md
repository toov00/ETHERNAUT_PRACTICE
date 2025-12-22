# Level 18: Alien Codex

This level deals with storage slot collisions (again!) combined with an integer underflow vulnerability.

The codex array has a `retract()` function that decrements its length without bounds checking. By calling it on an empty array, the length underflows, effectively giving the array access to the entire storage space.

Since dynamic array elements are stored starting at `keccak256(slot)`, and storage slots wrap around, we can calculate an index that points back to slot 0, which is where the owner variable lives. Writing to that index lets us overwrite the owner and claim the contract. But here, it is important to note that the array elements start at `keccak256(1)`, since the codex array's length is stored at slot 1. Slot 0 is occupied by other variables.

And, finding slot 0 isn't thaaaat straightforward. Logically, slot 0 refers to the last slot in codex (since there's a wraparound, and codex begins from slot 0), so this boils down to a modulus math problem! 
