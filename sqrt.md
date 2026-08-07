Aug-1
**
Given a non-negative integer x, return the square root of x rounded down to the nearest integer. The returned integer should be non-negative as well.
**

# Code(implementation-1)

```cpp []
class Solution {
public:
    int mySqrt(int x) {
        int ans = 0;
        for(long long i = 0; i <= x; i++){
        if(x >= i*i){
            ans = i;
        }
        else{
            break;
            }
        }
        return ans;
    }
    
};
```
# Code(implementation-2)

```cpp []
class Solution {
public:
    int binSearch(int n){
        int s = 0;
        int e = n;
        long long int mid = s + (e-s)/2;
        long long int ans = -1;
        while(s<=e){
            long long int square = mid * mid;
            if(square == n)
            {
                return mid;
            } 
            if(square < n)
            {
                ans = mid;
                s = mid + 1;
            }
            else
            {
                e = mid - 1; 
            }
            mid = s + (e-s)/2;
        }
        return ans;
    }
    int mySqrt(int x) {
        return binSearch(x);
    }
    
};
```
