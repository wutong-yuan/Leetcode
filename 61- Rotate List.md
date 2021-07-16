# 61. Rotate List

**# 61. Rotate List**# 

**_The leetcode article is helpful_**

//**
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
    public ListNode rotateRight(ListNode head, int k) {
        // basecase
        if (head == null) return null;
        // just one element in the list
        if (head.next == null) return head;
        
        // step1: connect the tail to the head
        ListNode lastNode = head;
        int n = 1;
        while (lastNode.next != null) {
            n++;
            lastNode = lastNode.next;
        }
        
        k = k % n;
        if (k == 0) return head;
        
        lastNode.next = head;
        
        // cut the list and get new head (n-k)th node and tail(n-k).next
        ListNode newTail = head;
        for (int i = 1; i < n - k; i++) {
            newTail = newTail.next;
        }
        
        ListNode newHead = newTail.next;
        newTail.next = null;
        
        return newHead;
    }
}
