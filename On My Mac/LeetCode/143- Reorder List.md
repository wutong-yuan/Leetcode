# 143. Reorder List

**# 143. Reorder List**# 

The leetcode solution is good. Check that if you forget.

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
    public void reorderList(ListNode head) {
        // step1: find the middle node, cut the list into two lists
        // 1->2->3----->4->-5>-6>, 4 is the middle. 
        ListNode middle = head;
        ListNode fast = head;
        while (fast != null && fast.next != null) {
            middle = middle.next;
            fast = fast.next.next;
        }
        
        // step2: reverse the second list to 6->5->4->null. 3 -> 4 still
        ListNode curr = middle;
        ListNode prev = null;
        while (curr != null) {
            ListNode temp = curr.next;
            curr.next = prev;
            prev = curr;
            curr = temp;
        }
        // out of this loop, prev = 6, curr = null
        // step3: merge two lists together
        ListNode second = prev;
        ListNode first = head;
        while (second.next != null) {
            ListNode next1 = first.next;
            ListNode next2 = second.next;
            first.next = second;
            second.next = next1;
            first = next1;
            second = next2;
        }
    }
}
