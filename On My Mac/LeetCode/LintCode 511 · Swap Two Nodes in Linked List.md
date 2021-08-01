# LintCode 511 · Swap Two Nodes in Linked List

**# LintCode 511 · Swap Two Nodes in Linked List**
**
**
**
**
/**
 * Definition for ListNode
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */

public class Solution {
    /**
     * @param head: a ListNode
     * @param v1: An integer
     * @param v2: An integer
     * @return: a new head of singly-linked list
     */
     public ListNode swapNodes(ListNode head, int v1, int v2) {
        // write your code here
        ListNode dummy = new ListNode(0);
        dummy.next = head;
        head = dummy;

        ListNode prev = null;
        ListNode prev1 = null;
        ListNode prev2 = null;
        ListNode node1 = null;
        ListNode node2 = null;
        ListNode current = head;
        while (current != null) {
            if (current.val == v1) {
                prev1 = prev;
                node1 = current;
            } else if (current.val == v2) {
                prev2 = prev;
                node2 = current;
            }
            if(node1 != null && node2 != null) break;
            prev = current;
            current = current.next;
        }
        if (node1 == null || node2 == null) return dummy.next;

        ListNode next1 = node1.next;
        ListNode next2 = node2.next;

**_// need to consider the case that n1 and n2 are adjacent _**
**_
_**
        if (next1 == node2) {
            prev1.next = node2;
            node2.next = node1;
            node1.next = next2;
        } else if (next2 == node1) {
            prev2.next = node1;
            node1.next = node2;
            node2.next = next1;
        } else {
            prev1.next = node2;
            node2.next = next1;
            prev2.next = node1;
            node1.next = next2;
        }

        return dummy.next;
    }
}
