# Combination Sum

## Problem Statement
Given an array of distinct integers `candidates` and a target integer `target`, return a list of all unique combinations of `candidates` where the chosen numbers sum to `target`. You may return the combinations in any order.

The same number may be chosen from candidates an unlimited number of times. Two combinations are unique if the 
frequency of at least one of the chosen numbers is different.

The test cases are generated such that the number of unique combinations that sum up to target is less than `150` combinations for the given input.
### Example
Input: candidates = [2,3,6,7], target = 7
Output: [[2,2,3],[7]]

## Approach
I use backtracking here. Explore all combinations recursively. Add candidate to current combination, subtract the candidate from the target, backtrack if target becomes zere or negative. Sort before to avoid duplicates. 

### Time Complexity
- **O(2^n)**: Depends on number of valid solutions and the depth of tree but worstcase all combinations are explored.
### Space Complexity
- **O(target/min(candidates))**: The complexity is proportional to maximum depth of recursion.

## Solution Code
```C#
public class Solution {
    public IList<IList<int>> CombinationSum(int[] candidates, int target) {
        Array.Sort(candidates);
        IList<IList<int>> result = new List<IList<int>>();
        _backtrack(0,candidates,target,new List<int>(), result);
        return result;
    }
    private void _backtrack(int start, int[] candidates, int target, List<int> combination, IList<IList<int>> result) {
        if(target == 0){
            result.Add( new List<int>(combination));
            return;
        }
        for(int i = start; i < candidates.Length; i++){
            if(candidates[i] > target)
                break;       
            combination.Add(candidates[i]);
            _backtrack(i, candidates, target - candidates[i], combination, result);
            combination.RemoveAt(combination.Count - 1);
        }
    }
}