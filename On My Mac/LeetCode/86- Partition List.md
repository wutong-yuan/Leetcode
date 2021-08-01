# 86. Partition List

**# 86. Partition List**# 

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
    public ListNode partition(ListNode head, int x) {
        
        //create two lists, starting with the two dummy heads
        // create two pointers for each of those two lists to iterate
        ListNode dummyFirstHead = new ListNode(0);
        ListNode dummySecondHead = new ListNode(0);
        ListNode firstPointer = dummyFirstHead;
        ListNode secondPointer = dummySecondHead;
        
        // cureate a pointer for the original list to iterate
        // if the current value is greater than x, put it in the second list
        // otherwise, put it in the first list
        ListNode current = head;
        while (current != null) {
            if (current.val < x) {
                firstPointer.next = current;
                firstPointer = firstPointer.next;
            } else {
                secondPointer.next = current;
                secondPointer = secondPointer.next;
            }
            current = current.next;
        }
        
        // before we join those two lists, the end of the second list needs to point to null
        secondPointer.next = null;
        
        //connect those two together
        firstPointer.next = dummySecondHead.next;
        return dummyFirstHead.next;
    }
}
