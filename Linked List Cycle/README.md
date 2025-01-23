# Linked List Cycle 

### Problem Statement
Given `head`, the head of a linked list, determine if the linked list has a cycle in it.

There is a cycle in a linked list if there is some node in the list that can be reached again by continuously following the `next` pointer. Internally, `pos` is used to denote the index of the node that `tail`'s `next` pointer is connected to. Note that `pos` is not passed as a parameter.

Return `true` if there is a cycle in the linked list. Otherwise, return `false`.

### Example
Input: head = [3,2,0,-4], pos = 1 Output: true

## Approach
Use the tortoise and hare method(Floyd's Cycle detection method). Two pointers fast and slow are used. Slow moves 1 step at a time and fast moves 2 steps at a time, if they meet at any point in time, then a cycle exists else not.

### Time Complexity
- **O(n)**: Each node is visited atmost twice.
### Space Complexity
- **O(1)**: We use extra space few variables.

## Solution Code
```C#
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     public int val;
 *     public ListNode next;
 *     public ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public bool HasCycle(ListNode head) {
        ListNode slow = head;
        ListNode fast = head;
        while(fast != null && fast.next != null){
            slow = slow.next;
            fast = fast.next.next;
            if(slow == fast){
                return true;
            }
        }
        return false;
    }
}