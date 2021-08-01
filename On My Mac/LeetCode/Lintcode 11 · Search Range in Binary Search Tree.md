# Lintcode 11 · Search Range in Binary Search Tree

# Lintcode **# 11 · Search Range in Binary Search Tree**
Algorithms
Medium**
**
**
**
DescriptionSolutionNotesDiscussLeaderboard

**Description**
Given a binary search tree and a range [k1, k2], return node values within a given range in ascending order.
**Example**
**Example 1:**

Input:
tree = {5}
k1 = 6
k2 = 10
Output:
[]
Explanation:
No number between 6 and 10
**Example 2:**

Input:
tree = {20,8,22,4,12}
k1 = 10
k2 = 22
Output:
[12,20,22]
Explanation:
[12,20,22] between 10 and 22

**_My solution _**
/**
 * Definition of TreeNode:
 * public class TreeNode {
 *     public int val;
 *     public TreeNode left, right;
 *     public TreeNode(int val) {
 *         this.val = val;
 *         this.left = this.right = null;
 *     }
 * }
 */

public class Solution {
    /**
     * @param root: param root: The root of the binary search tree
     * @param k1: An integer
     * @param k2: An integer
     * @return: return: Return all keys that k1<=key<=k2 in ascending order
     */
    public List<Integer> searchRange(TreeNode root, int k1, int k2) {
        ArrayList<Integer> range = new ArrayList<>();
        ArrayList<Integer> fullList = new ArrayList<>();
        if (root == null) return null;
        inorderTraversal(root, fullList);
        
        for (int i = 0; i < fullList.size(); i++) {
            if (fullList.get(i) >= k1 && fullList.get(i) <= k2) {
                range.add(fullList.get(i));
            }
        }
        return range;
        
    }
    public void inorderTraversal(TreeNode root, ArrayList<Integer> list) {
        if (root == null) return;

        inorderTraversal(root.left, list);
        list.add(root.val);
        inorderTraversal(root.right, list);
    }
}

https://www.jiuzhang.com/problem/search-range-in-binary-search-tree/ 

public class Solution {
    /**
     * @param root: param root: The root of the binary search tree
     * @param k1: An integer
     * @param k2: An integer
     * @return: return: Return all keys that k1<=key<=k2 in ascending order
     */
    public List<Integer> searchRange(TreeNode root, int k1, int k2) {
        // write your code here
        if (root == null) return null;
        ArrayList<Integer> range = new ArrayList<>();
        travel(root, k1, k2, range);
        return range;
    }

**    private void travel(TreeNode root, int k1, int k2, ArrayList<Integer> list) {**
**        if (root == null) return;**

// 剪枝，如果当前节点小于等于k1，不必访问左子树**
**
**        if(root.val > k1) {**
**            travel(root.left, k1, k2, list);**
**        } **
**        if (root.val >= k1 && root.val <= k2) {**
**            list.add(root.val);**
**        }**
// 剪枝，如果当前节点大于等于k2，不必访问右子树**
**
**        if (root.val < k2) {**
**            travel(root.right, k1, k2, list);**
**        }**
**    }**
**}**

没有剪枝

**private void travel(TreeNode root, int k1, int k2, ArrayList<Integer> list) {**
**        if (root == null) return;**
**
**
**        travel(root.left, k1, k2, list);**
**        if (root.val >= k1 && root.val <= k2) {**
**            list.add(root.val);**
**        }**
**        travel(root.right, k1, k2, list);**
**    }**

