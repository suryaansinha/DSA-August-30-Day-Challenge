# Intuition

The goal is to push all `0`s to the end of the array while keeping the relative order of the non-zero elements unchanged. A brute-force way to think about this is: for every zero found, find the next non-zero element after it and swap them into place, so each zero effectively "bubbles" its way to the right.

# Approach

1. Use two nested loops:
   - Outer loop with index `i` scans through the array.
   - Inner loop with index `j` starts right after `i` and looks ahead for a non-zero element.
2. If `nums[i]` is `0` and `nums[j]` is non-zero, swap them — this moves the non-zero value into position `i` and pushes the zero further right.
3. Once a swap happens for a given `i`, break out of the inner loop since position `i` is now fixed with a non-zero value (or the search continues naturally if no such `j` exists).
4. Repeat until `i` reaches the end of the array — by then all zeros are shifted to the back in their original relative order, and non-zero elements retain their original relative order.

# Complexity

- **Time complexity:**
$$O(n^2)$$
Because of the nested loop, in the worst case (e.g., all zeros except the last element) each `i` scans ahead through most of the remaining array.

- **Space complexity:**
$$O(1)$$
The swaps are done in-place with no extra data structures.

# Code
```cpp
class Solution {
public:
    void moveZeroes(vector<int>& nums) {
    int n = nums.size();
    for(int i = 0; i < n; i++){
        for(int j = i+1; j < n; j++){
            if(nums[i] == 0 && nums[j] != 0){
                swap(nums[i], nums[j]);
                break;
            }
        }
    }
    }
};
```
