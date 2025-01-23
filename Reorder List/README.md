# Reorder List

# Problem Statement
You are given the head of a singly linked-list. The list can be represented as:

> L0 → L1 → … → Ln - 1 → Ln
Reorder the list to be on the following form:

 > L0 → Ln → L1 → Ln - 1 → L2 → Ln - 2 → …
You may not modify the values in the list's nodes. Only nodes themselves may be changed.

### Example
Input: head = [1,2,3,4]Output: [1,4,2,3]

## Approach
It is a combination of 3 easy problems. (Easy #1)Find the middle of the list using fast and slow pointer. (Easy #2)List to the right of mid should be reversed. (Easy #3)Merge the two halves

### Time Complexity
- **O(n)**: We go through the list atmost once.
### Space Complexity
- **O(1)**: We use extra space few variables.

## Solution Code
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
    public void ReorderList(ListNode head) {
        ListNode fast = head;
        ListNode slow = head;

        while(fast!=null && fast.next!=null){       // to locate mid point
            fast = fast.next.next;
            slow = slow.next;
        }

        ListNode curr = slow.next;              // slow is the mid point
        slow.next = null;                       // cut the link because slow will become the tail irrespective of n%2

        ListNode prev = null;                   // start reversing the right half
        while(curr!= null){
            ListNode next = curr.next;
            curr.next = prev;
            prev = curr;
            curr = next;
        }


        ListNode first = head, second = prev;   // merge the two lists
        while(second!=null){                    // why second? because it is smaller list
            ListNode temp1 = first.next;
            ListNode temp2 = second.next;

            first.next = second;
            second.next = temp1;

            first = temp1;
            second = temp2;
        }         
    }
}