# 1650 Lowest common ancestor of Binary Tree III - with parent pointer
https://www.youtube.com/watch?v=31KtJn5IS9Q 

![1650 Lowest common ancestor of Binary Tree III - with parent pointer](images/1650%20Lowest%20common%20ancestor%20of%20Binary%20Tree%20III -%20with%20parent%20pointer.png)

/*
// Definition for a Node.
class Node {
    public int val;
    public Node left;
    public Node right;
    public Node parent;
};
*/

class Solution {
    public Node lowestCommonAncestor(Node p, Node q) {
        Set<Node> ancestors = new HashSet<>();
        
        while(p != null) {
            ancestors.add(p);
            p = p.parent;
        }
        
        while (q != null) {
            if(ancestors.contains(q)) {
                return q;
            }
           q = q.parent;
        }
        return null;
    }
}
![1650 Lowest common ancestor of Binary Tree III - with parent pointer-1](images/1650%20Lowest%20common%20ancestor%20of%20Binary%20Tree%20III -%20with%20parent%20pointer-1.png)

https://gist.github.com/theinterviewsage/ba227c7fd55d4f0f232c8efed115b6aa 
