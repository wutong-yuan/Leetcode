# 876. Middle of the Linked List

**# 876. Middle of the Linked List**# 

My solution: fast, code is a little long
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
    public ListNode middleNode(ListNode head) {
        
        int size = 0;
        ListNode current = head;
        while (current != null) {
            size++;
            current = current.next;
        }
        
        ListNode middleNode = head;

        for (int i = 1; i <= size / 2; i++) {
            middleNode = middleNode.next;
        }
        
        return middleNode;
    }
}
**_Two pointers: - see leetcode solution section_**

class Solution {
    public ListNode middleNode(ListNode head) {
        ListNode fast = head;
        ListNode slow = head;
        
        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;
        }
        return slow;
    }
}
