# 23. Merge k Sorted Lists

**# 23. Merge k Sorted Lists**
# 

**_Approach 1 D & C_**
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
    public ListNode mergeKLists(ListNode[] lists) {
        if (lists.length == 0) return null;
        
        return mergeHelper(lists, 0, lists.length - 1);
    }
    
    private ListNode mergeHelper(ListNode[] lists, int start, int end) {
        if (start == end) return lists[start];
        
        int mid = start + (end - start) / 2;
        ListNode left = mergeHelper(lists, start, mid);
        ListNode right = mergeHelper(lists, mid + 1, end);
        return merge(left, right);
    }
    
    private ListNode merge(ListNode list1, ListNode list2) {
        ListNode dummy = new ListNode(0);
        // tail is a pointer and pointing to the last element in the final sorted list
        // tail points to the dummy in the beginning
        // while we compare the node in list1 and list2, we move the tail pointer 
        ListNode tail = dummy;
        // p1 and p2 act as two pointers 
        // as we add the node to the final list we use p1 and p2 pointer to move to the next node int
        // the corresponding list
        ListNode p1 = list1;
        ListNode p2 = list2;
        while (p1 != null && p2 != null) {
            if (p1.val < p2.val) {
                // add the first node(p1) in list1 to the final list
                tail.next = p1;
                // move the tail pointer to the end of the final list
                tail = p1;
                //move the p1 pointer to the next node in list1
                p1 = p1.next;
            } else {
                tail.next = p2;
                tail = p2;
                p2= p2.next;
            }
        }
        // at this point, either list1 or list2 still have nodes left
        if (p1 != null) {
            tail.next = p1;
        } else {
            tail.next = p2;
        }
        
        return dummy.next;
    }
}

**_Approach 2: use Heap_**

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
    // PQ is automatically sorted but if the element is a ListNode, we need to tell
    //PQ how to sort those nodes
    private Comparator<ListNode> ListNodeComparator = new Comparator<ListNode>() {
        public int compare(ListNode left, ListNode right) {
            return left.val - right.val;
        }
    };
    public ListNode mergeKLists(ListNode[] lists) {
        if (lists == null || lists.length == 0) return null;
        
        Queue<ListNode> pq = new PriorityQueue<>(lists.length, ListNodeComparator);
        

        for (int i = 0; i < lists.length; i++) {
            if (lists[i] != null) {
                pq.offer(lists[i]);
            }
        }
        
        ListNode dummy = new ListNode(0);
        ListNode tail = dummy;
        while (!pq.isEmpty()) {
            ListNode node = pq.poll();
            tail.next = node;
            tail = node;
            if (node.next != null) {
                pq.offer(node.next);
            }
        }
        return dummy.next;
    }
}

**_Approach 3: merge two first then next two then next two _**

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
    public ListNode mergeKLists(ListNode[] lists) {
        
        ArrayList<ListNode> listsCopy = new ArrayList<>();
        for (int i = 0; i < lists.length; i++) {
            listsCopy.add(lists[i]);
        }
        
        if (lists == null || lists.length == 0) {
            return null;
        }
        
        while (listsCopy.size() > 1) {
            ArrayList<ListNode> newLists = new ArrayList<>();
            
            for (int i = 0; i < listsCopy.size() - 1; i += 2) {
                ListNode node1 = listsCopy.get(i);
                ListNode node2 = listsCopy.get(i + 1);
                ListNode mergedList = merge(node1, node2);
                newLists.add(mergedList);
            }
            if (listsCopy.size() % 2 == 1) {
                newLists.add(listsCopy.get(listsCopy.size() - 1));
            }
            listsCopy = newLists;
        }
        
        return listsCopy.get(0);
    }
    
    private ListNode merge(ListNode node1, ListNode node2) {
        ListNode p1 = node1;
        ListNode p2 = node2;
        ListNode dummy = new ListNode(0);
        ListNode tail = dummy;
        while (p1 != null && p2 != null) {
            if (p1.val < p2.val) {
                tail.next = p1;
                tail = p1;
                p1 = p1.next;
            } else {
                tail.next = p2;
                tail = p2;
                p2 = p2.next;
            }
        }
        
        if (p1 != null) {
            tail.next = p1;
        } else {
            tail.next = p2;
        }
        return dummy.next;
    }
}
