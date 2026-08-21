# Intuition

Reversing a string in-place can be done by swapping characters from the outside in — the first character swaps with the last, the second with the second-last, and so on, until the two pointers meet in the middle.

# Approach

1. Initialize two pointers: `start` at index `0` and `end` at the last index (`s.size() - 1`).
2. Loop while `start < end`:
   - Swap the characters at `s[start]` and `s[end]`.
   - Increment `start` and decrement `end` after the swap (done inline via `start++` and `end--`).
3. The loop naturally stops once the pointers meet or cross, meaning the entire string has been reversed in-place.

# Complexity

- **Time complexity:**
$$O(n)$$
Each character is visited once as the two pointers move toward each other.

- **Space complexity:**
$$O(1)$$
The reversal is done in-place using only two extra integer variables, with no additional data structures.

# Code
```cpp
class Solution {
public:
    void reverseString(vector<char>& s) {
        int start = 0;
        int end = s.size() - 1;
        while(start < end){
            swap(s[start++], s[end--]);
        }
    }
};
```
