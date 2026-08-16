# Intuition
<!-- Describe your first thoughts on how to solve this problem. -->
Without `+` or `-`, we need to reconstruct addition using bitwise operations. Thinking about how addition works bit by bit: `a XOR b` gives the sum of each bit *ignoring carry* (1+0=1, 0+0=0, 1+1=0 — matches XOR exactly), and `a AND b` tells us exactly which bit positions generate a carry (only 1+1 produces one). That carry needs to be added one position to the left, so we shift it: `(a AND b) << 1`. Repeating this process between the running sum and the new carry, until the carry becomes 0, gives the final sum.

# Approach
<!-- Describe your approach to solving the problem. -->
1. While `b` (the carry) is non-zero:
   - Compute `carry = (a & b) << 1` — the bits where both `a` and `b` are 1, shifted left by one position.
   - Compute `a = a ^ b` — the sum of `a` and `b` ignoring carry.
   - Set `b = carry` — the carry becomes the new value to add in the next iteration.
2. Once `b == 0`, `a` holds the final sum, so return it.
3. **C++ caveat:** shifting a signed int left can trigger undefined behavior on overflow, so cast to `unsigned int` before shifting to keep the wraparound well-defined.
4. Negative numbers work correctly without special-casing, since two's complement bit patterns behave the same under XOR/AND/shift regardless of sign — the carry simply shifts entirely out of the 32-bit register when the loop terminates (e.g. for `-1 + 1`).

**Example trace:** `a = 3 (011)`, `b = 5 (101)`

| Step | a | b | a^b | (a&b)<<1 |
|------|-----|-----|-----|----------|
| 1 | 011 | 101 | 110 | 010 |
| 2 | 110 | 010 | 100 | 100 |
| 3 | 100 | 100 | 000 | 1000 |
| 4 | 000 |1000 |1000 | 0000 |

`b` becomes 0 → return `a = 1000 = 8` ✅ (3 + 5 = 8)

# Complexity
- Time complexity:
<!-- Add your time complexity here, e.g. $$O(n)$$ -->
$$O(\log(\max(|a|,|b|)))$$, effectively $$O(32)$$ for 32-bit integers, since the carry shifts one bit left each iteration and eventually vanishes.

- Space complexity:
<!-- Add your space complexity here, e.g. $$O(n)$$ -->
$$O(1)$$ — only a constant number of extra variables are used.

# Code
```cpp []
class Solution {
public:
    int getSum(int a, int b) {
        while (b != 0) {
            unsigned int carry = ((unsigned int)a & (unsigned int)b) << 1;
            a = a ^ b;
            b = (int)carry;
        }
        return a;
    }
};
```
