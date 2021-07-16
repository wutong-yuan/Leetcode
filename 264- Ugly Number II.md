# 264. Ugly Number II

**# 264. Ugly Number II**
# 

**_Approach1: use heap_**
**_
_**
class Solution {
    public int nthUglyNumber(int n) {
        PriorityQueue<Long> heap = new PriorityQueue<>();
        Set<Long> seen = new HashSet<>();
        
        int[] factors = new int[3];
        factors[0] = 2;
        factors[1] = 3;
        factors[2] = 5;
        
        heap.offer(1L);
        seen.add(1L);
        long currentUgly = 1;
        long newUgly = 0;
        
        for (int i = 1; i <= n; i++) {
            currentUgly = heap.poll();
            for (int factor : factors) {
                newUgly = factor * currentUgly;
                if (!seen.contains(newUgly)) {
                    seen.add(newUgly);
                    heap.offer(newUgly);
                }
            }
        }
        return (int)currentUgly;
    }
}

**_Approach 2_**

public int nthUglyNumber(int n) {
        int[] nums = new int[n];
        int index2 = 0, index3 = 0, index5 = 0;
        nums[0] = 1;
        for(int i = 1; i < nums.length; i++){
            nums[i] = Math.min(nums[index2] * 2, Math.min(nums[index3] * 3, nums[index5] * 5));
            if(nums[i] == nums[index2] * 2)
                index2++;
            if(nums[i] == nums[index3] * 3)
                index3++;
            if(nums[i] == nums[index5] * 5)
                index5++;
        }
        return nums[n - 1];
    }

