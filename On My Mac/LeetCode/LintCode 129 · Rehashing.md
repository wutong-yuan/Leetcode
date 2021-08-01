# LintCode 129 · Rehashing

# LintCode **# 129 · Rehashing**

# 

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
     * @param hashTable: A list of The first node of linked list
     * @return: A list of The first node of linked list which have twice size
     */    
    public ListNode[] rehashing(ListNode[] hashTable) {
        // write your code here
        int oldCapacity = hashTable.length;
        int newCapacity = oldCapacity * 2;
        ListNode[] newTable = new ListNode[newCapacity];

        for (int i = 0; i < oldCapacity; i++) {
            while (hashTable[i] != null) {
                int newIndex = (hashTable[i].val % newCapacity + newCapacity) % newCapacity;
                // if the current position is null meaning, no element is mapped to 
                // this position yet. We just create a node with the old val
                // map it to this new position
                if (newTable[newIndex] == null) {
                    newTable[newIndex] = new ListNode(hashTable[i].val);
                    // if the current position is occupied, we need to map it to the end 
                    // of the linkedlist
                    // we use the dummy node as the head of the linkedlist in the current 
                    //position. Iterate this list until we find the last position
                    // put the new element overthere
                } else {
                    ListNode dummy = newTable[newIndex];
                    while (dummy.next != null) {
                        dummy = dummy.next;
                    }
                    dummy.next = new ListNode(hashTable[i].val);
                }
                // go to the next element in the old position ( there might be a linkedlist
                // at the old position)
                hashTable[i] = hashTable[i].next;
            }
        }
        return newTable;
    }
};
