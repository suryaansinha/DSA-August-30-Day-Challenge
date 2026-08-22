# Intuition

A palindrome reads the same forwards and backwards, but here we only care about alphanumeric characters and should ignore case. So the idea is to compare characters from both ends of the string moving inward, skipping over anything that isn't a letter or digit, and treating uppercase and lowercase letters as equal.

# Approach

1. Use two pointers, `st` starting at the beginning and `e` starting at the end of the string.
2. In each iteration of the main loop:
   - Advance `st` forward while it points to a non-alphanumeric character (using the `validCharacter` helper).
   - Move `e` backward while it points to a non-alphanumeric character.
3. Once both pointers land on valid characters, compare them after normalizing case with `toLowerCase` (which converts uppercase letters to lowercase and leaves other characters unchanged).
4. If the normalized characters don't match, the string isn't a palindrome — return `false` immediately.
5. Otherwise, move `st` forward and `e` backward, and repeat until `st` crosses `e`.
6. If the loop completes without finding a mismatch, the string is a valid palindrome — return `true`.

# Complexity

- **Time complexity:**
$$O(n)$$
Each character is visited at most once as the two pointers move toward each other and skip invalid characters.

- **Space complexity:**
$$O(1)$$
Only a constant number of extra variables (`st`, `e`) are used; no additional data structures are created.

# Code
```cpp
class Solution {
public:
    char toLowerCase(char ch) {
        if (ch >= 'a' && ch <= 'z') {
            return ch;
        } else {
            ch = ch - 'A' + 'a';
            return ch;
        }
    }
    bool validCharacter(char ch){
        return ((ch>='a' && ch<='z')||(ch>='0' && ch<='9')||(ch>='A' && ch<='Z'));
    }
    bool isPalindrome(string s) {
        int st = 0;
        int e = s.size() - 1;
        while(st <= e){
            while(st<e && !validCharacter(s[st])){
                st++;
            }
            while(st<e && !validCharacter(s[e])){
                e--;
            }

            if(toLowerCase(s[st]) != toLowerCase(s[e])){
                return false;
            }
            st++;
            e--;
        }
        return true;
    }
};
```
