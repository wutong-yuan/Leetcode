# 109. Convert Sorted List to Binary Search Tree

**# 109. Convert Sorted List to Binary Search Tree**
# 

**Be careful and compare this one with 148. in 148, we just need to cut the connection between the middle and the middle.next because if we don’t, when we recurse on the left side, we pass the head, and it would still the whole list not just the left side. **
**
**
**But here, we need to cut the middle node out of the whole list because this would be the root. So we need a prev pointer of the middle and set it to prev.next == null to cut the middle out **
**Then we do root.right == right, root.left = left. **

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
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    public TreeNode sortedListToBST(ListNode head) {
        if (head == null) return null;
        
        ListNode mid = findMid(head);
        TreeNode root = new TreeNode(mid.val);
        //base case for this recursion. Only one element left in the list
        if (head == mid) return root;
        
        TreeNode right = sortedListToBST(mid.next);
        // mid.next = null;
        TreeNode left = sortedListToBST(head);
        root.left = left;
        root.right = right;
        return root;
    }
    
    private ListNode findMid(ListNode head) {
        ListNode fast = head;
        ListNode slow = head;
        ListNode prev = null;
        
        while (fast!= null && fast.next != null) {
            prev = slow;
            fast = fast.next.next;
            slow = slow.next;
        }  
        // if prev is null meaning the head is the middle and the left is null, we don't need to cut 
        // the middle node out/ otherwise, we need to cut the middle out of the list
        if (prev != null) {
            prev.next = null;
        }
        return slow;
    }
}

**_Use extra space — convert the list to an array and this problem becomes convert an array to the list_**

class Solution {
    public TreeNode sortedListToBST(ListNode head) {
        if (head == null) return null;
        ArrayList<Integer> array = convertListToArray(head);
        return convertListToBST(0, array.size() - 1, array);
    }
    
    private ArrayList<Integer> convertListToArray (ListNode head) {
        ArrayList<Integer> array = new ArrayList<Integer>();
        ListNode temp = head;
        while (temp != null) {
            array.add(temp.val);
            temp = temp.next;
        }
        return array;
    }
    
    private TreeNode convertListToBST (int left, int right, ArrayList<Integer> array) {
        if (left > right) return null;
        
        int mid = left + (right - left) / 2;
        TreeNode root = new TreeNode(array.get(mid));
        
        if (left == right) return root;
        
        root.left = convertListToBST(left, mid - 1, array);
        root.right = convertListToBST(mid + 1, right, array);
        return root;
    }
}

