
# Code
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
