# 25. Reverse Nodes in k-Group

**# 25. Reverse Nodes in k-Group**

**_See paper notes_**

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
    public ListNode reverseKGroup(ListNode head, int k) {
        ListNode dummy = new ListNode(0);
        //dummy -> 1, create a dummy node and let it point to the original head
        dummy.next = head;
        
        // change the head to dummy and start to reverse
        head = dummy;
        // we keep reversing until we reach the end or the nodes in the remainning list
        // are less than k. for example, the last list has only one node 5, will break this while loop
        while (true) {
            head = reverseK(head, k);
            if (head == null) {
                break;
            }
        }
        
        return dummy.next;
    }
    
    private ListNode reverseK(ListNode head, int k) {
        // find the kth node. We start from the head, use the for loop
        // to find the kth node. The first kth node is node 2.
        // after we find the kth node, we start our reversal
        ListNode nk = head;
        for (int i = 0; i < k; i++) {
            if (nk == null) {
                return null;
            }
            nk = nk.next;
        }
        
        if (nk == null) {
            return null;
        }
        
        // start our reversal
        // the n1 node is node 1, which is the head.next. 
        // n1 was the head but after we assign dummy as our head, n1 is head.next now
        ListNode n1 = head.next;
        // we need to get the nkplus node as well, which is the node 3. because after we
        // reverse we need to connect the reversed list to the original list. 
        ListNode nkplus = nk.next;
        
        //below is the standard reversal 
        ListNode prev = null;
        ListNode curt = n1;
        while (curt != nkplus) {
            ListNode temp = curt.next;
            curt.next = prev;
            prev = curt;
            curt = temp;
        }
        
        // then we connect 
        // head needs to point to nk node, which is dummy -> 2
        head.next = nk;
        // 1 -> 3
        n1.next = nkplus;
        return n1;
    }
}
