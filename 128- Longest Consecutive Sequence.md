# 128. Longest Consecutive Sequence

**128. Longest Consecutive Sequence **

https://www.youtube.com/watch?v=qgizvmgeyUM&list=PLgUwDviBIf0p4ozDR_kJJkONnb1wdx2Ma&index=22 

class Solution {
    public int longestConsecutive(int[] nums) {
        Set<Integer> tempMap = new HashSet<>();
        for (int i = 0; i < nums.length; i++) {
            tempMap.add(nums[i]);
        }
        
        int longest = 0;
        for (int i = 0; i < nums.length; i++) {
            if(!tempMap.contains(nums[i] - 1)) {
                int currentNum = nums[i];
                int counter = 1;
                
                while (tempMap.contains(currentNum + 1)) {
                    currentNum++;
                    counter++;
                }
                longest = Math.max(counter, longest);
            }
        }
        return longest;
    }
} 
