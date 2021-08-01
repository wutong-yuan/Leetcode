# 78 Subset

https://leetcode.com/problems/subsets/discuss/27281/A-general-approach-to-backtracking-questions-in-Java-(Subsets-Permutations-Combination-Sum-Palindrome-Partitioning) 
  
Above is nice but not easy to understand.

Below is a much easier method to understand. 
https://www.youtube.com/watch?v=REOH22Xwdkk&list=PLot-Xpze53lf5C3HSjCnyFghlW0G1HHXo&index=4 

class Solution {
    public List<List<Integer>> subsets(int[] nums) {
        List<List<Integer>> result = new ArrayList<>();
        ArrayList<Integer> tempList = new ArrayList<Integer>();
        backtrack(result, tempList, nums, 0);
        return result;
    }
    
    public void backtrack(List<List<Integer>> list, ArrayList<Integer> tempList, int[] nums, int i) {
        if(i >= nums.length) {
            list.add(new ArrayList<>(tempList));
            return;
        }
        // decision to include nums[i]
        tempList.add(nums[i]);
        backtrack(list, tempList, nums, i + 1);
        // decision not to inlcude nums[i]
        tempList.remove(tempList.size() - 1);
        backtrack(list, tempList, nums, i + 1);
    }
}

![78 Subset](images/78%20Subset.png)

![78 Subset-1](images/78%20Subset-1.png)

![78 Subset-2](images/78%20Subset-2.png)

