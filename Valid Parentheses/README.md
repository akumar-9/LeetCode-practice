# Valid Parentheses

# Problem Statement
Given a string s containing just the characters `'('`, `')'`, `'{'`, `'}'`, `'['` and `']'`, determine if the input string is valid.

An input string is valid if:
1. Open brackets must be closed by the same type of brackets.
2. Open brackets must be closed in the correct order.
3. Every close bracket has a corresponding open bracket of the same type.
### Example
Input: s = "(]" Output: false
## Approach
Traverse the string and each time I see an open bracket, I push it onto a stack. If I see a closed bracket, I pop it from the stack only if the top of stack is same kind. 
### Time Complexity
- **O(n)**:where `n` is the length of the input string
### Space Complexity
- **O(n)**:In the worst case, the stack contains all open parentheses.

## Solution Code
```C#
public class Solution {
    public bool IsValid(string s) {
        Stack<char> stack = new Stack<char>();
        foreach(char c in s){
            if(c == '(' || c == '{' || c =='['){
                stack.Push(c);
                continue;
            }
            else if(stack.Count < 1){ 
                return false;
            }
            else if((c == ')' && stack.Peek() != '(') || 
                    (c == ']' && stack.Peek() != '[') || 
                    (c == '}' && stack.Peek() != '{') ){
                return false;
            }
            stack.Pop();
        }
        return stack.Count == 0;
    }
}