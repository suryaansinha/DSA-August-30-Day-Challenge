# Intuition

Rotating the array to the right by `k` steps means every element needs to move to a new index that is `k` positions ahead, wrapping around to the start once it goes past the end. If we know each element's final position in advance, we can directly place it there — as long as we work from a copy of the original array so we don't overwrite values before we've read them.

# Approach

1. Make a copy of the original array (`nums2`) so the source values stay intact while we overwrite `nums`.
2. Loop through the copy with index `i` from `0` to `n-1`.
3. For each element, compute its new position using `(i + k) % n` — the modulo handles the wrap-around when `i + k` exceeds the array length.
4. Assign `nums2[i]` to `nums[(i+k) % n]`, effectively placing every element at its correct rotated position in a single pass.

# Complexity

- **Time complexity:**
$$O(n)$$
We iterate through the array once, doing constant-time work per element.

- **Space complexity:**
$$O(n)$$
An extra array (`nums2`) of the same size as `nums` is used to hold the original values.

# Code
```cpp
class Solution {
public:
    void rotate(vector<int>& nums, int k) {
        int n = nums.size();
        vector<int> nums2(nums);
        for(int i = 0; i < n; i++){
        nums[(i+k)%n] = nums2[i];
        }
    }
};
```
