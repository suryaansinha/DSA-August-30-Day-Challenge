# Intuition

A rotated sorted array still contains a sorted half around `mid`, so we can use a modified binary search.

The main difference from **Search in Rotated Sorted Array (LC 33)** is the presence of **duplicates**.

If:

`nums[start] == nums[mid] == nums[end]`

then we cannot determine which half is sorted because both sides look identical. In this case, we safely shrink the search space by moving `start` forward and `end` backward.

Once the duplicates are handled, we can determine which half is sorted and continue with normal binary-search logic.

# Approach

1. Maintain two pointers:
   - `start` at the beginning of the search space.
   - `end` at the end of the search space.

2. Calculate `mid`.

3. If `nums[mid] == target`, return `true`.

4. If:
   ```cpp
   nums[start] == nums[mid] && nums[mid] == nums[end]
# Complexity
- Time complexity:
    O(log n) in the average/best case, but O(n) in the worst case due to duplicates.

- Space complexity:
    O(1)

# Code
```cpp []
class Solution {
public:
    bool search(vector<int>& nums, int target) {
        int start = 0;
        int end = nums.size() - 1;
        while(start <= end){
            while(start < end && nums[start] == nums[start + 1]){
                start++;
            }
            while(start < end && nums[end] == nums[end -1]){
                end--;
            }
            int mid = start + (end-start)/2;
            if(nums[mid] == target){
                return true;
            }
            else if(nums[mid] >= nums[start]){
                if(nums[mid]>=target && target>=nums[start]) {end = mid - 1;}
                else {start = mid + 1;}
            }
            else{
                if(nums[mid] <= target && nums[end] >= target) {start = mid + 1;}
                else{end = mid - 1;}
            }
        }
        return false;
    }
};
```
