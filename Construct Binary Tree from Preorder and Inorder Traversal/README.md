# Construct Binary Tree from Preorder and Inorder Traversal

# Problem Statement
Given two integer arrays preorder and inorder where preorder is the preorder traversal of a binary tree and inorder is the inorder traversal of the same tree, construct and return the binary tree.
### Example
Input: preorder = [3,9,20,15,7], inorder = [9,3,15,20,7]
Output: [3,9,20,null,null,15,7]

## Approach
I take advantage of the knowledge that pre-order has the form `root`, `left tree`, `right tree` and the in-order has the form `left tree`, `root`, `right tree`. That means the first item is always the root of the tree. Locate the `root` in the inorder, and the left sub tree will be the values that are left of this `root` and the right sub tree on the `root`. Effecient way to lookup the index of root in the in-order list is by making use of a dictionary(for O(1) lookups).
### Time Complexity
- **O(N)**:Each node in the tree is visited. The index lookup is also in the order of O(n).
### Space Complexity
- **O(N)**: Extra space for the hashmap.
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
    Dictionary<int, int> inorderMap;
    int preorderIndex = 0;
    public TreeNode BuildTree(int[] preorder, int[] inorder) {
        inorderMap = new Dictionary<int, int>();
        for(int i = 0; i < inorder.Length; i++){
            inorderMap[inorder[i]] = i;
        }
        return Build(preorder, 0, preorder.Length-1);
        TreeNode Build(int[] preorder, int left, int right){
            if(left > right)    return null;

            int rootVal = preorder[preorderIndex++];
            //int rootIndex = Array.IndexOf(inorder, rootVal);      this would be O(n) lookup otherwise
            int rootIndex = inorderMap[rootVal];
            TreeNode root = new TreeNode(rootVal);
            root.left = Build(preorder, left, rootIndex-1);
            root.right = Build(preorder, rootIndex+1, right);

            return root;
        }
    }
}