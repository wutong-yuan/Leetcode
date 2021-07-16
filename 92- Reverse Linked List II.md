# 92. Reverse Linked List II

**# 92. Reverse Linked List II**# 

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
    public ListNode reverseBetween(ListNode head, int left, int right) {
        ListNode dummy = new ListNode(0);
        dummy.next = head;
        head = dummy;
        
        ListNode nLeftPrev = head;
        for (int i = 0; i < left - 1; i++) {
            if (nLeftPrev == null) {
                return null;
            }
            nLeftPrev = nLeftPrev.next;
        }
        
        ListNode nLeft = nLeftPrev.next;
        ListNode nRight = head;
        for (int i = 0; i < right; i++) {
            if (nRight == null) {
                return null;
            }
            nRight = nRight.next;
        }
        
        ListNode nRightNext = nRight.next;
            
        ListNode prev = nLeftPrev;
        ListNode current = nLeft;
        
        while (current != nRightNext) {
            ListNode temp =current.next;
            current.next = prev;
            prev = current;
            current = temp;    
        }
        
        nLeft.next = nRightNext;
        nLeftPrev.next = nRight;
        
        return dummy.next;
    }
}
