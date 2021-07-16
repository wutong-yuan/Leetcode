# 1086. High Five

**# 1086. High Five**
# 

利用**map**与优先队列即可，找到对应的人的成绩，**pop**出前**5**个即可。**
**

class Solution {
    public int[][] highFive(int[][] items) {
        Map<Integer, PriorityQueue<Integer>> map = new HashMap<>();
        
        for (int[] item : items) {
            int id = item[0];
            int score = item[1];
            if (!map.containsKey(id)) {
                map.put(id, new PriorityQueue<Integer>());
            }
            PriorityQueue<Integer> queue = map.get(id);
            if (queue.size() < 5) {
                queue.offer(score);
            } else if (score > queue.peek()) {
                queue.poll();
                queue.offer(score);
            }
        }
        
        int[][] result = new int[map.size()][2];
        int index = 0;
        for (Map.Entry<Integer, PriorityQueue<Integer>> entry : map.entrySet()) {
            int id = entry.getKey();
            PriorityQueue<Integer> queue = entry.getValue();
            int sum = 0;
            int average = 0;
            for (int i = 0; i < 5; i++) {
                sum += queue.poll();
            }
            average = sum / 5;
            result[index][0] = id;
            result[index][1] = average;
            index++;
        }
        return result;
    }
}
