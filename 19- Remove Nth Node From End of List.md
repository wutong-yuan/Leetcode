# 19. Remove Nth Node From End of List

**# 19. Remove Nth Node From End of List**# 

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
    public ListNode removeNthFromEnd(ListNode head, int n) {
        ListNode dummy = new ListNode(0);
        dummy.next = head;
        ListNode pointer = dummy;
        
        int size = 0;
        
        while (pointer.next != null) {
            size++;
            pointer = pointer.next;          
        }
        
        pointer = dummy;
        int count = 0;
        while (pointer != null && pointer.next != null) {
            count++;
            ListNode prev = pointer;
            ListNode next = pointer.next.next;
            if (count == size + 1 - n) {
                prev.next = next;
            }
            pointer = pointer.next;
        }
        
        return dummy.next;
    }
}
