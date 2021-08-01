# 368. Largest Divisible Subset

**# 368. Largest Divisible Subset**
# 

class Solution {
    public List<Integer> largestDivisibleSubset(int[] nums) {
        int n = nums.length;
        Arrays.sort(nums);
        
        List<Integer>[] map = new List[n];
        for (int i = 0; i < n; i++) {
            map[i] = new ArrayList<>();
        }
        
        List<Integer> result = new ArrayList<>();
        List<Integer> lastOne = new ArrayList<>();
**        lastOne.add(nums[n - 1]);**
**        map[n - 1] = lastOne;**
**// if we do this way, we need to consider the nums.length == 1. Because the following for loop will execute only if the length is greater than 1.**
**        if (nums.length == 1) {**
**            result.add(nums[0]);**
**            return result;**
**        }**

        
        for (int i =** nums.length - 2**; i >= 0; i--) {
            List<Integer> tempLargest = new ArrayList<>();  
            
            for (int j = i + 1; j < nums.length; j++) {
                if (nums[j] % nums[i] == 0) {
                    if (tempLargest.size() < map[j].size()) {
                        tempLargest = map[j];
                    }
                }
            }
            map[i].add(nums[i]);
            map[i].addAll(tempLargest);
            if (map[i].size() > result.size()) {
                result = map[i];
            }
        }
        return result;
        
    }
}

**_Or we do the following_**

class Solution {
    public List<Integer> largestDivisibleSubset(int[] nums) {
        int n = nums.length;
        Arrays.sort(nums);
        
        List<Integer>[] map = new List[n];
        for (int i = 0; i < n; i++) {
            map[i] = new ArrayList<>();
        }
        
        List<Integer> result = new ArrayList<>();
        
        for (int **i = nums.length - 1;** i >= 0; i--) {
            List<Integer> tempLargest = new ArrayList<>();  
            
            for (int j = i + 1; j < nums.length; j++) {
                if (nums[j] % nums[i] == 0) {
                    if (tempLargest.size() < map[j].size()) {
                        tempLargest = map[j];
                    }
                }
            }
            map[i].add(nums[i]);
            map[i].addAll(tempLargest);
            if (map[i].size() > result.size()) {
                result = map[i];
            }
        }
        return result;
        
    }
    
}
