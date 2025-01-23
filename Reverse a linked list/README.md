# Reverse Linked List

## Problem Statement
Given the head of a singly linked list, reverse the list, and return the reversed list.

### Example
Input: head = [1,2,3,4,5] Output: [5,4,3,2,1]

## Approach
Use iterative approach. Keep track of prev, curr and next. Save the next node. Reverse the curr.next to point to prev. Move prev and current one step forward.

### Time Complexity
- **O(n)**: We go through the linked list once so O(n).
### Space Complexity
- **O(1)**: We use extra space few variables.

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
    public ListNode ReverseList(ListNode head) {
        ListNode curr = head;
        ListNode next;
        ListNode prev = null;
        while(curr != null){
            next = curr.next;
            curr.next = prev;
            prev = curr;
            curr = next;
        }
        return prev;
    }
}