# 148. Sort List

**# 148. Sort List**

# Be careful about the findMiddle () below.
Here we use fast = head.next instead of fast = head because we need to partition the list into two lists.
If we do fast = head, we would get stack overflow because the middle of [1,2,3] is 2 then the middle of [1,2] is 2 as well. 

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
    public ListNode sortList(ListNode head) {
        if (head == null || head.next == null) return head;
        // step1: find middle
        ListNode middle = findMiddle(head);
        //cut the list into two pieces
        ListNode right = sortList(middle.next);
        middle.next = null;
        ListNode left = sortList(head);
        //merge those two
        return merge(left, right);     
    }
    
   ** private ListNode findMiddle(ListNode head) {**
**        ListNode fast = head.next;**
**        ListNode slow = head;**
**        **
**        while (fast != null && fast.next != null) {**
**            fast = fast.next.next;**
**            slow = slow.next;**
**        }**
**        return slow;**
**    }**
**    **
    private ListNode merge(ListNode left, ListNode right) {
        if (left == null && right == null) return null;
        if (left == null) return right;
        if (right == null) return left;
        
        ListNode dummy = new ListNode(0);
        ListNode current = dummy;
        ListNode pointer1 = left;
        ListNode pointer2 = right;
        while (pointer1 != null && pointer2 != null) {
            if (pointer1.val < pointer2.val) {
                current.next = pointer1;
                pointer1 = pointer1.next;
            } else {
                current.next = pointer2;
                pointer2 = pointer2.next;
            }
            current = current.next;
        }
        if (pointer1 != null) {
            current.next = pointer1;
        } else if (pointer2 != null) {
            current.next = pointer2;
        }
        return dummy.next;
    }
}
