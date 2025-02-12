# Binary Tree Maximum Path Sum

# Problem Statement
A path in a binary tree is a sequence of nodes where each pair of adjacent nodes in the sequence has an edge connecting them. A node can only appear in the sequence at most once. Note that the path does not need to pass through the root.

The path sum of a path is the sum of the node's values in the path.

Given the `root` of a binary tree, return the maximum path sum of any non-empty path.

### Example
Input: root = [1,2,3]
Output: 6
Explanation: The optimal path is 2 -> 1 -> 3 with a path sum of 2 + 1 + 3 = 6.

## Approach
I use recursion here. First, find the max path sum of left subtree, then right and then calculate the current path sum and compare with max sum. At each node we calculate, two values, 1. Current path sum, 2. Maximum path sum to be returned to parent (this is where you make a choice between left and right subtree).
### Time Complexity
- **O(n)**:where `n` is the number of the nodes in the tree.
### Space Complexity
- **O(h)**:The recursive call stack uses space proportional to the height of the tree(h).
## Solution Code
```C#
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     public int val;
 *     public TreeNode left;
 *     public TreeNode right;
 *     public TreeNode(int val=0, TreeNode left=null, TreeNode right=null) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
public class Solution {
    public int MaxPathSum(TreeNode root) {
        int maxSum = int.MinValue;
        MaxGain(root);

        int MaxGain(TreeNode node){
            if(node == null)    return 0;
            
            int leftGain = Math.Max(0,MaxGain(node.left));
            int rightGain = Math.Max(0,MaxGain(node.right));

            int currentPathSum = node.val + leftGain + rightGain;

            maxSum = Math.Max(maxSum, currentPathSum);

            return node.val + Math.Max(leftGain, rightGain);
        }
        return maxSum;
    }
}