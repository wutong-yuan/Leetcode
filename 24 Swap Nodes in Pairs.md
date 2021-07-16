# 24 Swap Nodes in Pairs

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
    public ListNode swapPairs(ListNode head) {
        ListNode dummy = new ListNode(0);
        dummy.next = head;
        head = dummy;
        
        while (true) {
            head = reverse2(head, 2);
            if (head == null) break;
        }
        
        return dummy.next;
    }
    
    private ListNode reverse2(ListNode head, int k) {
        ListNode nk = head;
        for (int i = 0; i < k; i++) { 
            if (nk == null) return null;
            nk = nk.next;
        }
        
        if (nk == null) return null;
        
        ListNode n1 = head.next;
        ListNode nkplus = nk.next;
        
        ListNode prev = null;
        ListNode current = head;
        while (current != nkplus) {
            ListNode temp = current.next;
            current.next = prev;
            prev = current;
            current = temp;
        }
        //connect
        head.next = nk;
        n1.next = nkplus;
        
        return n1;
    }
}
