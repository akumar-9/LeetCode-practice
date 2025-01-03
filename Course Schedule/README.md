# Course Schedule


## Problem Statement
There are a total of `numCourses` courses you have to take, labeled from 0 to `numCourses` - 1. You are given an array `prerequisites` where `prerequisites[i]` = `[ai, bi]` indicates that you must take course `bi` first if you want to take course `ai`.

For example, the pair [0, 1], indicates that to take course 0 you have to first take course 1.
Return `true` if you can finish all courses. Otherwise, return fal`se.

### Example
Input: numCourses = 2, prerequisites = [[1,0]]
Output: true

## Approach
I use deadlock detection using dfs. If the graph of courses, has a cycle means no course can be completed. First build the graph. Graph is an array(know size) of List of integers(unkown size, hence List<int>). Prerequisite [a,b] means first take b then a. (b --> a). Build the graph using adjacency list. At any point, a node in the graph can be in one of 3 states. Unvisited(0), visiting(1) and visited(2). All nodes are marked unvisited first. A node is said to be visited, only if all of its neighbors are visited. If you encounter a neighbor that is already being visited, then a cycle is detected and courses cannot be completed. 

### Time Complexity
- **O(V + E)**: Building the graph and processing each node and edge takes linear time.
### Space Complexity
- **O(V + E)**: for the graph representation and the recursion stack (in the worst case, all nodes are in the stack).

## Solution Code
```C#
public class Solution {
    public bool CanFinish(int numCourses, int[][] prerequisites) {
        List<int>[] graph = new List<int>[numCourses];
        for(int i = 0; i < numCourses; i++){
            graph[i] = new List<int>();
        }

        foreach(var prereq in prerequisites){
            int course = prereq[0];
            int req = prereq[1];
            graph[req].Add(course);
        }

        int[] visited = new int[numCourses];
        bool hasCycle(int course){
            if(visited[course] == 1) return true;
            if(visited[course] == 2) return false;

            visited[course] = 1;
            foreach(var req in graph[course]){
                if( hasCycle(req)) return true;
            }
            visited[course] = 2;
            return false;
        }
        
        for(int i = 0; i < numCourses; i++){
            if(hasCycle(i)) return false;
        }

        return true;
    }

}