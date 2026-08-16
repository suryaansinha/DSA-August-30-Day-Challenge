# Intuition
<!-- Describe your first thoughts on how to solve this problem. -->
Rotating the array to the right by `k` steps means every element moves `k` positions ahead, wrapping around to the start once it goes past the end of the array. So the element currently at index `i` should end up at index `(i + k) % n` in the final array. Since we're placing elements out of order (not sequentially), we can't safely overwrite `nums` in place while reading from it — we'd risk overwriting a value before we've had a chance to move it. So we first take a copy of the original array, then place each element into its correct final position using modular arithmetic to handle the wraparound.

# Approach
<!-- Describe your approach to solving the problem. -->
1. Get `n`, the size of `nums`.
2. Create a copy `nums2` of the original array — this preserves the original values before we start overwriting `nums`.
3. Loop through each index `i` from `0` to `n-1`:
   - Compute the target index `(i + k) % n` — the `% n` handles wraparound when `i + k` exceeds the array bounds.
   - Place `nums2[i]` at `nums[(i + k) % n]`.
4. After the loop, `nums` holds the fully rotated array (modified in place via reference).

**Example trace:** `nums = [1,2,3,4,5,6,7]`, `k = 3`, `n = 7`

| i | nums2[i] | target = (i+k)%n | nums after placement |
|---|----------|-------------------|------------------------|
| 0 | 1 | 3 | `[_,_,_,1,_,_,_]` |
| 1 | 2 | 4 | `[_,_,_,1,2,_,_]` |
| 2 | 3 | 5 | `[_,_,_,1,2,3,_]` |
| 3 | 4 | 6 | `[_,_,_,1,2,3,4]` |
| 4 | 5 | 0 | `[5,_,_,1,2,3,4]` |
| 5 | 6 | 1 | `[5,6,_,1,2,3,4]` |
| 6 | 7 | 2 | `[5,6,7,1,2,3,4]` |

Final result: `[5,6,7,1,2,3,4]` ✅

# Complexity
- Time complexity:
<!-- Add your time complexity here, e.g. $$O(n)$$ -->
$$O(n)$$ — one pass to copy the array, one pass to place each element into its rotated position.

- Space complexity:
<!-- Add your space complexity here, e.g. $$O(n)$$ -->
$$O(n)$$ — the extra `nums2` array used to hold a copy of the original values.

# Code
```cpp []
class Solution {
public:
    void rotate(vector<int>& nums, int k) {
        int n = nums.size();
        vector<int> nums2(nums);
        for (int i = 0; i < n; i++) {
            nums[(i + k) % n] = nums2[i];
        }
    }
};
```
