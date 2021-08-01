# LintCode  486 · Merge K Sorted Arrays

# LintCode  **# 486 · Merge K Sorted Arrays**
# 

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

public class Solution {

    private Comparator<Element> elementComparator = new Comparator<Element>() {
        public int compare(Element left, Element right) {
            return left.val - right.val;
        }
    };
    /**
     * @param arrays: k sorted integer arrays
     * @return: a sorted array
     */
    public int[] mergekSortedArrays(int[][] arrays) {
        // write your code here
        if (arrays == null || arrays.length == 0) return new int[0];

        int totalSize = 0;
        PriorityQueue<Element> minHeap = new PriorityQueue<>(arrays.length, elementComparator);
        for (int i = 0; i < arrays.length; i++) {
            if(arrays[i].length > 0) {
                Element elem = new Element(arrays[i][0], i, 0);
                minHeap.offer(elem);
                totalSize += arrays[i].length;
            }
            
        }

        int[] result = new int[totalSize];
        int index = 0;
        while (!minHeap.isEmpty()) {
            Element elem = minHeap.poll();
            int row = elem.row;
            int col = elem.col;
            result[index] = elem.val;
            index++;
            if (col + 1 < arrays[row].length) {
                Element newElem = new Element(arrays[row][col + 1], row, col + 1);
                minHeap.offer(newElem);
            }
        }

        return result;
    }
}
