# Intuition

Roman numerals are built from fixed symbol groups for each decimal place (ones, tens, hundreds, thousands). Since a number can have at most 4 digits (1 ≤ num ≤ 3999), each digit maps independently to a small set of precomputed strings — so instead of computing symbols digit-by-digit with conditionals, we can just look them up in arrays indexed by digit value (0–9).

# Approach

1. Precompute 4 lookup arrays, one for each place value:
   - `ones[]` for 1s (I, II, III, IV, V, VI, VII, VIII, IX)
   - `tens[]` for 10s (X, XX, ... XC)
   - `hndrds[]` for 100s (C, CC, ... CM)
   - `thsnds[]` for 1000s (M, MM, MMM)
2. Each array is indexed 0–9, where index 0 is an empty string (that place contributes nothing).
3. Extract each digit of `num` using integer division and modulo:
   - Thousands digit: `num / 1000`
   - Hundreds digit: `(num % 1000) / 100`
   - Tens digit: `(num % 100) / 10`
   - Ones digit: `num % 10`
4. Concatenate the corresponding strings from each array to get the final Roman numeral.

# Complexity

- **Time complexity:**
$$O(1)$$
Since `num` is bounded (≤ 3999), the number of digits and lookups is constant.

- **Space complexity:**
$$O(1)$$
The lookup tables have fixed, constant size regardless of input.

# Code
```cpp
class Solution {
public:
    string intToRoman(int num) {
        //0,1,2,3,4,5,6,7,8,9
        string ones[] = {"","I","II","III","IV","V","VI","VII","VIII","IX"};

        //0,10,20,30,40,50,60,70,80,90
        string tens[] = {"","X","XX","XXX","XL","L","LX","LXX","LXXX","XC"};

        //0,100,200,300,400,500,600,700,800,900
        string hndrds[] = {"","C","CC","CCC","CD","D","DC","DCC","DCCC","CM"};

        //0,1000,2000,3000
        string thsnds[] = {"","M","MM","MMM"};

        return thsnds[num/1000] + hndrds[(num%1000)/100] + tens[(num%100)/10] + ones[num%10];
    }
};
```
