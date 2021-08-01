# LintCode 545 · Top k Largest Numbers II

**# LintCode 545 · Top k Largest Numbers II**
**
**
public class Solution {
    private PriorityQueue<Integer> minHeap;
    private int maxSize;
    /*
    * @param k: An integer
    */public Solution(int k) {
        // do intialization if necessary
        this.maxSize = k;
        minHeap = new PriorityQueue<Integer>();
    }

    /*
     * @param num: Number to be added
     * @return: nothing
     */
    public void add(int num) {
        // write your code here
        if (minHeap.size() < maxSize) {
            minHeap.offer(num);
        }else if (num > minHeap.peek()) {
            minHeap.poll();
            minHeap.offer(num);
        }
    }

    /*
     * @return: Top k element
     */
    public List<Integer> topk() {
        // write your code here
        List<Integer> list = new ArrayList<>();
        Iterator it = minHeap.iterator();
        while (it.hasNext()) {
**_// need to cast to integer here. Otherwise, it would have an error_**
            list.add((Integer) it.next());
        }
        Collections.sort(list, Collections.reverseOrder());
        return list;
    }
}

![LintCode 545 · Top k Largest Numbers II](images/LintCode%20545%20·%20Top%20k%20Largest%20Numbers%20II.png)

