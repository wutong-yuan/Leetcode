# 90 Subset II

# 90 Subset **# II**
**
**
**
**
class Solution {
    public List<List<Integer>> subsetsWithDup(int[] nums) {
        List<List<Integer>> result = new ArrayList<>();
        List<Integer> subset = new ArrayList<>();
        Arrays.sort(nums);
        
        helper(nums, result, subset, 0);
        
        return result;
    }
    
    public void helper(int[] nums, List<List<Integer>> result, List<Integer> subset,
                      int startIndex) {
        result.add(new ArrayList<>(subset));
        
        for (int i = startIndex; i < nums.length; i++) {
            **if (i >= 1 && nums[i] == nums[i - 1] && i > startIndex) {**
**                continue;**
**            } // the only difference with subset 1 and this is how we avoid duplicate subset**

            subset.add(nums[i]);
            helper(nums, result, subset, i + 1);
            subset.remove(subset.size() - 1);
        }
    }
}
