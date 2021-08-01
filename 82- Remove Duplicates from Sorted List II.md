# 82. Remove Duplicates from Sorted List II

**# 82. Remove Duplicates from Sorted List II**

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
    public ListNode deleteDuplicates(ListNode head) {
        ListNode dummy = new ListNode(0);
        dummy.next = head;
        
        ListNode prev = dummy;
        ListNode curr = dummy.next;
        
        while (curr != null) {
            while (curr.next != null && curr.val == curr.next.val) {
                curr = curr.next;
            }
            // only prev.next == curr meaning the current node has no duplicate
            if (prev.next == curr) {
                prev = curr;
                // if there is duplicate vals, curr moved toward to the next and prev.next 
                // will not point to curr any more
                // if that is the case, we need to skip curr because curr has duplicate vals.
            } else {
                prev.next = curr.next;
            }
            
            curr = curr.next;
        }
        
        return dummy.next;
    }
}
