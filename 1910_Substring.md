# Intuition

Since we need to remove every occurrence of `part` from `s`, including new occurrences that may form after a removal (because deleting a substring can bring previously separated characters together to form a new match), the simplest approach is to repeatedly search for `part` in `s` and erase it whenever found, continuing until no more matches remain.

# Approach

1. Loop with a `while` condition that continues as long as:
   - `s` is non-empty (`s.length() != 0`), and
   - `part` is still found somewhere within `s` (`s.find(part) < s.length()`, i.e., `find` didn't return `string::npos`).
2. On each iteration:
   - Locate the position of the first occurrence of `part` using `s.find(part)`.
   - Erase `part.length()` characters starting from that position using `s.erase(...)`.
3. Because erasing can cause characters before and after the removed part to become adjacent, this may create a brand-new match — the loop naturally handles this since it re-searches `s` from scratch on every iteration.
4. Once no more occurrences of `part` exist in `s`, the loop exits and the final string is returned.

# Complexity

- **Time complexity:**
$$O(n^2)$$
Each call to `find` and `erase` takes up to $$O(n)$$ time, and in the worst case (many overlapping/cascading removals) this process can repeat up to $$O(n)$$ times, giving a quadratic bound overall.

- **Space complexity:**
$$O(1)$$
The removal is done in-place on the string `s`, aside from the space needed for the string itself (no additional data structures are allocated).

# Code
```cpp
class Solution {
public:
    string removeOccurrences(string s, string part) {
        while(s.length() != 0 && s.find(part) < s.length()){
            s.erase(s.find(part), part.length());
        }
        return s;
    }
};
```
