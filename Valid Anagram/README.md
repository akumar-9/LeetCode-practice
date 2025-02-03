# Valid Anagram

# Problem Statement
Given two strings `s` and `t`, return true if `t` is an 
anagram of `s`, and false otherwise.

### Example
Input: s = "anagram", t = "nagaram" Output: true
## Approach
Count the frequency of each character in both strings. Compare the frequency maps. If they match, the strings are anagrams.

### Time Complexity
- **O(n)**:We traverse both strings once, resulting in  O(n)  time
### Space Complexity
- **O(1)**:The character count array has a fixed size of 26 (for lowercase letters).


## Solution Code
```C#
public class Solution {
    public bool IsAnagram(string s, string t) {
        if(s.Length != t.Length)    return false;
        int[] charCounts = new int[26];
        for(int i =0; i< s.Length;i++){
            charCounts[s[i] - 'a']++;
            charCounts[t[i] - 'a']--;
        }
        foreach(int count in charCounts){
            if(count!= 0){
                return false;
            }
        }
        return true;
    }
}