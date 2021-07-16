# 373. Find K Pairs with Smallest Sums

**# 373. Find K Pairs with Smallest Sums**
# 

class Element {
    int index1;
    int index2;
    int sum;
    
    public Element(int index1, int index2, int sum) {
        this.index1 = index1;
        this.index2 = index2;
        this.sum = sum;
    }
}
class Solution {
    private Comparator<Element> elemComparator = new Comparator<Element>() {
        public int compare(Element a, Element b) {
            return a.sum - b.sum;
        }
    };
    public List<List<Integer>> kSmallestPairs(int[] nums1, int[] nums2, int k) {
        PriorityQueue<Element> minHeap = new PriorityQueue<>(elemComparator);
        List<List<Integer>> result = new ArrayList<>();
        if(nums1 == null || nums1.length == 0 || nums2 == null || nums2.length == 0 || k <= 0) return result;

        
        int m = nums1.length;
        int n = nums2.length;
        for (int i = 0; i < m; i++) {
            minHeap.offer(new Element(i, 0, nums1[i] + nums2[0]));
        }
        for (int i = 0; i < **_Math.min(k, m * n);_** i++) {
            Element tempElem = minHeap.poll();
            int index1 = tempElem.index1;
            int index2 = tempElem.index2;
            ArrayList<Integer> tempList = new ArrayList<>();
            tempList.add(nums1[index1]);
            tempList.add(nums2[index2]);
            
            if(index2 + 1 < n) {
                minHeap.offer(new Element(index1, index2 + 1, nums1[index1] + nums2[index2 + 1]));
            }
           result.add(tempList);
        }
        return result;
    }
}
