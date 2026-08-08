# Intuition
Since letters is already sorted, a linear scan to find the first character greater than target would work but takes O(n) time. Whenever you're searching a sorted array for a threshold-crossing point (the first element satisfying some condition), that's a strong signal to reach for binary search instead — it narrows the search space by half each time rather than checking every element.

# Approach
Actually the letters here are alphabetic characters ('a'–'z'), so subtracting '0' doesn't map them meaningfully. Looking at your code, it does int t = target - '0' and int y = letters[mid] - '0' — this only produces a consistent relative ordering if all values are compared the same way, so the comparison y > t still works correctly as a proxy for letters[mid] > target, even though the individual offsets aren't meaningful digit values. It's a bit unconventional to subtract '0' for letters, but since both sides get the same offset subtracted, the relative comparison remains valid.

The core logic:

- Binary search over the sorted array with s = 0, e = size - 1.
- At each step, compute mid and compare letters[mid] to target.
- If letters[mid] > target: this is a candidate answer — record it in ans, then search the left half (e = mid - 1) to see if there's an even smaller qualifying letter.
- If letters[mid] <= target: this letter doesn't qualify, so search the right half (s = mid + 1).
- After the loop, if no letter greater than target was found (ans is empty), wrap around and return letters[0] (the smallest letter in the array) — since the problem guarantees circular behavior.

# Complexity
- Time complexity:
$$O(\log n)$$ — binary search halves the search space each iteration.

- Space complexity:
$$O(1)$$ — only a few extra variables (s, e, mid, ans) are used; no extra data structures proportional to input size.

# Code
```cpp []
class Solution {
public:
    char nextGreatestLetter(vector<char>& letters, char target) {
        int t = target - '0';
        
        int s = 0;
        int e = letters.size() - 1;
        string ans = "";
        while(s <= e){
            int mid = s + (e-s)/2;
            int y = letters[mid] - '0';
            if(y > t){
                ans = letters[mid];
                e = mid - 1;
            }
            else{
                s = mid + 1;
            }
            
        }
        if(ans.size()>0)
        {
            return ans[0];
        }
        
        return letters[0];
        
    }
};
```
