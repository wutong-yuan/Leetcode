# 21 Merge two Sorted List

#   21 Merge two Sorted List
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
         // create a headNode for the result list
        ListNode prehead = new ListNode(-1);
        // create a iterator which starts from the headNode
        ListNode prev = prehead;

        while (l1 != null && l2 != null) {
            // compare the value of the two lists. Here l1.value
            // is the the value of the first node in list 1
            if(l1.val <= l2.val) {
                // if l1.value <= l2.value, we let the headNode 
                // point to l1.
                prev.next = l1;
                // Then we compare the rest of l1 to l2
                l1 = l1.next;
            } else {
                prev.next = l2;
                l2 = l2.next;
            }
            // Each time, after we finish the comparison, we move
            // the iterator to the next. If above l1.val <= l2.val,
            // after this step, temp will be at the first element 
            // in list 1. 
            prev = prev.next;
        }
        // exactly one of l1 or l2 can be null at this point, so 
        // connect the non-null list to the end of the merged list
        prev.next = l1 == null ? l2 : l1;
        
        return prehead.next; 
    }
}

