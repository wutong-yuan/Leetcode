# 198. House Robber

**# 198. House Robber**

# 

**_Brute force _**
class Solution {
    int max = 0;
    public int rob(int[] nums) {
        if (nums.length == 1)   return nums[0];
        backtrack(nums, 0, new ArrayList<>());
        return max;
    }
    
    private void backtrack(int[] nums, int start, ArrayList<Integer> tempList) {
        if (start >= nums.length) {
            int sum = 0;
            for (int i = 0; i < tempList.size(); i++) {                
                sum += tempList.get(i);
            }
            max = Math.max(sum, max);
            return;
        };
        
        int sum = 0;
        for (int i = start; i < nums.length; i++) {
            tempList.add(nums[i]);
            backtrack(nums, i + 2, tempList);
            tempList.remove(tempList.size() - 1);            
        }
    }
}

**_DP - much faster_**
class Solution {
    public int rob(int[] nums) {
        int rob1 = 0;
        int rob2 = 0;
        
        
        for (int i = 0; i < nums.length; i++) {
            int temp = Math.max(nums[i] + rob1, rob2);
            rob1 = rob2;
            rob2 = temp;
        }
        
        return rob2;
    }
}
