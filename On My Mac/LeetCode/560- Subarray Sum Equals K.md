# 560. Subarray Sum Equals K

**# 560. Subarray Sum Equals K**

class Solution {
    public int subarraySum(int[] nums, int k) {
        Map<Integer, Integer> sumFrequencyMap = new HashMap<>();
        int count = 0;
        int n = nums.length;
        int preSum = 0;
        sumFrequencyMap.put(0, 1);
        
        for (int i = 0; i < n; i++) {
            preSum += nums[i];
            int reminder = preSum - k;
            if (sumFrequencyMap.containsKey(reminder)) {
                count += sumFrequencyMap.get(reminder);
            } 
            sumFrequencyMap.put(preSum, sumFrequencyMap.getOrDefault(preSum, 0) + 1);
        }
        
        return count;
    }
}

