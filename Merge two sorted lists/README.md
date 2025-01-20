# Merge Two Sorted Lists

# Problem Statement
You are given the heads of two sorted linked lists list1 and list2.

Merge the two lists into one sorted list. The list should be made by splicing together the nodes of the first two lists.

Return the head of the merged linked list.

### Example
Input: list1 = [1,2,4], list2 = [1,3,4] Output: [1,1,2,3,4,4]

## Approach
I use a new dummy node to serve as a starting point of the merged list. Use a current pointer to traverese and build the list. Traverse both lists, compare values, add the smaller value node to list, move the pointer for the list and the current pointer. If either of the list is exhausted, append the remaining nodes to the merged list. 

### Time Complexity
- **O(n+m)**: Where n and m are the lengths of the two lists. Each node is visited once.
### Space Complexity
- **O(1)**: We use extra space few variables.

## Solution Code
**
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
    public ListNode MergeTwoLists(ListNode list1, ListNode list2) {
        ListNode mergedHead = new ListNode(-1);
        ListNode current = mergedHead;
        while(list1!=null && list2!=null){
            if(list1.val <= list2.val){
                current.next = list1;
                list1= list1.next;
            }
            else{
                current.next = list2;
                list2 = list2.next;
            }
            current = current.next;
        }
        if(list1!=null){
            current.next = list1;
        }
        if(list2!=null){
            current.next = list2;
        }
    return mergedHead.next;
    }
}
