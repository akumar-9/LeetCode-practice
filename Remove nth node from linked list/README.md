# Remove Nth Node From End of List

# Problem Statement
Given the `head` of a linked list, remove the nth node from the end of the list and return its head.

### Example
Input: head = [1,2,3,4,5], n = 2 Output: [1,2,3,5]
## Approach
I use a new `dummy` node to serve as a starting point of the new list. Use two pointers `ahead` and `behind` pointers. Start at `dummy` and move `ahead` `n+1` times. Move ahead and behind pointer one position until the end of the list. The `behind` pointer will be now at the node that is before the node to be removed i.e. `n+1th` node from the end. Point the behind.next to it's next.

### Time Complexity
- **O(n)**: We go through the list atmost once.
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
    public ListNode RemoveNthFromEnd(ListNode head, int n) {
        ListNode dummy = new ListNode(-1, head);
        ListNode slow = dummy;
        ListNode fast = dummy;
        for(int i = 0; i < n+1; i++){
            fast = fast.next;
        }

        while(fast!= null){
            slow = slow.next;
            fast = fast.next;
        }
        
        slow.next = slow.next.next;

        return dummy.next;
    }
}