# Intuition
Since the array is sorted, we don't need to check every element one by one. We can repeatedly cut the search space in half by comparing the middle element to the target — if the middle element is too small, the target must be in the right half; if it's too large, the target must be in the left half.

# Approach
1. Maintain two pointers, `s` (start) and `e` (end), covering the current search range.
2. While `s <= e`:
   - Compute `mid` as `s + (e - s) / 2` (avoids overflow compared to `(s + e) / 2`).
   - If `nums[mid] == target`, return `mid` immediately.
   - If `nums[mid] < target`, the target must lie to the right, so move `s = mid + 1`.
   - Otherwise, the target must lie to the left, so move `e = mid - 1`.
3. If the loop ends without finding the target, return `-1` (stored in `ans`).

# Complexity
- **Time complexity:** $$O(\log n)$$
  Each iteration halves the search space.

- **Space complexity:** $$O(1)$$
  Only a few extra integer variables are used, regardless of input size.

# Code
```cpp
class Solution {
public:
    int search(vector<int>& nums, int target) {
        int s = 0;
        int e = nums.size() - 1;
        int ans = -1;
        while (s <= e) {
            int mid = s + (e - s) / 2;
            if (nums[mid] == target) {
                return mid;
            }
            else if (nums[mid] < target) {
                s = mid + 1;
            }
            else {
                e = mid - 1;
            }
        }
        return ans;
    }
};
```

** Date ** => 2 Aug
