# Intuition
A mountain array strictly increases then strictly decreases. At any index mid, comparing it to its next neighbor tells you which "slope" you're on:

- If arr[mid] < arr[mid+1], you're still climbing the increasing side, so the peak lies somewhere to the right (mid+1 or beyond).
- Otherwise, you're on the decreasing side (or at the peak itself), so the peak is at mid or to the left.

This gives a clean binary search condition — no need to scan linearly.

# Approach
1. Set s = 0, e = arr.size() - 1.
2. While s < e:
  - Compute mid = s + (e - s) / 2.
  - If arr[mid] < arr[mid+1]: the array is still increasing at mid, so the peak can't be at mid — move left boundary to s = mid + 1.
  - Else (arr[mid] >= arr[mid+1]): we're past or at the peak, so shrink the right boundary to e = mid (keep mid as a candidate).
3. Loop ends when s == e, which converges exactly on the peak index, since each iteration discards half the array while always keeping the peak within [s, e].
4. Return s (or equivalently e).

This works because the array's structure guarantees a single peak, so the comparison arr[mid] vs arr[mid+1] always correctly tells you which half to discard — the same invariant used in standard binary search, just adapted to a monotonic "slope direction" property instead of an exact target value.

# Complexity
- Time complexity:
$$O(\log n)$$ — the search space halves each iteration.

- Space complexity:
$$O(1)$$ — only a few pointer variables are used, no extra data structures.

# Code
```cpp []
class Solution {
public:
    int peakIndexInMountainArray(vector<int>& arr) {
        int s = 0;
        int e = arr.size() - 1;
        int mid = s + (e-s)/2;
        while(s<e){
            if(arr[mid]<arr[mid+1]){
                s = mid + 1;
            }
            else{e = mid;}

            mid = s + (e-s)/2;
        }
        return s;
    }
};
```
