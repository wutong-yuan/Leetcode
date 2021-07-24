# 403. Frog Jump

**# 403. Frog Jump**
# 

class Solution {
    public boolean canCross(int[] stones) {
        int n = stones.length;
        // map is used to store <stone, steps can jump from this stone>
        Map<Integer, Set<Integer>> map = new HashMap<>();
        for (int i = 0; i < n; i++) {
            int stone = stones[i];
            map.put(stone, new HashSet<Integer>());
        }
        int lastStone = stones[n - 1];
        // first stone can jump one step
        map.get(stones[0]).add(1);
        
        for (int i = 0; i < n; i++) {
            int stone = stones[i];
            
                // for each step in the step sets
            for (int jump : map.get(stone)) {
                // get the next reachable stone
                int nextStone = stone + jump;

                if (nextStone == lastStone) return true;

                // for all the stones in the array stones, we have initialize the set for them. The set size is 0 but the set itself is not null
                // as new HashSet<>() 
                Set<Integer> nextStoneStepSet = map.get(nextStone);
                // add applicable jumps for the reached stone
		// if the nextStoneStepSet == null, meaning that reachable stone is not in our stone list
                if (nextStoneStepSet != null) {
                     nextStoneStepSet.add(jump);
                    if (jump - 1 > 0) {
                        nextStoneStepSet.add(jump - 1);
                    }
                    nextStoneStepSet.add(jump + 1);
                }
            }
        }
        return false;
    }
}
