# Intuition
<!-- Describe your first thoughts on how to solve this problem. -->
`nums1` has extra space at the end (size `m+n`) to hold the final merged result, with only the first `m` elements being valid. If we merge from the front, we'd overwrite elements in `nums1` that we still need to compare later. The key insight is to merge **from the back instead** — since the tail end of `nums1` is empty space, we can safely place the largest remaining elements there without destroying any data we haven't looked at yet.

# Approach
<!-- Describe your approach to solving the problem. -->
1. Use three pointers:
   - `i = m - 1` → last valid element in `nums1`
   - `j = n - 1` → last element in `nums2`
   - `k = m + n - 1` → last position in the merged `nums1`
2. Compare `nums1[i]` and `nums2[j]`, place the larger one at `nums1[k]`, then decrement the corresponding pointer(s) (`i` or `j`) and `k`.
3. Continue until either `i < 0` or `j < 0`.
4. If there are leftover elements in `nums2` (`j >= 0`), copy them into `nums1` — this handles the case where `nums2` has smaller elements than everything left in `nums1`.
5. No need for a similar leftover loop for `nums1`, since if `i >= 0` still, those elements are already in their correct sorted position at the front of the array.

**Example trace:** `nums1 = [1,2,3,0,0,0]`, `m=3`, `nums2 = [2,5,6]`, `n=3`

| Step | i | j | k | Comparison | Action | nums1 state |
|------|---|---|---|-----------|--------|--------------|
| start | 2 | 2 | 5 | `3 vs 6` | 6 wins → `nums1[5]=6` | `[1,2,3,0,0,6]` |
| | 2 | 1 | 4 | `3 vs 5` | 5 wins → `nums1[4]=5` | `[1,2,3,0,5,6]` |
| | 2 | 0 | 3 | `3 vs 2` | 3 wins → `nums1[3]=3` | `[1,2,3,3,5,6]` |
| | 1 | 0 | 2 | `2 vs 2` | else branch → `nums1[2]=2` | `[1,2,2,3,5,6]` |
| | 1 | -1 | 1 | `j<0`, loop ends | — | — |

Final result: `[1,2,2,3,5,6]` ✅

# Complexity
- Time complexity:
<!-- Add your time complexity here, e.g. $$O(n)$$ -->
$$O(m + n)$$ — each element from both arrays is visited and placed exactly once.

- Space complexity:
<!-- Add your space complexity here, e.g. $$O(n)$$ -->
$$O(1)$$ — merging is done in-place within `nums1`, using only a constant number of extra pointer variables.

# Code
```cpp []
class Solution {
public:
    void merge(vector<int> &nums1, int m, vector<int> &nums2, int n) {
        int i = m - 1;
        int j = n - 1;
        int k = m + n - 1;

        while (i >= 0 && j >= 0) {
            if (nums1[i] > nums2[j]) nums1[k--] = nums1[i--];
            else nums1[k--] = nums2[j--];
        }
        while (j >= 0) nums1[k--] = nums2[j--];
    }
};
```
