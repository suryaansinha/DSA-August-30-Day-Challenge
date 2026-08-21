# Intuition

A peak element is one that's strictly greater than its neighbors. The simplest way to check this is to look at each element and verify it's greater than (or at the boundary of) the elements on both its left and right sides. Since boundaries (first and last elements) only have one neighbor, they should be treated as automatically satisfying the missing side.

# Approach

1. Loop through the array with index `i` from `0` to `n-1`.
2. For each element, check two conditions:
   - `leftOk`: true if `i` is the first index (`i == 0`), or the current element is greater than the element before it (`nums[i] > nums[i-1]`).
   - `rightOk`: true if `i` is the last index (`i == n-1`), or the current element is greater than the element after it (`nums[i] > nums[i+1]`).
3. If both `leftOk` and `rightOk` are true, `nums[i]` is a peak — return its index `i` immediately.
4. If no peak is found after scanning the whole array (which shouldn't happen given the problem guarantees at least one peak exists), return `-1` as a fallback.

# Complexity

- **Time complexity:**
$$O(n)$$
The array is scanned once, checking each element in constant time.

- **Space complexity:**
$$O(1)$$
Only a few boolean/integer variables are used, no extra data structures.

# Code
```cpp
class Solution {
public:
    int findPeakElement(vector<int>& nums) {
        int n = nums.size();
        for (int i = 0; i < n; i++) {
        bool leftOk  = (i == 0 || nums[i] > nums[i-1]);
        bool rightOk = (i == n-1 || nums[i] > nums[i+1]);
        if (leftOk && rightOk) return i;
    }
    return -1;
    }
};
```

*Note: this linear scan runs in* $$O(n)$$ *time. LeetCode's problem statement requires an* $$O(\log n)$$ *solution, which can be achieved with binary search by comparing `nums[mid]` with `nums[mid+1]` and moving toward the side with the larger neighbor.*
