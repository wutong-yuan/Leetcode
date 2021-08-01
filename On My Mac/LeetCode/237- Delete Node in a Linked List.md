# 237. Delete Node in a Linked List

**# 237. Delete Node in a Linked List**

Code is easy but not easy to figure it out 

class Solution {
    public void deleteNode(ListNode node) {
        if (node == null) return;
        node.val = node.next.val;
        node.next = node.next.next;
    }
}
