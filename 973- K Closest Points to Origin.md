# 973. K Closest Points to Origin

**973. K Closest Points to Origin**
# 

class Solution {
    public int[][] kClosest(int[][] points, int k) {
        PriorityQueue<int[]> maxHeap = new PriorityQueue<>(new Comparator<int[]>() {
            public int compare(int[] point1, int[] point2) {
                return getDistance(point2) - getDistance(point1);
            }
        });
        
        for (int[] point : points) {
            maxHeap.offer(point);
            if (maxHeap.size() > k) {
                maxHeap.poll();
            }
        }
        
        int[][] result = new int[k][2];
        int index = k;
        while (index > 0) {
            index--;
            result[index] = maxHeap.poll();
        }
        return result;
    }
    
    private int getDistance(int[] point) {
        int x = point[0];
        int y = point[1];
        int distance = x * x + y * y;
        return distance;
    }
}
