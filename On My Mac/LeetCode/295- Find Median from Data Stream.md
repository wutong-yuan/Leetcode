# 295. Find Median from Data Stream

**# 295. Find Median from Data Stream**

### Approach 1: use array sort each time to find the medium

class MedianFinder {
    ArrayList<Integer> numList;

    /** initialize your data structure here. */
    public MedianFinder() {
        numList = new ArrayList<Integer>();
    }
    
    public void addNum(int num) {
        this.numList.add(num);
    }
    
    public double findMedian() {
        if (this.numList.size() == 0 || this.numList == null) return 0.0;
        int size = numList.size();
        double median = 0.0;
        Collections.sort(this.numList);
        if(size % 2 != 0) {
            median = numList.get(size / 2) / 1.0;
            return median;
        }
        median = (numList.get(size / 2 - 1) + numList.get(size / 2)) / 2.0;
        return median;
    }
}

/**
 * Your MedianFinder object will be instantiated and called as such:
 * MedianFinder obj = new MedianFinder();
 * obj.addNum(num);
 * double param_2 = obj.findMedian();
 */

**_Approach 2_**_：_**_ use heap_**
**_
_**
**_xhttps://www.programcreek.com/2015/01/leetcode-find-median-from-data-stream-java/_**

class MedianFinder {

    private PriorityQueue<Integer> minHeap;
    private PriorityQueue<Integer> maxHeap;
    
    /** initialize your data structure here. */
    public MedianFinder() {
        minHeap = new PriorityQueue<>();
        maxHeap = new PriorityQueue<>(Comparator.reverseOrder());
    }
    
    public void addNum(int num) {
        minHeap.offer(num);
        int minOfMinHeap = minHeap.poll();
        maxHeap.offer(minOfMinHeap);
        
        if (minHeap.size() < maxHeap.size()) {
            int maxOfMaxHeap = maxHeap.poll();
            minHeap.offer(maxOfMaxHeap);
        }
    }
    
    public double findMedian() {
        if (minHeap.size() > maxHeap.size()) {
            return minHeap.peek();
        }
        return (minHeap.peek() + maxHeap.peek()) / 2.0;
    }
}

/**
 * Your MedianFinder object will be instantiated and called as such:
 * MedianFinder obj = new MedianFinder();
 * obj.addNum(num);
 * double param_2 = obj.findMedian();
 */

**_Extenstion: LintCode 81 · Find Median from Data Stream_**
**_
_**
**The median is not equal to median in math.**

The median is the number that in the middle of a sorted array, if there are n numbers in a sorted array A, the median is A[(n - 1) / 2] .
For example, if A=[1,2,3], the median is A[(3-1)/2] = A[1] = 2, if A=[1,19], median is A[(2-1)/2] = A[0] = 1.
**_
_**

public class Solution {
    private PriorityQueue<Integer> minHeap;
    private PriorityQueue<Integer> maxHeap;

    public Solution() {
        // do initialize if it is necessary
        minHeap = new PriorityQueue<Integer>();
        maxHeap = new PriorityQueue<Integer>(Comparator.reverseOrder());
    }

    /**
     * @param val: An integer
     * @return: nothing
     */
    public void add(int val) {
        // write your code here
        minHeap.offer(val);
        maxHeap.offer(minHeap.poll());

        if (minHeap.size() < maxHeap.size()) {
            minHeap.offer(maxHeap.poll());
        }
    }

    /**
     * @return: return the median of the data stream
     */
**    public int getMedian() {**
**        // write your code here**
**        if (minHeap.size() > maxHeap.size()) {**
**            return minHeap.peek();**
**        }**
**        return maxHeap.peek();**
**    }**

}

