# Binary Tree Level Order Traversal

# Problem Statement
Given the `root` of a binary tree, return the level order traversal of its nodes' values. (i.e., from left to right, level by level).

### Example
Input: root = [3,9,20,null,null,15,7]
Output: [[3],[9,20],[15,7]]

## Approach
I use BFS to traverse the tree. I track the number of nodes in the current level by tracking the size of the queue. Unlike BFS where we would continuously pop elements until the queue is empty, here we pop only based on the levelsize. Check the size of queue to get the number of nodes in the current level.
### Time Complexity
- **O(n)**:Each node is visited once.
### Space Complexity
- **O(n)**:The queue stores nodes level by level, which in the worst case is all leaf nodes.
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
    public IList<IList<int>> LevelOrder(TreeNode root) {
        List<IList<int>> result = new List<IList<int>>();
        if(node == null) {
            return;
        }
        Queue<TreeNode> queue = new Queue<TreeNode>();
        queue.Enqueue(node);
        while(queue.Count != 0){
            int levelCount = queue.Count;
            List<int> level = new List<int>();
            for(int i = 0; i < levelCount; i++){                
                TreeNode currNode = queue.Dequeue();
                if(currNode.left!=null){
                    queue.Enqueue(currNode.left);
                }
                if(currNode.right!= null){
                    queue.Enqueue(currNode.right);
                }
                children.Add(currNode.val);                
            }
            result.Add(children);
        }
        return result;
    }
}