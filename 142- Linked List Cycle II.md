# 142. Linked List Cycle II

**142. Linked List Cycle II**

/**
 * Definition for singly-linked list.
 * class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public ListNode detectCycle(ListNode head) {
        if (head == null || head.next == null) return null;
        ListNode s = head;
        ListNode f = head; 
        // faster alwasy runs faster than ser so check faster only.         
        // A fast pointer will either loop around a cycle and meet the s
        // pointer or reach the `null` at the end of a non-cyclic list. 
        while (f != null && f.next != null) {
            s = s.next;
            f = f.next.next;
            // if s == f go into second phrase
            if(s == f) {
                f = head;
                while (s != f) {
                    s = s.next;
                    f = f.next;
                }
                return s;
            }
         }
        return null;
    }
}
