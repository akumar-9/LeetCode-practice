# Merge K Sorted Lists

# Problem Statement
You are given an array of `k` linked-lists `lists`, each linked-list is sorted in ascending order.

Merge all the linked-lists into one sorted linked-list and return it.
### Example
Input: lists = [[1,4,5],[1,3,4],[2,6]] Output: [1,1,2,3,4,4,5,6]

## Approach
I use a min-heap to store all the heads, get min element from the heap and add it to the final merged list. Whichever node was popped, add it's next node to the heap. Do this until the heap is empty.

### Time Complexity
- **O(nlogk)**: Where n is total number of node across all lists and k is the number of linked lists.
### Space Complexity
- **O(k)**: Heap stores at most k elements at a time.

## Solution Code
```C#
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     public int val;
 *     public ListNode next;
 *     public ListNode(int val=0, ListNode next=null) {
 *         this.val = val;
 *         this.next = next;
 *     }
 * }
 */
public class Solution {
    public ListNode MergeKLists(ListNode[] lists) {
        if(lists.Length < 1){
            return null;
        }
        PriorityQueue<ListNode, int> minHeap = new PriorityQueue<ListNode, int>();
        foreach(var head in lists){
            if(head!= null)
                minHeap.Enqueue(head, head.val);
        }

        ListNode dummy = new ListNode(-1);
        ListNode current = dummy;

        while(minHeap.Count > 0){
            ListNode minNode = minHeap.Dequeue();
            current.next = minNode;
            current = current.next;

            if(minNode.next!= null){
                minHeap.Enqueue(minNode.next, minNode.next.val);
            }
        }

        return dummy.next;
    }
}
