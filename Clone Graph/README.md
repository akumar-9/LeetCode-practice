# Clone Graph


## Problem Statement
Given a reference of a node in a connected undirected graph.

Return a deep copy (clone) of the graph.

Each node in the graph contains a value (int) and a list (List[Node]) of its neighbors.

class Node {
    public int val;
    public List<Node> neighbors;
}
 

Test case format:

For simplicity, each node's value is the same as the node's index (1-indexed). For example, the first node with val == 1, the second node with val == 2, and so on. The graph is represented in the test case using an adjacency list.

An adjacency list is a collection of unordered lists used to represent a finite graph. Each list describes the set of neighbors of a node in the graph.

The given node will always be the first node with val = 1. You must return the copy of the given node as a reference to the cloned graph.


### Example
Input: adjList = [[2,4],[1,3],[2,4],[1,3]]
Output: [[2,4],[1,3],[2,4],[1,3]]

## Approach
I use DFS here. I maintain a Dictionary visited that keeps track of a node and its clone. If a node is already in the dictionary then it means that it already has been cloned. For cloning, in DFS, clone the current node, then clone its neighbors.

### Time Complexity
- **O(v+e)**: Each node and edge is visited once.
### Space Complexity
- **O(V)**: Recursion stack size for DFS.

## Solution Code
```C#
/*
// Definition for a Node.
public class Node {
    public int val;
    public IList<Node> neighbors;

    public Node() {
        val = 0;
        neighbors = new List<Node>();
    }

    public Node(int _val) {
        val = _val;
        neighbors = new List<Node>();
    }

    public Node(int _val, List<Node> _neighbors) {
        val = _val;
        neighbors = _neighbors;
    }
}
*/

public class Solution {
    public Node CloneGraph(Node node) {
        Dictionary<Node,Node> visited = new Dictionary<Node,Node>();
        return _cloneNode(visited, node);
    }
    private Node _cloneNode(Dictionary<Node,Node> visited, Node node){
        if(node == null)
            return null;
        if(visited.ContainsKey(node))
            return visited[node];

        Node cloneNode = new Node(node.val);
        visited[node] = cloneNode;
        foreach(Node neighbor in node.neighbors){
            cloneNode.neighbors.Add(_cloneNode(visited, neighbor));
        }
            
        return cloneNode;
    }
}