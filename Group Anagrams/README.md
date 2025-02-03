# Group Anagrams

# Problem Statement
Given an array of `strings` strs, group the anagrams together. You can return the answer in any order.

### Example
Input: strs = ["eat","tea","tan","ate","nat","bat"] Output: [["bat"],["nat","tan"],["ate","eat","tea"]]
## Approach
Anagrams have same frequency count. So I use this as a key to the dictionary for grouping. But a dictionary key must be immutable. So use a string that represents the frequency count. Since the input strings are lower case, I create an array called char count that will keep track of the frequency of characters in a string. Then join the counts using a delimiter and use this as a key.
### Time Complexity
- **O(n*k)**:where `n` is the length of array and `k` Maximum length of a string
### Space Complexity
- **O(1)**:The character count array has a fixed size of 26 (for lowercase letters).


## Solution Code
```C#
public class Solution {
    public IList<IList<string>> GroupAnagrams(string[] strs) {
        Dictionary<string, IList<string>> s_map = new Dictionary<string, IList<string>>();

        foreach(string s in strs){
            string key = stringToKey(s);
            if(!s_map.ContainsKey(key)){
                s_map[key]= new List<string>();
            }
            s_map[key].Add(s);
        }

        string stringToKey(string s){   // convert the frequency to an immutable key
            int[] charCount = new int[26];
            foreach(char c in s){
                charCount[c - 'a']++;
            }
            return String.Join(",", charCount);
        }

        return s_map.Values.ToList();
    }
}