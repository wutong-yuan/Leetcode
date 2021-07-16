# 378. Kth Smallest Element in a Sorted Matrix

**378. Kth Smallest Element in a Sorted Matrix**
**
**
**Approach 1: use heap**

class Element {
    int val;
    int row;
    int col;
    
    public Element(int val, int row, int col) {
        this.val = val;
        this.row = row;
        this.col = col;
    }
}

class Solution {
    
    private Comparator<Element> elemComparator = new Comparator<Element>() {
        public int compare(Element left, Element right) {
            return left.val - right.val;
        }
    };
    
    public int kthSmallest(int[][] matrix, int k) {
        if (matrix == null || matrix.length == 0) return 0;
        PriorityQueue<Element> minHeap = new PriorityQueue<Element>(elemComparator);
        
        for (int i = 0; i < matrix.length; i++) {
            Element elem = new Element(matrix[i][0], i, 0);
            minHeap.offer(elem);
        }
        
        int result = 0;
        for (int i = 0; i < k - 1; i++) {
            Element elem = minHeap.poll();
            int row = elem.row;
            int col = elem.col;
            if (col + 1 < matrix[row].length) {
                Element newElem = new Element(matrix[row][col + 1], row, col + 1);
                minHeap.offer(newElem);
            }
        }
        result = minHeap.poll().val;
        
        return result;
    }
}

**_Use binary search_**

class Solution {
    public int kthSmallest(int[][] matrix, int k) {
        int n = matrix.length;
        int low = matrix[0][0];
        int high = matrix[n - 1][n - 1];
        while (low <= high) {
            int mid = low + (high - low) / 2;
            int count = binarySearch(matrix, mid);
            if (count >= k ) {
                high = mid - 1;
            } else {
                low = mid + 1;
            } 
        }
        
        return low;
    }
    
    private int binarySearch(int[][] matrix, int target) {
        int n = matrix.length;
        int count = 0;
        for (int[] row : matrix) {
            int low = 0;
            int high = n - 1;
            while (low <= high) {
                int mid = low + (high - low) / 2;
                if (row[mid] <= target) {
                    low = mid + 1;
                }else {
                    high = mid - 1;
                }
            }
            count += low;
        }
        
        return count;
    }
}
